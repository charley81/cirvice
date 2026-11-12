# Membership verification options for Cirvice

**Research date:** 2026-11-12  
**Scope:** A first launch serving roughly 3,000 residents in a private neighborhood services platform.  
**Source policy:** Current first-party product pages and primary security/identity guidance only.

## Executive conclusion

A shared access code posted inside an already-verified private Facebook neighborhood group is **suitable as a time-limited launch bootstrap**, but it is not strong or durable membership verification on its own. It proves possession of a bearer secret, not residency. Its assurance is inherited from the Facebook group's admission process, and any member can copy the code to an outsider. Meta says private-group posts and membership lists are visible to current members and join requests normally require approval, but this does not prevent a member from manually disclosing a code. [Meta: differences between public and private groups](https://www.facebook.com/help/220336891328465)

For Cirvice's first launch, the best balance is a **hybrid**:

1. Use one expiring Facebook-group launch code to seed adoption.
2. Verify control of each account's email address.
3. Give verified members a small number of attributable, single-use invite links.
4. Offer a lightweight manual path for residents who are not on Facebook or do not know a member.
5. Rotate off the shared code after the launch window and make unique invites plus manual exceptions the normal path.
6. Add postcard verification only as an escalation if actual abuse justifies collecting a full address.

Do not collect identity documents. Do not make full residential addresses a default requirement. Cirvice needs reasonable evidence of **current neighborhood membership**, not government-grade proof of legal identity.

## What is being verified

These are different claims and should not be conflated:

- **Account contactability:** the applicant controls an email address or phone number.
- **Neighborhood membership:** the applicant currently lives in, owns property in, or otherwise meets Cirvice's stated eligibility rule for the neighborhood.
- **Legal identity:** the applicant is a particular real-world person.
- **Trustworthiness or professional qualification:** the applicant is safe, licensed, insured, or competent to provide a service.

The launch process should verify the first two only. Email confirmation does not prove residency. A neighborhood invite does not prove legal identity. Neither is a background check or endorsement.

NIST's identity-proofing guidance is stricter than Cirvice needs, but two design principles are directly useful: offer multiple paths for people with different means and technologies, including exception handling, and minimize personal data to what is necessary. [NIST SP 800-63A, multiple proofing options](https://pages.nist.gov/800-63-4/sp800-63a.html) and [NIST SP 800-63A, collection and data minimization](https://pages.nist.gov/800-63-4/sp800-63a/privacy/#collection-and-data-minimization)

## Is a Facebook-group access code suitable?

### Yes, for a controlled launch

It is practical when all of the following are true:

- The group's admins already apply a meaningful and current neighborhood-membership check.
- The group is private, and the code is posted only to current members.
- Cirvice accepts that the method provides moderate, not high, assurance.
- The code expires or is rotated after the launch cohort.
- Residents outside Facebook have an equally visible alternative.
- Cirvice can suspend individual accounts independently of rotating the code.

Meta's current Help Center states that only current members can see content and membership in a private group, and that private-group join requests require approval unless limited membership is enabled. It also says a private group can be visible or hidden. These controls make the group a reasonable distribution channel, but they do not turn a shared code into individual evidence. [Meta Help Center](https://www.facebook.com/help/220336891328465)

### Why it should not be the permanent model

- **Code sharing:** every member receives the same reusable bearer credential. A screenshot, direct message, copied text, or compromised Facebook account can disclose it.
- **No attribution:** Cirvice cannot determine which member disclosed a shared code.
- **Coarse revocation:** rotating the code invalidates it for every legitimate person who has not yet joined. Rotation does not remove accounts already created with the old code.
- **Stale upstream membership:** people may remain in the Facebook group after moving away. Cirvice inherits the group's offboarding weaknesses as well as its onboarding strengths.
- **Facebook exclusion:** residents without Facebook accounts, residents who avoid Meta for privacy reasons, and residents who have not joined the group are blocked unless Cirvice provides another path.
- **Assurance ceiling:** possession of the code only shows that the applicant obtained it somehow. It does not directly prove where they live.

### Controls if Cirvice uses it

- Generate an unguessable code; do not use a neighborhood name, postcode, or memorable phrase.
- Rate-limit attempts and monitor unusual signup bursts.
- Give the code a short launch window, such as 2–4 weeks, then rotate or disable it.
- Tag accounts with the code version/cohort used so incidents can be investigated without retaining Facebook data.
- Require a verified email before activation.
- Do not require Facebook OAuth and do not collect Facebook profile or group-membership data.
- Post the non-Facebook route beside the code wherever the launch is announced.
- Make clear that the code is for eligible residents and must not be reposted.

Entropy prevents guessing, not deliberate sharing. The expiration and monitoring controls therefore matter as much as code length.

## Exactly what Neighbora publicly documents

### Documented workflow

Neighbora's public pages currently state the following:

1. It describes itself as private to a building and limited to verified or approved residents. [Neighbora home page](https://neighbora.app/) and [Neighbora for buildings](https://neighbora.app/buildings)
2. Its resident flow says: **“Enter your building's code and verify your address.”** The same page separately says residents may add identity verification later, indicating that its basic resident-access claim and identity verification are distinct concepts. [Neighbora home page](https://neighbora.app/)
3. The public join page asks for a **community code** from a community flyer or invitation. Residents without one are told to ask the building's front office. [Neighbora join page](https://neighbora.app/join)
4. Its building-launch page says Neighbora prepares a building code, QR links, and welcome-packet language, while the property team distributes them through existing channels such as resident email, the front desk, elevators, or move-in flows. [Neighbora for buildings](https://neighbora.app/buildings)
5. The invalid-code UI says codes can come from a building's property team or a neighbor's invite. [Neighbora invalid-code page](https://neighbora.app/join/INVALIDTESTCODE)
6. Account signup offers Google, Facebook, Apple, or email authentication. The email flow sends an email verification link. This establishes account authentication/contact control, not building membership. [Neighbora signup](https://neighbora.app/signup) and [Neighbora login](https://neighbora.app/login)
7. Its privacy policy says it collects information including name and email, with phone optional for SMS. It also describes automatically collected IP address and general location as city-level rather than apartment number. [Neighbora privacy policy](https://neighbora.app/privacy)

### Not publicly documented

Neighbora's official public pages do **not** state:

- What “verify your address” technically requires.
- Whether a resident enters a full street address, unit number, or only selects a building.
- Whether the entered information is checked against a property-management roster, lease system, postal record, email domain, geolocation, human review, or another source.
- Whether the building/community code is shared, unique, one-time, expiring, rate-limited, or revocable.
- Whether a neighbor's invite is individually attributable or capped.
- Whether an address is retained after verification and, if so, for how long.
- How moved-out residents are detected or removed.
- What happens when the code is shared outside the building.

Accordingly, the most exact supportable description is: **Neighbora publicly says that a resident enters a building/community code and verifies their address, with launch codes and links distributed through a property team or invitations; it does not publicly explain the address-verification mechanism.** Anything more specific would be inference.

### Public inconsistency that remains unresolved

Neighbora's marketing repeatedly says “verified residents” or “approved residents,” while its Terms of Service says, more broadly, **“we don't screen or verify users or their listings.”** The terms also say Neighbora does not verify professional licensing or insurance. The public pages do not reconcile whether “verified residents” means only access to a building-distributed code, a separate address check, or something else. Cirvice should not assume a stronger process without direct confirmation from Neighbora. [Neighbora terms](https://neighbora.app/terms), [home page](https://neighbora.app/), and [for buildings](https://neighbora.app/buildings)

## Comparison of practical options

Ratings below concern neighborhood-membership assurance, not legal identity.

| Option | Security / membership assurance | Privacy | Admin workload at ~3,000 residents | Code sharing / abuse | Revocation | Accessibility |
|---|---|---|---|---|---|---|
| **Shared code in verified private Facebook group** | Low–medium; inherits the group's admission quality but only proves code possession | Low additional data for Cirvice; creates dependence on Meta | Low | High; easy to copy and unattributable | Poor for unused access: rotate for everyone. Existing accounts still require individual suspension | Poor alone; excludes non-Facebook residents and non-members of the group |
| **Unique invite links** | Medium when random, single-use, short-lived, and issuer-linked | Low; no address or document needed | Low after implementation; some support for expired or misdirected links | Medium–low; still transferable before redemption, but leakage is attributable and bounded | Good for unused links; revoke one token or issuer. Accounts remain separately revocable | Good if links can be delivered by email, SMS, print/QR, or in person |
| **Existing-member sponsorship** | Medium; adds accountable social evidence but is vulnerable to collusion, careless sponsors, and stale members | Low PII, but the sponsor relationship forms a sensitive social graph | Low centrally; moderate fraud/support review | Lower than a global code if each sponsorship creates one invite | Good traceability; suspend sponsor and review sponsored accounts after abuse | Generally good, but disadvantages new or socially isolated residents |
| **Manual admin review** | Medium–high if admins use a reliable external source or personal knowledge; highly variable otherwise | Variable. Can be low if the admin returns only yes/no; high if Cirvice stores documents | High. As a planning example, reviewing just 5% of 3,000 applicants is 150 cases; at 3 minutes each that is 7.5 staff hours, excluding follow-up | No reusable code, but social engineering and inconsistent decisions are risks | Good at account level | Good when offered through email/phone/in-person channels; bias, language, disability, and schedule barriers need attention |
| **Address + mailed postcard code** | Medium–high proof of access to mail at an address; does not prove identity, sole occupancy, or continuing residency | Highest among these options because a full address must be processed | Medium–high operational burden, cost, delivery delay, returned mail, and support | Lower-scalability attack; household members or intercepted mail can still share a code | Good for the unused code; poor for detecting later moves without re-checking | Works without Facebook or smartphones, but is slow and weak for temporary residents, people without reliable mail, and urgent onboarding |
| **Email-domain check** | High only if the domain owner issues and promptly removes individual accounts based on current residency; otherwise low or irrelevant | Low–medium; exposes affiliation and email | Low with an allowlist; integration/sync raises it | Account sharing and stale mailboxes remain possible | Good only with timely domain lifecycle or periodic re-checks | Poor for ordinary neighborhoods where residents use personal email; useful in some universities, employers, managed buildings, or institutions |
| **Hybrid** | Medium–high because weaknesses are bounded and exception paths exist | Can remain low if it avoids documents and addresses by default | Medium; automation handles most applicants, admins handle exceptions | Better containment through expiring cohorts, attributable invites, and monitoring | Good if token revocation and account suspension are separate | Best; residents can use different channels |

## Option details

### Unique invite links

Unique links are a direct improvement over a global code because Cirvice can bind each token to an issuer, limit it to one redemption, expire it, and revoke it without disrupting everyone else. They do not need to contain the recipient's name or email.

Implement them as opaque random tokens, store only a hash, set an expiry, invalidate after use, rate-limit validation, and record issuer and redemption time. OWASP's primary token guidance recommends cryptographically random, sufficiently long, single-use, expiring tokens and rate limiting; although written for password reset, those properties apply directly to bearer invitation links. [OWASP Forgot Password Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html)

An invite proves that a verified account vouched for whoever redeemed it. It does not prove the recipient is the intended person, so Cirvice should cap invites and preserve an exception-review path.

### Existing-member sponsorship

Sponsorship converts social knowledge into attributable evidence: “verified member A vouches that applicant B is eligible.” NIST calls the analogous role an “applicant reference” and recommends clear policies, risk assessment, and recording who vouched for whom. Cirvice is not claiming NIST identity-assurance compliance, but the accountability pattern is useful. [NIST SP 800-63A, applicant references](https://pages.nist.gov/800-63-4/sp800-63a/ial-general/#ARs)

Recommended controls:

- Sponsors must be verified, unflagged, and established for a minimum period.
- Limit outstanding and lifetime sponsorships, with higher limits for trusted launch admins.
- Tell sponsors exactly what they are vouching for: current neighborhood eligibility, not character or service quality.
- Record the sponsor relationship and review a sponsor's invitees after confirmed abuse.
- Do not display the sponsorship graph to other residents.

### Manual admin review

Manual review is the best exception path, not the best default. Prefer an administrator who can check an existing source without copying it into Cirvice—for example, a neighborhood-group admin, property manager, association officer, or other designated verifier returns a yes/no decision.

Collect the minimum needed to route the case. Avoid uploads of leases, utility bills, IDs, or bank/credit statements. Store the decision, verifier, date, and a coarse reason code rather than evidence copies. Publish eligibility criteria and an appeal route to reduce inconsistent or biased decisions.

### Address and postcard verification

A mailed one-time code demonstrates access to mail delivered at an address. NIST explicitly describes postal confirmation codes as proof that an applicant can receive a code at a postal address, requires random codes, expiration, and invalidation after use, and allows up to 21 days for delivery within the contiguous United States. That is useful assurance, but it is not the same as proving identity or ongoing residency. [NIST SP 800-63A, confirmation codes](https://pages.nist.gov/800-63-4/sp800-63a/ial-general/#ConfirmCodes)

Use this only if observed abuse or a partner's risk requirement justifies the privacy and operational cost. If introduced:

- Explain why the full address is needed and how long it is retained.
- Use it only to address the mailer and confirm neighborhood boundaries.
- Delete the plaintext full address promptly after successful verification or expiry unless a documented need requires retention.
- Retain only neighborhood ID, verification method/date, and status. If duplicate-address control is necessary, prefer a keyed digest of a normalized address with tightly controlled keys over retaining plaintext.
- Never use address knowledge questions as a substitute for delivery of a code.
- Provide a manual alternative for people without reliable mail.

### Email-domain checks

A verified email proves control of that mailbox. A domain suffix proves affiliation only when the domain's issuer maintains a direct, current mapping between mailbox eligibility and residency. That is uncommon for a normal neighborhood.

Use domain checks only for a clearly bounded partner population—such as a managed residential institution that issues every current resident an account and promptly deprovisions movers. Do not treat generic employer, school, council, ISP, or personal email domains as neighborhood evidence. Always retain another path for household members who do not receive the institutional account.

## Recommended staged model

### Stage 0: Define eligibility and minimum data

Before launch, publish one sentence defining who qualifies—for example, current adult residents within a named boundary, with any explicit rules for property owners, carers, or staff.

Store only:

- account ID;
- verified email;
- display name;
- neighborhood ID, not full address;
- verification method;
- shared-code cohort or invite/sponsor identifier;
- verifier and coarse decision reason for manual cases;
- verified-at, review-at, and status timestamps.

Do not collect identity documents, date of birth, government identifiers, Facebook profile data, or a full residential address.

### Stage 1: Launch window

For the first 2–4 weeks:

1. Post one unguessable, expiring launch code in the already-verified private Facebook group.
2. Require email verification before the account becomes active.
3. Provide a prominent **“Not on Facebook?”** route handled by designated neighborhood admins using an existing roster or personal knowledge, returning only a yes/no decision to Cirvice.
4. Give a small set of trusted seed members individually attributable, single-use invite links for residents outside the Facebook group.
5. Rate-limit code attempts and alert on abnormal redemption velocity or concentrated device/network patterns. Retain raw fraud telemetry only briefly under a documented retention period.
6. Keep account suspension separate from invitation-code rotation.

This gets the community moving without turning address or document collection into a condition of entry.

### Stage 2: Move away from the global code

At the end of the launch window:

- Disable or rotate the launch code.
- Make verified-member sponsorship through single-use links the normal route.
- Give ordinary members a conservative invite allowance; raise limits only after trustworthy use.
- Keep manual admin review as the universal fallback.
- Review accounts tied to a leaked invite rather than disrupting unrelated members.
- Add in-product reporting for suspected non-residents and an accountable suspension/appeal process.

### Stage 3: Maintain current membership

Initial verification decays when residents move. Add lightweight lifecycle controls:

- Annual eligibility re-attestation by default.
- Earlier review after credible reports, repeated abuse, or a sponsor's confirmed misuse.
- Immediate self-service “I moved” account closure or neighborhood transfer.
- Partner-admin offboarding only when a reliable partner roster exists.
- Reconfirm dormant accounts before restoring access after a long absence.

Do not require annual address documents merely to solve a problem that may be handled by re-attestation, reports, and targeted review.

### Stage 4: Escalate only if evidence supports it

Track, without excessive personal data:

- confirmed outsider accounts per 1,000 signups;
- invite/code leakage incidents;
- manual-review rate and turnaround time;
- false rejection and appeal rate;
- percentage joining through non-Facebook paths;
- moved-resident reports;
- abuse concentration by verification method.

Only if those measures show meaningful infiltration should Cirvice pilot mailed address codes for disputed/high-risk cases or for a particular neighborhood partner. Identity-document collection is not justified for this use case unless Cirvice later introduces a separate, genuinely high-risk regulated function.

## Final recommendation

Use the private Facebook group as a **bootstrap trust channel**, not as Cirvice's permanent membership authority. Pair its short-lived shared code with verified email, attributable one-time invites, and a manual non-Facebook path from day one. Retire the global code after launch, maintain revocable sponsorship records, and review membership periodically. Keep postcard verification as an exception and avoid identity documents and stored full addresses unless measured abuse demonstrates that the extra assurance is worth the privacy, access, and operating costs.

## Primary sources

- [Meta Help Center — Differences between public and private Facebook groups](https://www.facebook.com/help/220336891328465)
- [Neighbora — Home](https://neighbora.app/)
- [Neighbora — Join](https://neighbora.app/join)
- [Neighbora — For buildings](https://neighbora.app/buildings)
- [Neighbora — Signup](https://neighbora.app/signup)
- [Neighbora — Login](https://neighbora.app/login)
- [Neighbora — Privacy policy](https://neighbora.app/privacy)
- [Neighbora — Terms of service](https://neighbora.app/terms)
- [NIST SP 800-63A — Identity Proofing and Enrollment](https://pages.nist.gov/800-63-4/sp800-63a.html)
- [NIST SP 800-63A — Confirmation codes](https://pages.nist.gov/800-63-4/sp800-63a/ial-general/#ConfirmCodes)
- [NIST SP 800-63A — Applicant references](https://pages.nist.gov/800-63-4/sp800-63a/ial-general/#ARs)
- [NIST SP 800-63A — Collection and data minimization](https://pages.nist.gov/800-63-4/sp800-63a/privacy/#collection-and-data-minimization)
- [OWASP Cheat Sheet Series — Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html)
