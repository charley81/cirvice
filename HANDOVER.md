# Neighborhood Skills Marketplace — Codex Handoff

**Status:** Product discovery complete enough to begin specification and design; **implementation not authorized yet**
**Date:** November 11, 2026
**Working title:** Neighborhood Skills Marketplace (final name TBD)
**Document purpose:** Transfer product context, decisions, constraints, and next actions to Codex without losing discovery work.

---

## 1. Instruction to Codex

You are joining a new project at the **product definition and planning stage**. Read this document in full and treat the **Confirmed decisions** as requirements. Treat **Recommendations / open decisions** as proposals to examine, not choices already made. Do **not** immediately scaffold the application or write production code. First:

1. Review the product concept, target users, assumptions, trust boundaries, and MVP constraints.
2. Produce a concise **Product Brief**, **MVP Requirements / Acceptance Criteria**, **Information Architecture**, **Core User Flows**, and a proposed **Technical Architecture + Data Model**.
3. Identify conflicts, security risks, high-cost complexity, and scope creep. Recommend the smallest safe and useful first release.
4. Present any material decisions for approval before implementation. Keep questions focused; make sensible provisional recommendations rather than blocking progress over trivial details.
5. After specification approval, follow the user's design-first workflow in Section 12, then implement incrementally with tests, review, and commits.

**Project objective:** Build a real, neighborhood-focused full-stack web application with genuine users, while demonstrating production-quality frontend and backend engineering to potential employers.

---

## 2. Origin / Evidence of Demand

The product concept comes from a **real residential neighborhood of approximately 3,000 residents**. Residents already use an existing community Facebook group to:

- Request recommendations for local services.
- Advertise skills or services they can provide.
- Ask to borrow items.
- Sell items or promote local businesses.

The user discussed a **neighborhood skills-and-services marketplace** with residents and potential service providers. They expressed enthusiasm about having a dedicated platform. This is **qualitative early feedback**, not validated adoption, willingness to pay, or market-size proof.

The project evolved from a broad neighborhood bulletin board and borrowing platform to a **focused skills and paid-services directory**, because borrowing items raises theft/liability concerns and broad community features add complexity.

### Problem statement

Useful information about neighbors' skills and services is currently scattered across Facebook posts and difficult to find later. Residents who have valuable skills may lack an easy, dedicated way to showcase them to nearby customers. Neighbors seeking services may prefer to discover and support people they know are part of their community.

### Product promise

> Discover what your neighbors can do. Offer your skills, find local services, and support people in your own neighborhood.

---

## 3. Confirmed Product Decisions

These are agreed decisions, not implementation guesses.

1. **Private neighborhood model.** Only approved neighborhood members may browse the marketplace, view resident provider profiles, and contact providers. A public informational landing page may explain the product and invite residents to join.
2. **Single resident account.** Any approved resident can browse/hire and advertise their own services; there are no separate buyer and seller login types.
3. **Focus on skills and services.** The MVP is **not** a general-purpose neighborhood social network, classifieds site, borrowing platform, or marketplace for physical goods.
4. **Individual Service Providers only.** An Approved Member may offer professional or hobby-based services, skills, and talents that they personally perform. Cirvice does not support business profiles, business branding, teams, employees, or services performed by another person.
5. **Business ownership is irrelevant.** A member who owns or works for a business may offer their own work, but only under their member identity. They cannot advertise the business, use its name or logo, or link to its website or social-media account.
6. **Multiple services per Service Provider.** One member can offer unrelated services (e.g., web development, audio mixing/mastering, car washing) through a single Provider Profile, with each service represented by a separate Service Listing.
7. **Service discovery + inquiry is the core workflow.** A member finds a service and sends a request to the Service Provider. Service Providers can review/respond and track request status.
8. **No platform payment processing in MVP.** Users arrange fulfillment and payment outside the platform. No platform commissions, escrow, payment guarantees, or complex booking infrastructure in v1.
9. **Administrator-controlled access and moderation.** Membership approval, listing moderation/reporting, and revocation are needed from the start.
10. **One neighborhood to start.** Architect for future multi-neighborhood support and tenant isolation; launch first in the user's existing neighborhood.
11. **Mobile-first and well designed.** Discoverability, low friction, accessible UI, performance, and refined visual quality matter, but functionality takes precedence over elaborate animation.
12. **Real product + portfolio.** Aim for actual resident participation, plus a clearly labeled, **separate demo environment** with synthetic data so recruiters can explore the software even if adoption is initially low.

### Clarification on labels

"Approved neighborhood member" means community-access approval, **not** verified identity, criminal-background screening, professional license, insurance, or guaranteed service quality. Never imply that a Service Provider is certified merely because of neighborhood approval.

---

## 4. Target Users and Jobs to Be Done

### Resident seeking help

- **When** I need a service, **I want** to browse or search what people in my neighborhood offer, **so I can** quickly identify relevant options and request help.
- I want to see examples of work, descriptions, basic price guidance, and the member identity of the person who will perform the service.
- I want to inquire without exposing my personal contact details to everyone.

### Service Provider

- **When** I have a skill I can monetize, **I want** a simple public-to-members Provider Profile and Service Listings, **so I can** find local customers without creating a separate website.
- I may offer several unrelated skills and have different pricing for each.
- I personally perform every service I list, even if I also own or work for a business.
- I need to manage inquiries and pause services as needed.

### Neighborhood administrator

- **When** someone requests access, **I need** to approve, reject, revoke, or request more information.
- **When** inappropriate or suspicious content appears, **I need** to review reports and moderate quickly with an audit trail.

---

## 5. MVP Definition and Scope

### v1 outcome

> An approved resident can create a service listing; another approved resident can find it and send an inquiry; the provider can respond; admins can maintain membership and listing safety.

### Must-have feature groups

**A. Accounts and neighborhood access**
- Account creation and sign-in / sign-out.
- Neighborhood membership request, pending state, admin approval/rejection/revocation.
- Server-enforced private access to all member-only content and routes.
- Support a resident being a customer and a provider with the same account.

**B. Member/provider profile**
- Member name, shown as first name and last initial by default, with the full surname optional; optional photo, short biography, and account settings.
- One Provider Profile per Approved Member, visible to other Approved Members only while it has at least one published Service Listing.
- No business names, logos, descriptions, websites, social-media links, home addresses, email addresses, or phone numbers.
- Only the Service Provider can edit their profile; administrators may hide or remove it but may not rewrite it.

**C. Service listings**
- Create, read, update, pause/unpublish, and delete own service listings.
- Title, description, category, optional photos / work examples, price type (starting price, hourly, fixed, or custom quote as appropriate), availability status.
- Every Service Listing describes work that its Service Provider personally performs.
- No business branding, external website links, or social-media links.
- Multiple Service Listings per Service Provider, with no fixed numeric limit at launch.
- Admin review / moderation before or after publication, according to final policy.

**D. Discovery**
- Category browsing; searchable listing titles, descriptions, and relevant profile fields.
- Filter by service category; sensible empty states.
- Listing details show provider, portfolio examples, price guidance, inquiry action, and appropriate disclaimers.

**E. Inquiries**
- An approved member sends a structured inquiry to a service provider.
- Private text exchanges or a minimal response thread (decide simplest viable implementation).
- Track statuses such as new, accepted, declined, cancelled, completed.
- Enforce valid status transitions and access control for customer, provider, and admin.
- No off-platform contact information required to be public.

**F. Administration and safety**
- Admin membership queue and decisions.
- Listing and user reports, admin removal/suspension, basic audit records.
- Rate limits / anti-abuse around invites, inquiries, uploads, and account creation.
- Clear privacy and conduct guidance; account deletion and data-removal handling.

### Out of scope for v1

- In-app payments, deposits, fees, commissions, insurance or guarantees.
- Escrow, refunds, disputes over payment, or job fulfillment claims.
- Public social newsfeed, general neighborhood announcements, item borrowing, item sales.
- Reviews/ratings, ranking algorithms, AI matching, maps/geolocation, cross-neighborhood browsing.
- Scheduling/calendar availability and instant booking.
- Mobile native apps, video calls, sophisticated chat/push infrastructure.
- License/background verification (but restrict or handle regulated/high-risk categories responsibly).

### Design principle

**Profiles and persistent service listings, not temporary social posts.** A member should be able to quickly find an actual service without scrolling an unstructured feed.

---

## 6. Suggested Information Architecture

### Public

- `/` — Marketing / introduction / why join
- `/join` — Membership and account entry (or authentication routes)
- `/membership-status` — Pending/approved/rejected/revoked messaging as appropriate
- Privacy policy, terms / community rules, basic contact/help

### Approved members

- `/discover` — Service search, category browse, filters
- `/services/[slug-or-id]` — Service detail
- `/providers/[id]` — Provider Profile for one Service Provider
- `/services/new` — Create service
- `/my-services` — Own listings and management
- `/inquiries` — Sent and received inquiry list
- `/inquiries/[id]` — Private inquiry thread/detail
- `/settings` — Member and profile settings

### Admin

- `/admin` — Admin overview
- `/admin/memberships` — Membership review and revocation
- `/admin/services` — Listing moderation
- `/admin/reports` — Reports and actions
- `/admin/categories` — Category maintenance (can initially be seeded in code if desired)

**Important:** Routes are proposals. Codex should propose a coherent route design and document roles / guards for each; the final URLs need not match exactly.

---

## 7. Core UX Journeys and Acceptance Tests

### Journey 1 — Join the community

1. New resident arrives at public landing page.
2. Creates an account and requests neighborhood access.
3. Sees a clear pending state and what happens next.
4. Admin reviews the request and approves/rejects.
5. Approved member can browse; pending/rejected members cannot see private listings or profiles, including via direct URLs or APIs.

**Acceptance criteria:** unauthorized access consistently fails server-side; decision and status changes are persisted; member receives clear feedback.

### Journey 2 — Publish a personal service

1. Approved member selects **Offer a Service**.
2. Completes basic service form: name, description, category, price style, optional photos.
3. Publishes or submits for moderation, depending on final policy.
4. Listing appears in discovery only when allowed.
5. The Service Provider can edit, pause, or delete the listing.

**Acceptance criteria:** validation errors are understandable; only the Service Provider can edit listing content; administrators may hide or remove content but may not rewrite it; hidden or paused listings are inaccessible to other members.

### Journey 3 — Offer multiple personal services

1. An Approved Member creates one Provider Profile without a separate provider application.
2. The member creates one or more Service Listings for unrelated services, skills, or talents.
3. Each Service Listing identifies the member and describes work that the member personally performs.
4. The Provider Profile becomes visible to other Approved Members only when at least one Service Listing is published.

**Acceptance criteria:** the member must be approved; each service is personally performed by the member; business branding and external links are not allowed; only the member can edit their profile and listings.

### Journey 4 — Discover and inquire

1. Approved member searches or browses a category.
2. Opens a service detail and views provider information.
3. Submits inquiry with description and optional preferred timing.
4. Provider sees the request and replies / accepts or declines.
5. Both participants can see allowed status updates; unrelated users cannot.

**Acceptance criteria:** correct access controls, no leaking customer contact details, valid status transitions, abuse/report mechanisms.

### Journey 5 — Admin handles a report

1. Member reports a service or message.
2. Admin reviews context, records action, and can disable listing or membership.
3. Affected content becomes inaccessible according to policy.

**Acceptance criteria:** moderation is auditable; admin permissions are server enforced; sensitive data is not indiscriminately exposed.

---

## 8. Trust, Privacy, and Community Controls

The application is for a real neighborhood. Security is a product requirement, not a stretch goal.

- **Neighborhood isolation:** authorize every read and write by neighborhood and membership status; prevent cross-tenant IDOR attacks. Do not trust route params or client-side guards alone.
- **Account security:** use a mature authentication library, secure session handling, CSRF protection as applicable, and proper cookie configuration.
- **Membership checks:** invite codes may assist onboarding but do not prove residency; approval can be revoked. Do not automatically trust a shared invitation code.
- **Data minimization:** avoid storing or publishing precise addresses, identity documents, utility bills, unnecessary phone numbers, or minors' information in the MVP.
- **Provider trust claims:** no invented credentials or "background checked," "licensed," or "insured" labels without an actual verification workflow.
- **Regulated/high-risk services:** define an approved category policy; exclude or gate categories involving licensing, childcare, medical services, other high-liability work until safeguards exist.
- **User safety:** report/block abuse where practical, moderator controls, email/privacy boundaries, protection against spam and harassment.
- **Uploads:** validate type, size, ownership, and access; guard against malicious files and public object exposure.
- **Retention/deletion:** specify lifecycle for deleted listings, accounts, inquiry messages, and audit logs; legal/operational policies to be reviewed before public launch.
- **Avoid unapproved scraping/importing:** do not copy private Facebook posts or member details into production without permission.
- **Demo isolation:** synthetic user data must never be confused with real residents or actual completed jobs.

---

## 9. Technical Direction — Recommendations, NOT Final Decisions

The user wants employable full-stack skills with a modern JavaScript/TypeScript stack. Evaluate and justify options before scaffolding.

| Concern | Proposed choice |
|---|---|
| Web application | Next.js + React + TypeScript |
| Database | PostgreSQL |
| ORM | Drizzle |
| Authentication | Auth.js or Better Auth (evaluate fit) |
| Styling | Modern CSS approach (CSS Modules, StyleX, or Tailwind; choose deliberately) |
| Uploads | Supabase Storage or S3-compatible object storage |
| Email | Transactional provider such as Resend |
| Validation | Zod or equivalent shared schemas |
| Tests | Vitest + Playwright |
| Hosting | Vercel or another production-compatible provider |
| Observability | Minimal error monitoring, logs, and opt-in privacy-conscious analytics |

### Implementation expectations

- Strong TypeScript usage with clear component/server boundaries.
- Server-side authorization for membership, ownership, inquiries, and admin actions.
- Relational schema, migrations, indexed search fields, data constraints, and transactions where needed.
- Business logic separate from UI; validate form/API inputs on server.
- Accessible design: semantic HTML, labels, keyboard navigation, focus states, contrast, error messages.
- Mobile-first responsive UI, performant images, meaningful loading and empty states.
- Tests for access controls, listing CRUD, inquiry transitions, and moderation.
- Deployment, environment documentation, seeded **demo-only** data, and reproducible setup.
- A portfolio-facing README that explains architecture, user problem, major decisions, accessibility, tests, and trade-offs.

---

## 10. Conceptual Data Model

Propose a normalized schema rather than simply implementing these names verbatim.

- **User:** credentials/auth identity, display name, optional avatar, bio, preferences.
- **Neighborhood:** name, region, membership policy, active state; one launch neighborhood, expandable later.
- **Membership:** user, neighborhood, role (`member`, `admin`), status (`pending`, `approved`, `rejected`, `revoked`), review metadata. Consider separation of role/status.
- **ProviderProfile:** one Approved Member and neighborhood; member-name display configuration; optional photo and biography; visible to other Approved Members only while at least one Service Listing is published.
- **ServiceCategory:** category name, slug, active/approved status.
- **Service:** provider, neighborhood, title, description, category, price type and amount (where relevant), publication status, availability status, timestamps.
- **ServiceImage:** service, object key, alt text, sort order.
- **Inquiry:** customer, provider, service, neighborhood, status, timestamps, optional preferred date.
- **InquiryMessage:** inquiry, author, message, timestamp; access limited to participants/admin under documented policy.
- **Report / ModerationAction:** reporter, target, reason, outcome, reviewer, timestamps.
- **AuditEvent:** membership/moderation/security-sensitive changes.

### Key invariants

- Membership must be approved in the neighborhood for discovery or contact.
- Listing owners and buyers must belong to the permitted neighborhood.
- Provider must not mutate someone else's listings; inquiry participants must not see unrelated threads.
- All admin mutations require admin role checked server-side.
- Price may be fixed, starting-at, hourly, or quote-based. Avoid misleading comparisons across pricing types.
- Every Service Listing identifies one Service Provider, and that member personally performs the listed service.
- Provider Profiles and Service Listings cannot advertise a business, team, employee, or other worker.

---

## 11. Launch Strategy and Measurement

### Intended rollout (targets, not predictions)

1. **Discovery:** Speak with potential providers/buyers. Already done informally; keep tracking specific objections, desired categories, and willingness to list.
2. **Alpha:** 5–8 residents test sign-up, listing, and inquiry flows.
3. **Seed genuine supply:** Recruit approximately 10–15 providers to publish real, opt-in listings. The user may offer web/app development, music mixing/mastering, and car washing as legitimate initial services.
4. **Neighborhood beta:** Invite the first 25–50 approved members, potentially via existing Facebook/community channels with admin permission.
5. **Iterate:** Fix friction and measure whether people actually contact providers.

### Success measures

- Approved neighborhood members.
- Number of active real provider profiles and published services.
- Search-to-service-detail conversion / discovery usage.
- Genuine inquiries submitted.
- Provider response rate and response latency.
- Repeat use and qualitative feedback.

**North star for early validation:** a genuine inquiry between neighbors, not merely signups or pageviews.

**Cold-start mitigation:** recruit providers before launch; keep a separate, clearly labeled recruiter demo with fictional data. Never inflate production stats or invent recommendations.

---

## 12. User's Preferred Design-to-Development Workflow

Follow this order unless there is a documented reason to change it:

1. Client/product brief.
2. Establish brand, audience, business goals, product goals, and constraints.
3. Define site/application structure and information architecture.
4. Design **three distinct homepage / entry-screen directions** using selected reference sites.
5. Choose one visual direction.
6. Make detailed changes to the chosen primary screen.
7. Create reusable section patterns and design tokens.
8. Design the mobile version.
9. Create mobile component/section patterns and tokens.
10. Design remaining screens desktop and mobile.
11. Define backend and content/data requirements (this is an application with a database, not automatically a Sanity CMS project).
12. Implement page/feature by page/feature with an agent and Figma integration where useful.

Implementation should be conducted in small, reviewable vertical slices. Example: auth + membership gate, then provider creation + listing CRUD, then directory + filtering, then inquiry flow, then administration. For each slice: approved mini-spec, tests, implementation, QA, commit, and PR when using branches.

The user likes **minimal, refined design**, good typography, reusable components, and production-quality execution. Do not infer that every site must use Astro or Sanity: this project is specifically intended to deepen full-stack React/Next.js experience.

---

## 13. Open Questions / Decisions for Product Specification

Codex should present concrete recommendations (and ask only if essential):

1. **Product name and identity.** Working title is generic; don't assume `NeighborMade` is available or suitable (a related term has appeared in competitor positioning). Check naming/trademark/domain conflicts before final branding if authorized to research.
2. **How is residency validated?** Admin approval, community invitation, optional reference to HOA or Facebook group; define minimum evidence without collecting intrusive personal documents.
3. **Listing approval policy.** Review all new listings before publication or publish then moderate? Choose based on community size, safety, and admin workload.
4. **Inquiry communication model.** Structured inquiry + provider reply versus lightweight threaded messaging; decide minimal safe implementation and notifications.
5. **Provider pricing model.** Quote only vs fixed / hourly / from price; keep search and sort behavior understandable.
6. **Approved and prohibited categories.** Start with low-risk services, with guidelines for services requiring licenses or involving vulnerable people.
7. **Contact privacy / reporting.** What data is visible, what actions can be reported, and how moderators are notified.
8. **Seeding demo.** How to keep realistic demo accounts, posts, and inquiries isolated from production and safe to showcase.
9. **Brand and launch language.** Make clear that every Service Provider offers their own work and that neighborhood membership does not imply vetting.
10. **Potential terms/policies.** Determine what needs legal review before inviting real residents. Avoid presenting product design as legal advice.

---

## 14. Competitive Context (Background, Not Validated Market Research)

Comparable categories discussed:

- **Nextdoor:** broad neighborhood community and business/service discovery.
- **Thumbtack / Taskrabbit:** public service marketplaces, not neighborhood-member-only by default.
- **Smaller neighbor-skills platforms** surfaced during exploratory discussion, including Neighbora, hômis, KnackCity, Neighbor Knowledge, and Quellr Hub. **Their current operations, exact features, user counts, and market position have not been independently revalidated in this handoff.** Codex must verify before relying on them in a competitor report.

Strategic product positioning: **not a Nextdoor clone**. Emphasize a focused, private directory where real residents offer services, skills, and talents that they personally perform, with persistent Provider Profiles and simple contact/inquiry flows.

---

## 15. Immediate Deliverables for Codex

Create the following planning documents in a `/docs` or `/planning` directory (suggest file names; adapt to existing repo conventions):

1. `product-brief.md` — audience, problem, outcome, positioning, evidence vs assumptions.
2. `mvp-prd.md` — functional requirements, nonfunctional requirements, explicit exclusions, acceptance criteria.
3. `information-architecture.md` — route map, navigation, permissions, content per screen.
4. `user-flows.md` — join, provider onboarding, add service, search/inquire, moderation; include edge cases and empty states.
5. `technical-architecture.md` — recommended stack, auth/authorization, tenancy, deployment, file uploads, email, performance, observability.
6. `data-model.md` — ERD/schema proposal, relationships, constraints, indexes, tenancy and privacy boundary.
7. `security-and-trust.md` — threat model, role permissions, moderation, retention, policies to resolve.
8. `implementation-plan.md` — vertical slices with tests and completion criteria.
9. `open-decisions.md` — decisions requiring approval, alternatives, and recommended defaults.

**Do not generate boilerplate files purely for appearance.** Use clear, practical specs with enough detail to implement and test. Present a concise decision summary to the user before beginning app code.

---

## 16. Ready-to-Paste First Message to Codex

> We're starting a new full-stack product called **Neighborhood Skills Marketplace** (working title). Please read `neighborhood-skills-marketplace-codex-handoff.md` completely and use it as the source of truth for product discovery. This will be a private, resident-approved neighborhood directory where neighbors offer paid services, skills, and talents that they personally perform and other Approved Members can contact them. Cirvice does not support business profiles, business advertising, teams, or services performed by other people. The first launch serves a real neighborhood of about 3,000 residents, with early positive qualitative feedback. The purpose is both a usable community product and a production-quality full-stack portfolio case study. **Do not scaffold or implement yet.** Start by reviewing requirements, separating confirmed decisions from recommendations, identifying security/scope risks, and proposing the planning documents and key decisions listed in Section 15. Favor a small Next.js/TypeScript/PostgreSQL MVP and our established design-first workflow. When you have a proposed plan, provide a concise summary of the decisions you need me to approve.

---

*End of handoff.*
