# Production platform components around Cirvice's fixed stack

- **Research date:** 2026-11-12
- **Wayfinder tickets:** [research question #13](https://github.com/charley81/cirvice/issues/13), constrained by the [planning map #1](https://github.com/charley81/cirvice/issues/1)
- **Fixed stack:** Next.js, React, TypeScript, PostgreSQL
- **Decision status:** shortlist and decision criteria only; this is not a final architecture decision.
- **Source policy:** current first-party documentation and pricing pages. Prices are public USD list prices before tax and should be rechecked before purchase.

## Executive findings

1. **Authentication is not tenant isolation.** Cirvice's difficult requirement is preventing one neighborhood from reading or changing another neighborhood's members, listings, inquiries, files, search records, jobs, or telemetry. Keep neighborhood membership and application roles authoritative in PostgreSQL even if an external service authenticates the user.
2. **PostgreSQL can provide a second authorization boundary.** Row-Level Security (RLS) can restrict rows by policy and defaults to deny when enabled without a policy. Table owners and `BYPASSRLS` roles normally bypass it, so the runtime role and migration/maintenance roles must be deliberately separated. [`FORCE ROW LEVEL SECURITY` and negative tests are essential](https://www.postgresql.org/docs/current/ddl-rowsecurity.html).
3. **A shared schema with an immutable `neighborhood_id` is the credible launch baseline to evaluate.** A database per neighborhood is stronger physical isolation but multiplies migrations, pooling, backups, support, and reporting. Revisit it only if contractual isolation, very large tenants, or noisy-neighbor requirements emerge.
4. **PostgreSQL-native search and jobs can defer extra systems.** PostgreSQL full-text search plus `pg_trgm` is credible at first-neighborhood scale; PostgreSQL-backed jobs are also credible if a continuously running worker is available. External services become valuable when product requirements—not fashion—demand stronger relevance, long workflows, or elastic worker execution.
5. **Consolidation and portability pull in opposite directions.** Supabase can combine database, auth, storage, queues, and logs with low operating burden. Vercel plus Neon/R2/independent services spreads failure domains and keeps interfaces more replaceable, but creates more vendors and dashboards. Render offers a conventional Node/container path with fewer serverless constraints.
6. **Private-community data should not leak into analytics or observability.** Do not send addresses, email addresses, inquiry text, listing free text, cookies, tokens, signed URLs, or upload contents to analytics, logs, replay, or error tools. Use pseudonymous account and neighborhood IDs, allowlisted event properties, short retention, and sampling.

## Cross-cutting production requirements

These requirements should survive whichever products are selected:

- Every neighborhood-owned relational row carries `neighborhood_id`; tenant-crossing foreign keys and uniqueness rules include it where practical.
- Server code checks current membership and role. Database RLS independently restricts ordinary runtime access. The runtime role must not own protected tables or have `BYPASSRLS`.
- Removal or suspension takes effect promptly. Do not rely only on long-lived JWT role claims that can remain stale.
- Object metadata, search documents, job payloads, caches, and telemetry include a non-PII neighborhood identifier and are authorized independently.
- Preview/test environments use synthetic or sanitized data. Database branches copied from production are not automatically privacy-safe.
- Backups, object storage, and external search indexes have separate restore/rebuild procedures.
- All external effects—email, webhooks, file processing—are idempotent and safe under retries.
- Every provider has a documented export/exit path, retention policy, deletion procedure, cost alert, and least-privilege credential model.

## 1. Authentication and authorization support

| Option | Capability and authorization fit | Tenant isolation, operations, portability, privacy | Current cost signals |
|---|---|---|---|
| **Better Auth** | TypeScript-first authentication and authorization framework with sessions, social login, 2FA, passkeys, a built-in limiter, database management, and an [organization/access-control plugin](https://www.better-auth.com/docs/plugins/organization). It fits an application-owned membership model because Cirvice can keep neighborhood eligibility, administrator roles, suspensions, and invitations in its own schema. | Auth data stays in Cirvice's database and the framework is open source, giving the best data ownership and low provider lock-in. It does **not** make domain authorization or RLS correct automatically. Cirvice owns upgrades, session incidents, email verification, recovery, abuse defenses, and availability. See the [official introduction](https://www.better-auth.com/docs/introduction). | No per-user core license; infrastructure and engineering/on-call time are the meaningful costs. |
| **Supabase Auth** | Password, magic link/OTP, social login, passkeys, SSO, JWTs, hooks, and direct integration with PostgreSQL RLS. Supabase explicitly positions Auth tokens plus RLS as its authorization model. [Auth overview](https://supabase.com/docs/guides/auth) | Strong fit when Supabase PostgreSQL is also used: user identity and application data can be connected in one database, while RLS remains the enforcement layer. Service-role credentials bypass RLS and require strict server-only handling. Moderate ecosystem coupling; ordinary PostgreSQL data and policies remain portable, while auth workflows and SDKs require migration work. | [Free](https://supabase.com/pricing) includes 50,000 MAU. Pro starts at **$25/month**, includes 100,000 MAU, then $0.00325/MAU; that plan also bundles database and storage allowances. |
| **Clerk** | Polished Next.js SDKs and UI, account management, invitations, organizations, roles, and permissions. Clerk's [Organizations guide](https://clerk.com/docs/organizations/overview) says to store organization IDs with resources and warns that filtering by organization does not itself authorize access. | Lowest auth UI burden, but identity/session data and workflows are vendor-managed. Database authorization and RLS are still required. A neighborhood should not be modeled as a Clerk Organization without checking commercial limits: included organizations allow only 20 members, far below the expected first-neighborhood population. Cirvice could instead use Clerk only for identity and keep memberships entirely in PostgreSQL. | [Hobby](https://clerk.com/pricing) includes 50,000 monthly retained users. Pro is **$25/month** or $20/month billed annually. The Enhanced B2B add-on is **$100/month** or $85/month annually and removes the 20-member Organization limit. |

### Authentication shortlist

- **Evaluate Better Auth** when data ownership and portability outweigh the burden of owning the auth service.
- **Evaluate Supabase Auth** when an integrated PostgreSQL/RLS platform is already a leading hosting candidate.
- **Evaluate Clerk** when prebuilt account UX and managed operations justify external identity dependence; keep neighborhood membership in PostgreSQL unless the Enhanced B2B economics are acceptable.

Regardless of provider, model Cirvice authorization separately: `account`, `neighborhood`, `membership`, membership status, administrator grants, provider/listing ownership, moderation powers, and suspension state. Authentication-provider roles should not become the only source of truth.

## 2. ORM and query tooling

| Option | Capabilities and PostgreSQL fit | Isolation, operations, portability, lock-in, cost |
|---|---|---|
| **Drizzle ORM + Drizzle Kit** | SQL-like relational and query APIs, standard database drivers, generated migrations, and direct support for PostgreSQL roles and [RLS policies](https://orm.drizzle.team/docs/rls). Its [overview](https://orm.drizzle.team/docs/overview) emphasizes SQL transparency, low dependencies, and serverless use. | Strongest fit when PostgreSQL features and reviewed SQL are first-class. Low runtime/provider lock-in. Requires SQL competence and disciplined migration review; its RLS tooling does not remove the need to test the emitted policies. Open source. |
| **Prisma ORM** | Generated type-safe client, schema workflow, migrations, Studio, transactions, and broad adoption. PostgreSQL-specific or optimized operations can use [TypedSQL/raw queries](https://www.prisma.io/docs/orm/prisma-client/using-raw-sql/raw-queries). [ORM overview](https://www.prisma.io/docs/orm/overview/introduction/what-is-prisma) | Strong developer ergonomics, but a larger ORM-specific schema/client abstraction. RLS, extensions, triggers, partial indexes, and specialized SQL may require custom SQL migrations. Never treat client middleware or a global query filter as the tenant boundary. Core ORM is open source; hosted Prisma products are optional. |
| **Kysely** | Thin, type-safe SQL query builder with inferred result types and explicit escape hatches. [Official introduction](https://www.kysely.dev/docs/intro) | Highest SQL visibility and low framework lock-in, but least batteries-included. The team must choose schema type generation and migration conventions. Good fit for a SQL-strong team that wants ordinary SQL to remain obvious. Open source. |

### ORM decision criteria

Prefer the option that makes these tasks clearest and safest: reviewing migrations, establishing request-scoped RLS context inside transactions, using connection pools correctly, expressing PostgreSQL indexes/extensions, and testing real SQL. Benchmark only after correctness and maintainability; ORM microbenchmarks should not decide the architecture.

## 3. User uploads

| Option | Authorization and tenant fit | Operations, portability, scaling, privacy, cost |
|---|---|---|
| **Cloudflare R2** | S3-compatible object storage with [presigned URLs](https://developers.cloudflare.com/r2/api/s3/presigned-urls/). Cirvice must authorize each upload/read and store authoritative object ownership in PostgreSQL; bucket prefixes are organization, not authorization. | Low storage/egress cost and good S3 API portability. Adds a control plane and has no native relational authorization. [Pricing](https://developers.cloudflare.com/r2/pricing/): 10 GB-month, 1M Class A, and 10M Class B operations free monthly; Standard storage is $0.015/GB-month, Class A $4.50/M, Class B $0.36/M, internet egress free. |
| **Supabase Storage** | Storage metadata is protected through PostgreSQL RLS on `storage.objects`; uploads are denied by default without policies. This can align object access with neighborhood membership. [Access-control docs](https://supabase.com/docs/guides/storage/security/access-control) | Lowest integration burden with Supabase Auth/database. Service keys bypass RLS. Database backups do not restore deleted storage objects, so object recovery remains separate. [Pro pricing](https://supabase.com/pricing) includes 100 GB file storage and 250 GB cached egress; overages are $0.0213/GB storage and $0.03/GB cached egress. |
| **Amazon S3** | Mature IAM, lifecycle, replication, encryption, eventing, and [presigned upload/download URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html). | Deepest ecosystem and strong portability, but the highest setup burden for IAM, CORS, CDN, malware scanning, lifecycle, and cost controls. [Pricing](https://aws.amazon.com/s3/pricing/) varies by region, class, requests, retrieval, and transfer. Best fit when AWS is already an operating competency. |
| **Vercel Blob** | Public/private stores and direct client uploads integrate closely with Vercel. | Lowest effort on Vercel, highest hosting coupling. Private delivery streams through Functions and can incur both Blob and function-path transfer. [Pricing](https://vercel.com/docs/vercel-blob/usage-and-pricing): Hobby includes 1 GB storage/10 GB transfer; on-demand storage is $0.023/GB, simple ops $0.40/M, advanced ops $5/M, and Blob transfer $0.05/GB in the cited US region. |

For every option: use browser-to-store uploads; generate opaque keys; cap file size, dimensions, type, and count; inspect content rather than trusting MIME/extension; strip unnecessary image metadata; quarantine or scan risky formats; use short-lived signed reads for private material; and delete/revoke objects when membership or content state changes.

## 4. Transactional email

| Option | Capability and operational fit | Privacy, portability, scaling, cost |
|---|---|---|
| **Postmark** | Transactional-first service with API/SMTP, templates, transactional/broadcast Message Streams, bounce handling, event webhooks, and detailed delivery history. | Strong diagnostics and clear transactional separation. Review retained message content and disable open/click tracking where it adds no product value. [Pricing](https://postmarkapp.com/pricing): developer testing 100 emails/month; Basic **$15/month for 10,000**, then $1.80/1,000, with 45-day data retention. |
| **Resend** | TypeScript-friendly API, SMTP, templates, batch/scheduled sends, idempotency keys, and replayable/verifiable [webhooks](https://resend.com/docs/webhooks/introduction). | Very low integration burden and good fit with React Email. [Pricing](https://resend.com/pricing): Free 3,000 emails/month; Pro **$20/month for 50,000**, then $0.90/1,000. Standard email retention is 30 days. |
| **Amazon SES** | API/SMTP, IAM, configuration sets, reputation controls, and SNS event publishing for delivery, bounce, complaint, open, and click events. [Event data docs](https://docs.aws.amazon.com/ses/latest/dg/event-publishing-retrieving-sns-contents.html) | Lowest unit cost at volume, but domain setup, sandbox exit, reputation monitoring, event plumbing, and troubleshooting are Cirvice's burden. [À-la-carte pricing](https://aws.amazon.com/ses/pricing/) is $0.10/1,000 outbound emails plus attachment data and optional features. Best when AWS operations already exist or volume makes the savings material. |

Use an outbox/idempotency key so retries cannot duplicate invitations or inquiry notifications. Keep recipient addresses and rendered message bodies out of general logs. Treat authentication-email delivery as a production dependency and maintain a suppression/bounce process.

## 5. Search

| Option | Capabilities and authorization fit | Operations, portability, scaling, privacy, cost |
|---|---|---|
| **PostgreSQL full-text search + `pg_trgm`** | Native lexing, ranking, highlighting, GIN/GiST indexes, and indexed trigram similarity. [Full-text search](https://www.postgresql.org/docs/current/textsearch.html); [`pg_trgm`](https://www.postgresql.org/docs/current/pgtrgm.html) | Best tenant-isolation fit because search runs under the same transaction and RLS policies as source data. No index synchronization, second datastore, or vendor fee. Relevance tuning and search-as-you-type UX require more application work, and large/global search loads share database resources. |
| **Typesense Cloud or self-hosted** | Typo tolerance, faceting, geosearch, instant search, and API access control. [Scoped search keys](https://typesense.org/docs/guide/data-access-control.html) can cryptographically embed a non-overridable tenant filter. | Good portability because Typesense is self-hostable; Cloud removes cluster operations. External indexing introduces lag, deletion/reindex procedures, and another place private data can leak. Cloud uses dedicated clusters priced by memory/bandwidth and advertises no record or operation limits; use the [current calculator](https://cloud.typesense.org/pricing). |
| **Algolia** | Mature hosted relevance, faceting, typo tolerance, analytics, and low operational burden. Backend-generated [secured API keys](https://www.algolia.com/doc/guides/security/api-keys/how-to/user-restricted-access-to-data) can enforce record filters. | Fastest path to sophisticated hosted search, but strongest vendor/relevance-model lock-in and request-sensitive cost. External index authorization must fail closed. [Pricing](https://www.algolia.com/pricing/) includes 10,000 requests/month and 50,000 records on Free; paid usage currently lists 100,000 records included and metered requests/records. |

### Search shortlist

- Prototype **PostgreSQL FTS + `pg_trgm` first** against realistic listing/category/filter queries.
- Escalate to **Typesense** if typo tolerance, facets, geosearch, or query latency cannot meet measured targets without harming the primary database.
- Evaluate **Algolia** when minimizing search operations is worth higher lock-in and request/record pricing.

Keep private inquiry/message search in PostgreSQL unless a later audited requirement justifies replication. Never let a client-provided `neighborhood_id` filter be the only external-index authorization control.

## 6. App hosting and PostgreSQL

Next.js itself remains portable: official documentation supports a Node.js server, Docker container, static export, and platform adapters; Node and Docker support all framework features. [Next.js deployment options](https://nextjs.org/docs/app/getting-started/deploying)

| Pairing | Capabilities and scaling | Isolation, operations, portability, privacy, cost |
|---|---|---|
| **Vercel + Neon** | Vercel provides the most integrated Next.js deployment, previews, CDN, image optimization, Functions, firewall, and scaling. Neon provides PostgreSQL pooling, autoscaling/scale-to-zero, read replicas, and copy-on-write [database branches](https://neon.com/docs/introduction/branching). | Low app/DB operations and a strong preview workflow. Keep regions close and avoid making Vercel-only cache/storage primitives pervasive if exit flexibility matters. Neon remains ordinary PostgreSQL and documents `pg_dump` backups in addition to instant restore. [Vercel Pro](https://vercel.com/pricing) is **$20/month** with $20 usage credit. [Neon Launch pricing](https://neon.com/pricing) is $0.106/CU-hour plus $0.35/GB-month; Neon publishes about **$15/month** for a small intermittent database and $22 for a small always-on database. Launch history can be configured to seven days. |
| **Vercel + Supabase** | Combines the most integrated Next.js host with managed PostgreSQL, Auth, RLS, Storage, Queues/Cron, APIs, and logs. | Lowest number of separate data-platform vendors and strongest integrated RLS story. It also concentrates outage/blast-radius and platform dependence. Transaction pooling affects session state and prepared-statement choices. [Vercel Pro](https://vercel.com/pricing) is $20/month; [Supabase Pro](https://supabase.com/pricing) starts at **$25/month** and includes a Micro instance, 8 GB database disk, daily backups retained seven days, 100 GB files, and 100,000 MAU. PITR starts at $100/month. |
| **Render web service + Render Postgres** | Conventional long-running Node or Docker service, private networking, background workers/cron, managed PostgreSQL, pooling, PITR, replicas, and optional HA. [Next.js deployment](https://render.com/docs/deploy-nextjs-app) | Avoids serverless request/connection constraints and is straightforward to move as a Node server/container. Requires more capacity planning and lacks Vercel's deepest Next.js integration. [Pricing](https://render.com/pricing): a 512 MB web service starts at **$7/month** and a 1 GB PostgreSQL instance at **$19/month**; storage and stronger production capacity are extra. Paid databases receive PITR, while HA requires at least 1 CPU and a separately billed standby. [HA docs](https://render.com/docs/postgresql-high-availability) |

### Hosting/database gates

Require a tested restore, explicit RPO/RTO, connection-pool metrics, slow-query visibility, migration recovery, regional placement, spend ceilings, and standard `pg_dump` export regardless of provider. A provider's backup feature is not proven until Cirvice has restored it into an isolated environment and validated application behavior.

## 7. Background work and rate limiting

### Background work

| Option | Capabilities and tenant fit | Operations, portability, scaling, cost |
|---|---|---|
| **pg-boss + a worker service** | PostgreSQL-backed Node queue using `SKIP LOCKED`, transactional enqueue, retries, dead letters, cron, dependencies, and concurrency/rate policies. It can insert a job in the same transaction as the domain change. [Official repository](https://github.com/timgit/pg-boss) | Fewest systems and high data portability. Requires an always-running worker, queue-table maintenance, monitoring, and capacity isolation from transactional traffic. Open source; cost is worker/database capacity. Maintained by a small project, which is a supply-chain/support consideration. |
| **Supabase Queues + Cron** | `pgmq`-based durable queues with guaranteed delivery, visibility windows, archival, and RLS; Cron uses `pg_cron` for SQL/functions/HTTP. [Queues](https://supabase.com/docs/guides/queues); [Cron](https://supabase.com/docs/guides/cron) | Strong integrated option on Supabase and easy transactional enqueue. Cirvice still needs consumers, idempotency, retry/dead-letter policy, and monitoring. Supabase recommends no more than eight concurrent cron jobs and ten minutes per job. Cost consumes the existing database/compute allowance. |
| **Inngest** | Durable steps save progress, retry failed steps, wait without holding compute, and provide concurrency/throttling/rate controls, including per-tenant keys. [Durable steps](https://www.inngest.com/docs/features/inngest-functions/steps-workflows); [concurrency](https://www.inngest.com/docs/guides/concurrency) | Lowest orchestration burden for notifications and multi-step workflows, but creates workflow/runtime lock-in. External effects still need idempotency because a provider call can succeed before the step result is saved. [Pricing](https://www.inngest.com/pricing): Free 50,000 executions and five concurrent steps; Pro starts at **$99/month**. A run plus each step consumes executions. |
| **Trigger.dev** | Long-running TypeScript tasks on managed workers, retries, schedules, waits/checkpoints, queues, and per-tenant/shared concurrency. Tasks can run without request timeouts. [Task overview](https://trigger.dev/docs/tasks-overview); [concurrency](https://trigger.dev/docs/queue-concurrency) | Better fit for CPU/file processing and long tasks. Open source and self-hostable, but self-hosting is substantial; cloud deploys task bundles to Trigger.dev infrastructure. [Pricing](https://trigger.dev/pricing): Free includes $5 monthly credits and 20 concurrent runs; Hobby **$10/month**, Pro **$50/month**, plus per-run and per-second compute. |

Every handler should carry `neighborhood_id`, re-check current authorization/state when it runs, use a business idempotency key, bound retries, and expose failed/dead-letter work to an administrator. Assume an external side effect can happen more than once even when the queue's delivery claim is stronger.

### Rate limiting and abuse controls

- **Upstash Ratelimit + Redis** is connectionless and designed for serverless/edge runtimes, with multiple algorithms, per-identifier limits, multi-region support, analytics, and configurable fail-open timeouts. [SDK overview](https://upstash.com/docs/redis/sdks/ratelimit-ts/overview) Use keys such as `neighborhood:account:action`, not IP alone. [Pricing](https://upstash.com/pricing/redis): Free 500,000 commands/month; pay-as-you-go $0.20/100,000; fixed plans start at $10/month. The production SLA/multi-zone **Prod Pack is an additional $200/month per database**, an important cost cliff.
- **Vercel Firewall rate rules** are useful as a coarse outer layer for floods and automated abuse. [Vercel pricing](https://vercel.com/pricing) lists 1M allowed rate-limit requests/month included on Pro, then $0.50/M. They do not replace account-, neighborhood-, invitation-, inquiry-, or listing-level limits in application code.
- **Database constraints** remain the final invariant layer: invitation redemption count, one active membership/account, posting cooldown state, unique idempotency keys, and transactional quota changes cannot rely only on a cache.

Layer controls: edge/IP for floods; account/neighborhood/action for product abuse; database constraints for invariants; CAPTCHA or manual review for suspicious signup/listing activity.

## 8. Privacy-conscious analytics

| Option | Privacy and capability | Operations, portability, lock-in, cost |
|---|---|---|
| **Plausible Cloud or Community Edition** | Aggregate page/event analytics with no cookies or persistent identifiers. Raw IP and User-Agent are used to derive a daily identifier but not stored; hosted visitor data remains on European-owned EU infrastructure. [Data policy](https://plausible.io/data-policy) | Best privacy posture and simplest reporting, but intentionally weak for user-level longitudinal product analysis. Open source/self-hostable; Cloud avoids operations. [Current homepage pricing](https://plausible.io/#pricing) starts at **$9/month** for one site/up to 10,000 monthly pageviews, $14 Growth, $19 Business. |
| **Umami Cloud or self-hosted** | Cookie-free analytics with custom events, funnels, journeys, retention, and cohorts. It supports PostgreSQL when self-hosted. [FAQ](https://umami.is/docs/faq) | More product-analysis depth than Plausible while remaining open source and exportable. Cloud offers US/EU regions; self-hosting adds upgrades, database, and monitoring. [Pricing](https://umami.is/pricing): Hobby free for 100,000 events/one site; Pro **$20/month** for 1M events. Each pageview, custom event, and stored event property affects usage. |
| **PostHog Cloud EU** | Rich product analytics, feature flags, experiments, surveys, session replay, and error tracking. Cloud EU keeps event data in Frankfurt and provides privacy controls and a DPA. [Privacy docs](https://posthog.com/docs/privacy) | Highest capability and highest governance/data-volume burden. Autocapture, identified users, and replay can collect much more than Cirvice needs; self-hosting is officially unsupported for production guarantees and carries a large stack. [Pricing](https://posthog.com/pricing) includes 1M analytics events and 5,000 replays/month free, then usage billing with limits. |

### Analytics decision rule

Use **Plausible or Umami** if the launch question is aggregate adoption and conversion. Evaluate **PostHog** only if product funnels, flags, or experiments are important enough to justify a larger privacy program. Do not enable session replay on private inquiries, membership review, administrator tools, or forms containing sensitive text without explicit legal/privacy review and rigorous masking.

## 9. Error monitoring and logging

| Option | Capabilities | Operations, portability, privacy, cost |
|---|---|---|
| **Sentry** | First-party Next.js SDK covers browser, server, edge, source maps, errors, traces, logs, metrics, and optional replay. [Next.js guide](https://docs.sentry.io/platforms/javascript/guides/nextjs/) | Strongest error-workflow shortlist. Configure sampling and [server-side scrubbing](https://docs.sentry.io/security-legal-pii/scrubbing/); replay is high risk for a private marketplace. Data can be stored in US or EU, but some account/integration metadata remains US-hosted and the chosen region cannot be changed without a new organization. [Region docs](https://docs.sentry.io/organization/data-storage-location/) [Pricing](https://sentry.io/pricing/): Developer free with 5,000 errors; Team **$26/month** annually with 50,000 errors; Business $80. |
| **Axiom** | Central logs, traces, metrics, dashboards, alerts, and native [OpenTelemetry ingestion](https://axiom.co/docs/send-data/opentelemetry). | Strong logs/traces complement when platform log retention and querying are insufficient. OpenTelemetry reduces backend lock-in. Apply redaction before ingestion. [Pricing](https://axiom.co/pricing): Personal free with 30-day retention/25 GB storage; Cloud **$25/month** platform fee includes 1 TB loading compute, 100 GB-hours query compute, and 100 GB storage before usage charges. |
| **Better Stack** | Exceptions, logs, traces, metrics, uptime, incidents/on-call, and status pages in one platform. | Credible consolidation option if Cirvice wants monitoring plus incident workflow from one vendor. Compare its error depth with Sentry before consolidating. [Pricing](https://betterstack.com/pricing): Free includes 100,000 exceptions and 3 GB each of logs/traces retained three days; the Nano telemetry bundle is **$30/month** monthly or $25 annually for 40 GB each and 30-day log retention. |

Use **OpenTelemetry** for custom traces/logs where practical: it is an open-source, vendor-agnostic framework for traces, metrics, and logs, so changing backends does not require replacing all instrumentation. [OpenTelemetry overview](https://opentelemetry.io/docs/what-is-opentelemetry/)

A sensible evaluation sequence is one error tracker plus structured hosting logs first; add a dedicated log platform only when retention, cross-service correlation, or query needs justify it. Centralize redaction and use pseudonymous account/neighborhood IDs.

## 10. Testing

These tools are complementary rather than competing products, and all are open source:

| Layer | Shortlist | Production value |
|---|---|---|
| Unit/service | **Vitest** | Fast TypeScript tests, coverage, mocks, and watch mode. It is Vite-powered and requires current Node/Vite versions. [Guide](https://vitest.dev/guide/) |
| React behavior | **React Testing Library** | Tests DOM behavior as a user experiences it instead of component implementation details, improving accessibility and refactor resilience. [Introduction](https://testing-library.com/docs/react-testing-library/intro/) |
| External API simulation | **Mock Service Worker (MSW)** | Reusable network-level handlers in browser and Node for auth/email/upload failure paths without SDK-specific mocks. [Docs](https://mswjs.io/docs/) Do not use mocks as the only evidence for database authorization. |
| Real PostgreSQL integration | **Testcontainers for Node.js + PostgreSQL** | Throwaway real databases for migrations, constraints, transactions, extensions, and RLS. [Overview](https://node.testcontainers.org/); [PostgreSQL module](https://node.testcontainers.org/modules/postgresql/) |
| Browser end-to-end | **Playwright** | Chromium, Firefox, and WebKit, isolated browser contexts, parallel execution, traces, screenshots, and CI sharding. [Introduction](https://playwright.dev/docs/intro); [trace viewer](https://playwright.dev/docs/trace-viewer-intro) |

### Minimum production test gates

1. Apply every migration to an empty database and a production-like previous schema.
2. Run an authorization matrix against two neighborhoods and all roles: anonymous, applicant, approved member, provider, administrator, suspended/removed member, and platform maintenance role.
3. Prove cross-neighborhood denial for direct IDs, joins, search, files, jobs, cached responses, and administrator actions.
4. Test RLS with the **actual runtime database role**, not a superuser/table owner that bypasses policies.
5. Run Playwright flows for invitation/joining, approval/removal, listing moderation, private inquiry, notification, and private upload/download using separate browser contexts.
6. Test duplicate webhook/job/email delivery and timeout-after-success scenarios with stable idempotency keys.
7. Restore the database and object storage into an isolated environment and verify application behavior.
8. Load-test search/feed queries, pool saturation, image delivery, signup/invitation abuse paths, and job backlogs.

CI cost is primarily runner time rather than test-tool licensing. Keep traces/screenshots only for failures or short retention so browser artifacts do not become a privacy or storage problem.

## Shortlist of credible evaluation paths

These are deliberately **evaluation paths**, not recommendations to adopt whole bundles unchanged.

### A. Integrated PostgreSQL authorization path

- Supabase PostgreSQL + Auth + RLS + Storage, optionally Queues/Cron
- Drizzle or Kysely; Prisma remains viable if its ergonomics win in a spike
- Resend or Postmark
- PostgreSQL FTS/`pg_trgm`
- Sentry plus platform logs
- Plausible or Umami
- Vitest, React Testing Library, Testcontainers, Playwright, MSW

**Why evaluate:** lowest vendor count, coherent RLS/file authorization, public starting platform cost about **$25/month** plus app hosting.

**Main risks:** provider concentration, service-role bypass mistakes, platform coupling, and expensive PITR beyond seven-day daily backups.

### B. Best-of-breed managed/serverless path

- Vercel + Neon PostgreSQL
- Better Auth or Clerk identity, with Cirvice membership/authorization in PostgreSQL
- Drizzle, Kysely, or Prisma
- R2 or S3-compatible storage
- PostgreSQL search initially
- pg-boss on a worker, or Inngest/Trigger.dev when durable orchestration is justified
- Upstash for application rate limits
- Sentry; Axiom only when log needs justify it
- Plausible or Umami

**Why evaluate:** strongest Next.js operations, replaceable PostgreSQL/object interfaces, independent failure domains. Vercel Pro plus Neon's published small intermittent database is roughly **$35/month** before email, analytics, jobs, and monitoring.

**Main risks:** vendor/dashboard sprawl, network locality, auth and job cost cliffs, and inconsistent privacy/retention controls across services.

### C. Portable conventional-host path

- Render Node/Docker web service + Render PostgreSQL
- Better Auth or another database-owned identity/session model
- Drizzle/Kysely/Prisma
- R2 or S3
- PostgreSQL search
- pg-boss plus a Render background worker/cron
- Sentry and OpenTelemetry-compatible logs
- Plausible/Umami

**Why evaluate:** ordinary Node/container deployment, long-running workers, straightforward PostgreSQL portability, fewer serverless lifetime/connection constraints. Entry paid web + 1 GB database is about **$26/month** before worker, storage, email, and observability.

**Main risks:** more capacity planning, weaker framework-specific optimization, and materially higher cost when HA/standby and larger instances are required.

## Decision criteria and proof-of-concept questions

Before choosing components, run a narrow proof of concept around the hard boundaries rather than a generic CRUD demo:

1. **Authorization ownership:** Can a resident be removed and lose access immediately without waiting for a provider claim/token to expire?
2. **Tenant isolation:** Can the same policy protect listings, inquiries, moderation views, search, files, and jobs? What credentials bypass it?
3. **Operator safety:** Can an administrator investigate a case without receiving unrestricted cross-neighborhood access by default?
4. **Recovery:** What are the measured database and object-store RPO/RTO? Has restore actually been tested?
5. **Portability:** Export users, database, files, and search records in a trial exit. Which identifiers or workflows cannot be reconstructed?
6. **Runtime fit:** Do background work, uploads, database transactions, and connection pools fit the chosen host's execution model?
7. **Search threshold:** Does PostgreSQL meet typo tolerance, faceting, relevance, and p95 latency targets at projected and 10× data?
8. **Job threshold:** Are tasks simple transactional notifications, or do they require multi-day waits, per-tenant concurrency, replay, and long compute?
9. **Privacy:** What resident data reaches each subprocessor, in which region, for how long, and how is deletion propagated?
10. **Cost:** Model launch, 10× active residents, and an abuse spike. Include base plans, per-user/org limits, egress, image transforms, queue steps/retries, Redis HA/SLA, logs, traces, replay, backups/PITR, and support.
11. **Operational burden:** Count production dashboards, credentials, webhooks, status pages, incident contacts, and restore procedures—not just monthly invoice lines.
12. **Testing:** Can CI prove cross-neighborhood denial using the real PostgreSQL role and policies, not mocks?

The decision should optimize for demonstrable tenant isolation, recoverability, privacy, and operability at Cirvice's small initial scale while preserving credible exits. It should not optimize for the largest feature list or the currently fashionable vendor.
