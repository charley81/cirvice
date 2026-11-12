# South Carolina–North Carolina launch legal and compliance issue spotter

**Research ticket:** [#4 — Identify launch legal and compliance questions for South Carolina and North Carolina](https://github.com/charley81/cirvice/issues/4)  
**Planning map:** [#1 — Plan Cirvice for a production-ready first-neighborhood launch](https://github.com/charley81/cirvice/issues/1)  
**Current through:** November 12, 2026  
**Scope:** United States federal law, South Carolina, and North Carolina. Primary sources only.

> **Not legal advice.** This is issue spotting for product and launch planning. It does not determine how a court or regulator would classify Cirvice, resolve a dispute, or apply a law to particular facts. Cirvice should obtain advice from qualified South Carolina and North Carolina counsel before launch, and from a tax professional and licensed insurance broker where noted.

## Product assumptions that control this analysis

This analysis assumes the launch described in the planning map:

- a private, mobile-first web marketplace for approved neighborhood residents age 18 or older;
- one member account and, optionally, one provider profile per person;
- service listings, structured inquiries, private asynchronous messages, and email notifications;
- administrator approval before a listing is published;
- providers and customers negotiate, contract, perform, and pay each other off-platform;
- no booking, payment processing, escrow, commissions, subscriptions, listing fees, advertising, ratings, reviews, recommendation badges, public contact details, or background checks;
- optional provider business information and disclosure when a team or nonresident worker may perform the service; and
- no default collection of identity documents or full home addresses.

A change to any of these facts can change the legal analysis. The highest-impact triggers are listed at the end.

## How to read the findings

- **Requirement** — a legal duty likely to apply if the stated facts are true.
- **Risk/control** — a product or operational control that reduces a material legal risk, but is not necessarily mandated in that exact form.
- **Counsel question** — a fact-dependent classification, drafting, or state-law issue that should not be settled without a qualified attorney.

## Executive launch findings

1. **The marketplace label does not determine Cirvice's status.** Actual conduct—especially pricing, assigning work, controlling performance, handling money, or making provider-quality promises—will matter more than terms saying Cirvice is “only a platform.” Federal wage-and-hour rules use a fact-intensive economic-reality analysis, and federal tax classification turns on the right to control work. ([29 C.F.R. pt. 795](https://www.ecfr.gov/current/title-29/subtitle-B/chapter-V/subchapter-B/part-795); [IRS, Independent contractor defined](https://www.irs.gov/businesses/small-businesses-self-employed/independent-contractor-defined))
2. **Truthful scope language is a launch requirement.** “Resident approved,” “listing approved,” “license checked,” “insured,” “background checked,” “safe,” and “recommended” are materially different claims. False or misleading platform statements can create federal and state consumer-protection exposure. ([15 U.S.C. § 45](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap2-subchapI-sec45.htm); [S.C. Code §§ 39-5-20, 39-5-140](https://www.scstatehouse.gov/code/t39c005); [N.C. Gen. Stat. §§ 75-1.1, 75-16](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-1.1.html))
3. **“Broad lawful services” needs a state-by-state credential gate.** SC and NC regulate many service categories differently, including construction, electrical, plumbing/HVAC, locksmithing, child care, health-related services, transportation, food, pest control, and professional services. A disclaimer does not make an unlawful listing lawful.
4. **Privacy duties are material under the applicable federal and state framework.** FTC deception/unfairness authority, state breach laws, state secure-disposal laws, contract promises, and communications law all matter. Cirvice needs a data inventory, accurate privacy notice, security program, vendor controls, incident plan, and retention schedule before real residents join.
5. **User content and private messaging create separate legal workstreams.** Section 230 may protect Cirvice from some claims based on third-party content, but it has express exceptions and does not protect Cirvice's own promises or conduct. Copyright, nonconsensual intimate imagery, child sexual exploitation reports, and stored-message disclosure require specific procedures.
6. **Accessibility should be treated as a launch control while counsel resolves legal classification.** DOJ states that Title III applies to web offerings of businesses open to the public; NC and SC also protect access to public accommodations. Whether a private neighborhood service qualifies, and whether any exemption applies, requires counsel, but a login wall should not be treated as an accessibility strategy.
7. **Cross-state operation must be reviewed as two launches.** Entity qualification, provider licensing, consumer law, breach notice, local permits, tax treatment, and insurance can turn on the state of the resident, operator, or service performance. A single choice-of-law clause does not erase nonwaivable law.

## 1. Platform status, worker classification, and marketplace boundaries

### Likely requirements and controls

- **Risk/control — preserve a true referral/listing model.** Providers should choose whether to offer services, describe their own lawful services, set or negotiate their own prices, decide how and when to work, provide their own tools, and contract directly with customers. Cirvice should not assign jobs, require acceptance, set compensation, supervise methods, evaluate work as an employer would, or discipline providers for declining work. These facts are relevant to federal employee/contractor analysis. ([29 C.F.R. §§ 795.105–795.110](https://www.ecfr.gov/current/title-29/subtitle-B/chapter-V/subchapter-B/part-795); [IRS guidance](https://www.irs.gov/businesses/small-businesses-self-employed/independent-contractor-defined))
- **Risk/control — state the parties accurately.** Product copy and terms should say that the provider and customer, not Cirvice, decide whether to contract and are responsible for scope, price, performance, permits, taxes, and payment. Do not state that this language overrides a legal classification.
- **Risk/control — avoid acting as the contractor or seller.** Cirvice should not quote a bundled job, promise completion, collect the contract price, subcontract the work, warrant the result, or present a provider as acting “for Cirvice” without counsel reviewing contractor, agency, employment, and seller status.
- **Current tax boundary.** Under the current design, SC's marketplace-facilitator definition requires both listing/advertising tangible personal property and collecting or processing payment; NC's definition requires making items available and collecting or enabling payment. A services-only platform that does not process payment appears outside those definitions, but adding goods or payments requires a new state tax review. ([S.C. Code § 12-36-71](https://www.scstatehouse.gov/code/t12c036); [N.C. Gen. Stat. §§ 105-164.3(133), 105-164.4J](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_105/GS_105-164.3.html))

### Counsel questions

- Could Cirvice be treated as an employer, joint employer, employment agency, agent, broker, general contractor, or other regulated intermediary based on listing approval, messaging, later monetization, or operational control?
- Which provider restrictions are legitimate marketplace safety rules, and which could become evidence of control over how services are performed?
- Should terms expressly prohibit providers from claiming to be Cirvice employees, agents, franchises, endorsed providers, or authorized representatives?
- Do any SC or NC industry-specific referral, lead-generation, contractor, health-care, child-care, transportation, or professional rules apply to a proposed launch category even when Cirvice takes no payment?

## 2. Consumer protection, advertising, and platform claims

### Requirements

- **Federal:** Section 5 of the FTC Act prohibits unfair or deceptive acts or practices in or affecting commerce. Platform statements about approval, verification, safety, credentials, insurance, background checks, availability, privacy, or moderation must match actual practice. ([15 U.S.C. § 45](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap2-subchapI-sec45.htm))
- **South Carolina:** Unfair or deceptive acts in trade or commerce are unlawful. The statute authorizes public enforcement and a private action for an ascertainable loss, with treble damages for a willful or knowing violation and attorney's fees for a successful plaintiff. ([S.C. Code §§ 39-5-20, 39-5-50, 39-5-140](https://www.scstatehouse.gov/code/t39c005))
- **North Carolina:** Unfair or deceptive acts in or affecting commerce are unlawful; an injured person may recover treble damages, with attorney's fees available in specified circumstances. ([N.C. Gen. Stat. §§ 75-1.1, 75-16, 75-16.1](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-1.1.html))

### Launch controls

- Use separate, precisely defined labels:
  - **“Residence eligibility approved”** means only that Cirvice applied its neighborhood-access process.
  - **“Listing approved”** means only that an administrator allowed publication under community rules.
  - **“License checked”** should appear only for a named license type, issuing authority, license number or lookup result, jurisdiction, and check date.
  - **“Insured”** should appear only if Cirvice defines what evidence it reviewed, for what policy type and period, and how expiration is handled.
- Do not use “vetted,” “verified provider,” “trusted,” “safe,” “qualified,” “recommended,” “guaranteed,” “licensed,” “bonded,” “insured,” or “background checked” as broad badges unless counsel approves the exact substantiation and ongoing verification process.
- Require providers to warrant that their listing is truthful, that they hold every license/permit required where the work is performed, and that team/nonresident-worker disclosures are accurate. Preserve the submitted claim and later edits.
- Give customers a clear safety notice: Cirvice is not a substitute for checking scope, price, contracts, references, licenses, insurance, permits, and suitability. This notice must not contradict actual platform conduct.
- Build a correction/reporting path for false credentials, impersonation, fraud, unsafe services, and misleading business-team claims. Apply the published policy consistently.

### Provider/customer contract risk

Some contracts formed after personal solicitation at a residence—particularly consumer-credit sales—carry cancellation and form requirements. SC and NC statutes provide three-business-day cancellation rights for covered home-solicitation sales. Providers, rather than Cirvice, should form their service contracts, but counsel should decide whether the platform's inquiry flow or scripts could make Cirvice a seller or seller's agent. ([S.C. Code §§ 37-2-501–37-2-503](https://www.scstatehouse.gov/code/t37c002); [N.C. Gen. Stat. §§ 25A-38–25A-40](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_25A/GS_25A-38.html))

## 3. Privacy, security, and breach response

### Federal requirements and risk

- An inaccurate privacy or security promise can be deceptive under FTC Act § 5, and unreasonable security practices can create unfairness risk. The FTC's business guidance emphasizes collecting only needed data, limiting access, securely storing and transmitting sensitive information, requiring service-provider safeguards, and securely disposing of data. ([15 U.S.C. § 45](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap2-subchapI-sec45.htm); [FTC, Start with Security](https://www.ftc.gov/business-guidance/resources/start-security-guide-business))
- COPPA applies to covered online services directed to children under 13 or with actual knowledge they collect personal information from a child under 13. Cirvice's 18+ rule reduces but does not eliminate the need for an underage-account process. ([15 U.S.C. §§ 6501–6506](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap91.htm); [16 C.F.R. pt. 312](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-312))

### South Carolina requirements

- A person conducting business in SC that owns or licenses covered personal identifying information must notify affected SC residents after a qualifying breach **in the most expedient time possible and without unreasonable delay**, subject to law-enforcement and investigation/restoration needs. A processor or maintainer must notify the owner or licensee immediately after discovery. If notice goes to more than 1,000 people at once, the business must notify the SC Department of Consumer Affairs' Consumer Protection Division and nationwide consumer reporting agencies. ([S.C. Code § 39-1-90](https://www.scstatehouse.gov/code/t39c001))
- When a business disposes of a customer business record containing personal identifying information, it must make the information unreadable or undecipherable, directly or through a disposal contractor. ([S.C. Code § 37-20-190](https://www.scstatehouse.gov/code/t37c020))

### North Carolina requirements

- A business owning or licensing covered personal information must notify affected NC residents after a qualifying breach **without unreasonable delay**, subject to documented law-enforcement delay and investigation/restoration needs. A maintainer must notify the owner or licensee immediately after discovery. Whenever notice is provided to an affected person, the business must also notify the NC Attorney General's Consumer Protection Division without unreasonable delay; notice to more than 1,000 people also triggers notice to nationwide consumer reporting agencies. ([N.C. Gen. Stat. § 75-65](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-65.html))
- A business conducting business in NC or holding an NC resident's personal information must take reasonable measures to prevent unauthorized access to or use of that information during and after disposal, including written disposal policies and destruction or erasure that prevents practical reconstruction. ([N.C. Gen. Stat. § 75-64](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-64.html))
- NC also restricts specified public disclosure and handling of Social Security numbers. Cirvice should not collect SSNs for the launch model. ([N.C. Gen. Stat. §§ 75-62, 75-66](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-62.html))

### Launch controls

- Create a data inventory covering account data, residency evidence, invitation attribution, manual-review notes, provider claims, listing history, private messages, email events, moderation reports, logs, support records, and vendors.
- Collect the minimum data needed. Prefer an 18+ attestation over a full birth date unless counsel identifies a reason to collect date of birth. Do not collect identity documents, SSNs, financial data, or full addresses by default.
- Publish an accurate privacy notice describing data categories, purposes, disclosures, vendors, security limitations, retention approach, account closure, and contact method. Do not promise absolute security or deletion that backups and legal holds cannot support.
- Use role-based administrator access, multifactor authentication for administrators, encryption in transit and at rest, secrets management, tested backups, logging, dependency patching, vendor due diligence, and a written incident-response plan.
- Put security, confidentiality, use limitation, deletion/return, incident notice, subprocessors, and cooperation terms in vendor contracts.
- Build one incident workflow that identifies affected residents by state, assesses both statutory definitions, preserves evidence, records the decision, and supports SC/NC agency notices. Do not assume an incident is harmless merely because email/password data falls outside a narrow state statutory definition; FTC, contract, and other duties may still matter.

### Counsel questions

- What exact facts trigger notice under each state's acquisition, harm, encryption, and information-definition tests?
- What resident, regulator, consumer-reporting-agency, and vendor notice templates should be pre-approved?
- Does any planned analytics, fraud-prevention, identity, communications, or background-check vendor introduce additional federal or state duties?
- How should Cirvice handle access, correction, deletion, and account-export requests that it voluntarily promises, even where no general state privacy statute requires them?

## 4. Commercial email and account notifications

### Requirements

CAN-SPAM applies to commercial email and also prohibits materially false or misleading header information in commercial and transactional/relationship messages. Commercial email must use accurate routing and “From” information, nondeceptive subject lines, a functioning opt-out mechanism, a valid physical postal address, and timely opt-out processing; commercial messages generally may not continue more than 10 business days after a valid opt-out. ([15 U.S.C. § 7704](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap103-sec7704.htm); [16 C.F.R. pt. 316](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-316))

Federal law generally preempts state laws specifically regulating commercial email, except state rules addressing falsity or deception and generally applicable contract, tort, fraud, or computer-crime law. ([15 U.S.C. § 7707](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap103-sec7707.htm))

### Launch controls

- Classify every template before use:
  - account verification, security, terms changes, and inquiry-message alerts are likely transactional/relationship messages when kept focused on the account or requested interaction;
  - launch promotions, provider discovery campaigns, newsletters, and re-engagement messages are commercial;
  - mixed messages require primary-purpose analysis under the FTC rule.
- Keep essential account/security notices separate from marketing preferences. A marketing opt-out should not disable a security or requested-message notice.
- Establish a business postal address before sending promotional email; do not expose a founder's home address merely to satisfy the email footer.
- Maintain suppression lists and require the email vendor to honor them. Cirvice remains responsible for messages sent on its behalf.
- Treat Facebook-group links and member invitations as access paths, not permission for unrelated promotional email.

### Counsel question

Classify the first-neighborhood launch invitation, provider-listing announcements, and any mixed notification/marketing templates before sending them at scale.

## 5. Content, moderation, private messages, and legal process

### Section 230 is limited protection, not a compliance plan

47 U.S.C. § 230 generally prevents treating an interactive-computer-service provider as the publisher or speaker of information supplied by another information-content provider and protects certain good-faith moderation. It expressly does not displace federal criminal law, intellectual-property law, communications-privacy law, or specified sex-trafficking claims. It also does not protect Cirvice from liability for content Cirvice materially creates or for Cirvice's own promises and conduct. ([47 U.S.C. § 230](https://www.govinfo.gov/content/pkg/USCODE-2025-title47/html/USCODE-2025-title47-chap5-subchapII-partI-sec230.htm))

### Copyright

Section 230 does not cover intellectual property. The DMCA's user-storage safe harbor is conditional: among other things, a service provider must designate and publish an agent, register that agent with the Copyright Office, respond expeditiously to valid notices, provide the statutory counter-notice process, adopt and reasonably implement a repeat-infringer policy, and accommodate standard technical measures. ([17 U.S.C. § 512](https://www.govinfo.gov/content/pkg/USCODE-2025-title17/html/USCODE-2025-title17-chap5-sec512.htm); [U.S. Copyright Office DMCA Designated Agent Directory](https://www.copyright.gov/dmca-directory/); [37 C.F.R. § 201.38](https://www.ecfr.gov/current/title-37/chapter-II/subchapter-A/part-201/section-201.38))

**Risk/control:** If users can upload listing photos, logos, text, or attachments, implement a DMCA policy and agent registration before launch if counsel recommends preserving the safe harbor. Terms should grant Cirvice only the content license needed to host, display, moderate, and remove user content and should prohibit infringement and impersonation.

### Nonconsensual intimate imagery

The federal TAKE IT DOWN Act required a “covered platform” to establish a clear notice-and-removal process by May 19, 2026. A covered platform must remove a validly reported nonconsensual intimate visual depiction, and make reasonable efforts to remove known identical copies, as soon as possible and no later than 48 hours after receiving the request. The definition includes a public-serving website or online service that primarily provides a forum for user-generated content, including messages, but excludes email and certain services where interactive features are incidental to provider-selected content. ([TAKE IT DOWN Act, Pub. L. 119-12, § 3](https://www.govinfo.gov/content/pkg/PLAW-119publ12/html/PLAW-119publ12.htm))

**Counsel question:** Does a private, resident-only service-listing and messaging marketplace “serve the public” and “primarily provide[] a forum for user-generated content”? If yes—or if uncertain—implement a documented workflow for the statutory notice, identity/contact, signature, location, good-faith statement, 48-hour removal, and duplicate-removal duties before launch.

### Child sexual exploitation reports

A covered provider that obtains actual knowledge of facts or circumstances showing an apparent child-pornography offense must report to NCMEC's CyberTipline as soon as reasonably possible. The statute does not itself require providers to monitor or affirmatively search, screen, or scan. A completed report triggers a 90-day preservation duty for the submitted content and reasonably accessible contextual material, with secure storage and restricted access. ([18 U.S.C. § 2258A](https://www.govinfo.gov/content/pkg/USCODE-2025-title18/html/USCODE-2025-title18-partI-chap110-sec2258A.htm))

**Requirement/control:** Create a restricted escalation path so moderators do not download, duplicate, forward, or casually circulate suspected child sexual abuse material. Counsel should prepare the reporting and evidence-handling procedure.

### Stored communications and monitoring

If Cirvice is an electronic communication service or remote computing service to the public, the Stored Communications Act restricts voluntary disclosure of message contents and customer records, subject to statutory exceptions. A government preservation request requires preservation for 90 days and a renewed request adds another 90 days. Unauthorized access to stored communications can also create criminal and civil exposure. ([18 U.S.C. §§ 2701–2703, 2707](https://www.govinfo.gov/content/pkg/USCODE-2025-title18/html/USCODE-2025-title18-partI-chap121.htm))

**Counsel questions:**

- Is Cirvice an electronic communication service “to the public” despite neighborhood approval and private threads?
- What terms/consent permit administrator access for support, abuse reports, and safety while respecting federal and state communications law?
- Does any automated scanning or contemporaneous message review implicate the Wiretap Act, and what provider/consent exception is available? ([18 U.S.C. § 2511](https://www.govinfo.gov/content/pkg/USCODE-2025-title18/html/USCODE-2025-title18-partI-chap119-sec2511.htm))
- Who may receive and validate subpoenas, warrants, emergency requests, preservation letters, civil demands, and user-notice restrictions?

### Moderation controls

Before launch, publish and operationalize:

- prohibited services and content;
- truthful identity, business-team, credential, and insurance rules;
- harassment, discrimination, fraud, exploitation, dangerous-service, sexual-service, trafficking, and illegal-content rules;
- user reporting, emergency direction, investigation, appeal, suspension, and termination procedures;
- moderator access limits and audit logs;
- evidence preservation and legal-process escalation; and
- a policy against promises that every message or listing is proactively monitored.

South Carolina's Stop Harm from Addictive Social Media Act takes effect January 1, 2027, but its “covered social media platform” definition is limited to platforms with at least $1 billion in worldwide annual advertising revenue in a qualifying year. It is not a Cirvice launch requirement on the stated facts, but its classification should be rechecked if the business or law changes. ([S.C. Code §§ 39-5-910–39-5-1000](https://www.scstatehouse.gov/code/t39c005))

## 6. Provider categories, licenses, permits, and credential claims

### Why this is a launch blocker

Licensing turns on the service, project value, location, and sometimes who contracts with the customer. A provider licensed in one state is not automatically authorized in the other. The place where the work is performed—not only the provider's residence—must drive the check.

Examples illustrate the mismatch:

- **SC commercial/general or mechanical contracting:** a license is required for contracting work when total construction cost is greater than $10,000. ([S.C. Code § 40-11-30](https://www.scstatehouse.gov/code/t40c011))
- **SC residential work:** a residential builder includes specified residential construction, repair, or improvement over $5,000; residential specialty contracting can begin above $500, and specified trades require licensing or registration. ([S.C. Code §§ 40-59-20, 40-59-30, 40-59-220](https://www.scstatehouse.gov/code/t40c059))
- **NC general contracting:** the general-contractor threshold is $40,000 or more. ([N.C. Gen. Stat. § 87-1](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_87/GS_87-1.html))
- **NC electrical work:** engaging or offering to engage in electrical contracting requires the applicable license. ([N.C. Gen. Stat. § 87-43](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_87/GS_87-43.html))
- **NC plumbing/heating/fire sprinklers:** covered contracting requires licensing, subject to defined exceptions including certain minor repairs or replacements. ([N.C. Gen. Stat. § 87-21](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_87/GS_87-21.html))
- **NC locksmithing:** performing or offering locksmith services requires a license. ([N.C. Gen. Stat. § 74F-3](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_74F/GS_74F-3.html))

SC's contractor law also authorizes discipline for aiding an unlicensed entity to evade the law and for false or deceptive advertising. ([S.C. Code § 40-11-110](https://www.scstatehouse.gov/code/t40c011))

### Required launch work

Create a counsel-reviewed **service-category matrix** with, for each state and category:

1. whether the category is allowed, conditionally allowed, or prohibited at launch;
2. license, registration, certification, bond, insurance, permit, supervision, and project-value rules;
3. the official issuing authority and public lookup;
4. what evidence Cirvice checks, who checks it, and renewal/expiration cadence;
5. exact customer-facing label language;
6. whether a business entity, individual qualifier, or every worker must hold the credential;
7. whether team or subcontracted performance is permitted and what must be disclosed; and
8. what happens when a credential expires, is suspended, cannot be verified, or is reported false.

Official starting points are the [South Carolina Department of Labor, Licensing and Regulation professions list](https://llr.sc.gov/professions.aspx) and [North Carolina professional licenses and permits portal](https://www.nc.gov/working/professional-licenses-permits), followed by the governing board's statute and rules.

### Categories requiring express counsel review before being allowed

At minimum: construction and home repair; electrical, plumbing, HVAC, alarm, locksmith, and pest-control work; child care and transportation of children; elder, disability, home-care, or health-related services; food preparation/catering; passenger transportation; legal, tax, accounting, investment, insurance, real-estate, and other professional advice; security services; animal care where regulated; and any service involving weapons, controlled substances, hazardous materials, or entry into an occupied home.

## 7. Accessibility and nondiscrimination

### Federal and state risk

DOJ states that ADA Title III requires businesses open to the public to provide full and equal enjoyment and that its requirements apply to goods, services, privileges, and activities offered on the web. DOJ also states that it has not adopted a detailed Title III website technical standard, while identifying WCAG as useful technical guidance. ([42 U.S.C. § 12182](https://www.govinfo.gov/content/pkg/USCODE-2025-title42/html/USCODE-2025-title42-chap126-subchapIII-sec12182.htm); [DOJ, Guidance on Web Accessibility and the ADA](https://www.ada.gov/resources/web-guidance/))

North Carolina prohibits denying a qualified person with a disability full and equal enjoyment of a place of public accommodation and defines such places to include establishments that supply goods or services to the public or solicit or accept any person's patronage. South Carolina protects full and equal use of public accommodations and prohibits disability discrimination without reasonable justification. ([N.C. Gen. Stat. §§ 168A-3, 168A-6, 168A-11](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_168A/GS_168A-6.html); [S.C. Code §§ 43-33-20, 43-33-520–43-33-540](https://www.scstatehouse.gov/code/t43c033))

### Launch controls

- Treat keyboard operation, visible focus, semantic structure, form labels and errors, sufficient contrast, zoom/reflow, screen-reader support, text alternatives, reduced-motion support, and accessible authentication/messaging as acceptance criteria.
- Test core resident, provider, inquiry, messaging, moderation, and account-recovery flows with automated tools **and** manual keyboard/screen-reader review.
- Provide a plainly visible accessibility/support contact and a process for timely remediation or an effective alternative.
- Ensure residency verification has an accessible manual route and does not force use of Facebook, inaccessible documents, or a single sensory method.
- Do not claim “ADA compliant” based only on an automated scan or overlay.

### Counsel questions

- Is Cirvice a federal or state public accommodation despite residence eligibility and login controls?
- Could any federal private-club exemption apply, and would the commercial marketplace model or broad neighborhood availability defeat it?
- What accessibility statement and remediation process accurately describe launch readiness without overpromising?

## 8. Terms, electronic assent, and policy architecture

### Electronic records

Federal E-SIGN and both states' Uniform Electronic Transactions Acts generally prevent denying legal effect solely because a record, contract, or signature is electronic. They preserve substantive law, require retainable/reproducible records in specified situations, and provide rules for attribution and retention. Federal law adds detailed consent rules when another law requires consumer information to be provided in writing and it is delivered electronically. ([15 U.S.C. § 7001](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap96-subchapI-sec7001.htm); [S.C. Code §§ 26-6-70–26-6-120](https://www.scstatehouse.gov/code/t26c006); [N.C. Gen. Stat. §§ 66-317–66-322](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_66/GS_66-317.html))

### Launch controls

Use affirmative, recorded assent rather than passive browsewrap. Preserve:

- the exact version of terms and linked policies shown;
- the account, timestamp, action, and relevant technical evidence of assent;
- notices and assent for material changes; and
- a user-accessible copy capable of download or printing.

The policy set should include:

1. **Terms of Service** — eligibility, account ownership, platform role, direct provider/customer relationship, acceptable use, content license, suspension/termination, disclaimers, liability allocation, disputes, governing law, and policy-change process.
2. **Privacy Notice** — actual data practice, vendors, sharing, security, retention, closure, and contact.
3. **Community and Service Rules** — prohibited services/content, credential claims, team disclosure, safety, reporting, moderation, appeals, and enforcement.
4. **Provider Terms** — truthful listings, licenses/permits/tax/insurance, no agency, customer contract responsibility, worker/team disclosure, and evidence obligations.
5. **Copyright/DMCA Policy** and, if applicable, **TAKE IT DOWN notice-and-removal process**.
6. **Accessibility contact/process** and **law-enforcement request policy** suitable for a private service.

### Attorney drafting required

Qualified SC/NC counsel should draft or approve:

- the precise platform/provider/customer relationship and disclaimers;
- limitation of liability, indemnity, release, warranty disclaimer, arbitration, class waiver, venue, and choice-of-law clauses;
- what rights cannot be waived under federal, SC, or NC consumer law;
- termination and appeal rights;
- consent to moderation and administrator access to private messages;
- electronic-delivery consent where a law requires written notice;
- minors/age representations; and
- consistency among product copy, onboarding, terms, privacy notice, and actual operations.

## 9. Records, retention, deletion, and legal holds

### Requirements

- If another law requires a record to be retained, E-SIGN and the state UETA statutes generally allow electronic retention when the record accurately reflects the final information and remains accessible and reproducible for the required period. ([15 U.S.C. § 7001(d)](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap96-subchapI-sec7001.htm); [S.C. Code § 26-6-120](https://www.scstatehouse.gov/code/t26c006); [N.C. Gen. Stat. § 66-322](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_66/GS_66-322.html))
- Government preservation requests under 18 U.S.C. § 2703(f) require 90-day preservation, extendable once for another 90 days. NCMEC reports trigger the separate 90-day preservation and security duties described above. ([18 U.S.C. § 2703(f)](https://www.govinfo.gov/content/pkg/USCODE-2025-title18/html/USCODE-2025-title18-partI-chap121-sec2703.htm); [18 U.S.C. § 2258A(h)](https://www.govinfo.gov/content/pkg/USCODE-2025-title18/html/USCODE-2025-title18-partI-chap110-sec2258A.htm))
- SC and NC secure-disposal statutes apply when covered personal information is disposed of. ([S.C. Code § 37-20-190](https://www.scstatehouse.gov/code/t37c020); [N.C. Gen. Stat. § 75-64](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-64.html))

### Launch controls

Adopt a written schedule covering:

- account and eligibility records;
- invitation attribution and manual-review notes;
- provider credential evidence and check dates;
- listing versions, approvals, rejections, and reports;
- terms/policy versions and assent evidence;
- private messages and attachments;
- email consent, classification, delivery, and suppression events;
- moderation, appeals, safety reports, and administrator access logs;
- security logs, incidents, and breach decisions;
- vendor, insurance, entity, tax, and governance records; and
- backups and deletion propagation.

Use the shortest period consistent with operational need, promised practice, limitation periods, insurance, tax/entity duties, safety needs, and counsel advice. Add a documented legal-hold process that suspends ordinary deletion for identified records. Indefinite retention “just in case” increases breach and discovery exposure.

## 10. Entity structure, cross-state qualification, local operation, and insurance

### Entity and foreign qualification

A separate entity can help separate business liabilities from personal affairs only if it is correctly formed and operated. Counsel and a tax professional should choose the formation state, tax treatment, governance, ownership, contracts, banking, and capitalization.

A foreign LLC may need authority before transacting business in the other state. SC and NC list activities that do not alone constitute transacting business, including interstate commerce; NC also lists selling property or services through independent contractors. Those exclusions do not decide taxation, regulation, personal jurisdiction, or whether Cirvice's full set of local activities requires qualification. ([S.C. Code §§ 33-44-1002–33-44-1008](https://www.scstatehouse.gov/code/t33c044); [N.C. Gen. Stat. §§ 57D-7-01–57D-7-03](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_57D/GS_57D-7-01.html))

**Counsel questions:**

- In which state should Cirvice be formed, and must it foreign-qualify in the other before launch?
- What registered agent, public business address, assumed-name filing, annual filing, state tax registration, and county/municipal business-license obligations apply to the operator's exact location and neighborhood boundaries?
- Does appointing a neighborhood administrator in the other state, soliciting providers there, or conducting manual residency review there change the answer?

FinCEN currently states that entities created in the United States are exempt from federal beneficial-ownership-information reporting under the Corporate Transparency Act; recheck this at formation because the rule has changed repeatedly. ([FinCEN, Beneficial Ownership Information](https://www.fincen.gov/boi))

### Workers' compensation and employees

If Cirvice hires employees, SC generally exempts a person regularly employing fewer than four employees in the same business, subject to statutory details; NC generally requires coverage for businesses regularly employing three or more employees, with stated exceptions and counting rules. Misclassification can change the count and obligations. ([S.C. Code § 42-1-360](https://www.scstatehouse.gov/code/t42c001); [NC Industrial Commission, Employers' obligation to obtain coverage](https://www.ic.nc.gov/wcinsrqmt.html))

### Insurance review

No source reviewed creates a general rule that every no-fee neighborhood listing marketplace must buy a particular policy. That does not make launch without insurance prudent. A licensed broker should assess:

- commercial general liability;
- technology errors and omissions;
- cyber/privacy and breach-response coverage;
- media liability for user content and advertising;
- directors and officers coverage;
- employment practices and workers' compensation if workers are hired;
- crime/social-engineering coverage; and
- umbrella/excess coverage.

Counsel and the broker should review exclusions for marketplace services, professional services, contractor work, bodily injury, abuse/molestation, cyber events, user content, and known incidents. Product copy must not imply that providers or customers are protected by Cirvice's policy. If provider insurance is displayed, define acceptable evidence, minimums by category, expiration handling, and the limits of certificate review.

## 11. Cross-state operating rules

- **Provider credentials:** check the state and locality where the service will be performed. A border resident may need different authority for work across the state line.
- **Consumer protection:** assume the resident's state consumer law may apply; do not rely on a choice-of-law clause to waive nonwaivable rights.
- **Privacy/breach:** identify affected residents by state and run both notice analyses where an incident crosses the border.
- **Entity/local licensing:** map the operator, administrators, business location, solicitation, and service area to state, county, and municipality.
- **Taxes:** providers remain responsible for their own income, business, and applicable sales/use tax duties, but Cirvice needs a new state-tax analysis before it handles payments, charges providers/customers, sells goods, or bundles taxable services.
- **Terms and support:** do not tell users that only one state's law protects them. Provide one support and incident process capable of routing state-specific obligations.

## Decisions requiring qualified counsel before launch

Cirvice should not launch to the full neighborhood until SC/NC counsel has answered and documented at least these questions:

1. What entity and formation state should be used, and is foreign qualification required?
2. Does the exact product make Cirvice an employer, agent, broker, contractor, seller, employment service, or regulated referral service for any category?
3. Which service categories are allowed, conditional, or prohibited in each state, and what credential evidence is required?
4. What exact claims may Cirvice make about residence approval, listing review, licenses, insurance, safety, or provider quality?
5. What provider/customer home-solicitation, cancellation, contract, permit, and disclosure rules should the platform warn about without assuming the provider's legal work?
6. Are the terms, provider terms, privacy notice, community rules, assent flow, dispute clauses, and electronic-delivery process enforceable in both states?
7. Is Cirvice covered by ADA Title III or state public-accommodation law, and what launch accessibility standard and remediation process should be adopted?
8. Is Cirvice covered by the TAKE IT DOWN platform definition, the Stored Communications Act service definitions, NCMEC reporting law, or Wiretap Act restrictions for planned moderation?
9. Should Cirvice register a DMCA agent and implement the full safe-harbor workflow before accepting user content?
10. What breach decision tree and regulator/resident notice templates satisfy SC and NC law?
11. What retention periods and legal-hold rules apply to terms assent, credentials, listings, messages, moderation, security logs, and incidents?
12. What local business-license, tax-registration, and permit obligations apply in the exact counties and municipalities?
13. What insurance should Cirvice carry, and what provider insurance evidence—if any—should it require or display?
14. How should underage accounts, suspected exploitation material, emergencies, threats, subpoenas, warrants, and preservation requests be handled?

## Recommended launch artifacts

These are compliance deliverables, not substitutes for counsel:

- counsel-approved service-category and credential matrix for both states;
- Terms of Service, Provider Terms, Privacy Notice, Community/Service Rules, DMCA Policy, and accessibility process;
- exact claim-language dictionary for “approved,” “checked,” “licensed,” and “insured”;
- administrator moderation handbook and restricted escalation runbook;
- TAKE IT DOWN assessment and, if applicable, takedown form/workflow;
- NCMEC and law-enforcement request procedures;
- CAN-SPAM template inventory and suppression process;
- data map, vendor register, security baseline, incident-response plan, and SC/NC breach matrix;
- retention/deletion schedule and legal-hold procedure;
- entity, foreign-qualification, tax, local-license, and insurance signoffs; and
- accessibility test plan and issue-reporting channel.

## Re-review triggers

Obtain a new legal review before adding any of the following:

- booking, payments, escrow, commissions, subscriptions, listing fees, tips, refunds, or dispute handling;
- physical goods, lending/borrowing, transportation booking, or delivery;
- ratings, written reviews, rankings, badges, endorsements, or “recommended” providers;
- identity-document collection, facial/biometric checks, background checks, credit reports, or full addresses;
- minors, household accounts, nonresident users, or public access;
- SMS, automated calls, push notifications, location tracking, targeted advertising, or sale/sharing of data;
- real-time chat, calls, video, public feeds, broad photo/file uploads, or automated message scanning;
- employees, assigned jobs, required pricing, provider uniforms, work supervision, or platform warranties;
- another neighborhood, state, or country; or
- any new high-risk or licensed service category.

## Primary-source index

### Federal

- [15 U.S.C. § 45 — FTC Act](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap2-subchapI-sec45.htm)
- [29 C.F.R. pt. 795 — FLSA employee/independent-contractor classification](https://www.ecfr.gov/current/title-29/subtitle-B/chapter-V/subchapter-B/part-795)
- [IRS — Independent contractor defined](https://www.irs.gov/businesses/small-businesses-self-employed/independent-contractor-defined)
- [15 U.S.C. § 7704 — CAN-SPAM requirements](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap103-sec7704.htm)
- [15 U.S.C. § 7707 — CAN-SPAM effect on other laws](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap103-sec7707.htm)
- [16 C.F.R. pt. 316 — CAN-SPAM rule](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-C/part-316)
- [47 U.S.C. § 230](https://www.govinfo.gov/content/pkg/USCODE-2025-title47/html/USCODE-2025-title47-chap5-subchapII-partI-sec230.htm)
- [17 U.S.C. § 512 — DMCA safe harbors](https://www.govinfo.gov/content/pkg/USCODE-2025-title17/html/USCODE-2025-title17-chap5-sec512.htm)
- [TAKE IT DOWN Act, Pub. L. 119-12](https://www.govinfo.gov/content/pkg/PLAW-119publ12/html/PLAW-119publ12.htm)
- [18 U.S.C. § 2258A — NCMEC reporting and preservation](https://www.govinfo.gov/content/pkg/USCODE-2025-title18/html/USCODE-2025-title18-partI-chap110-sec2258A.htm)
- [18 U.S.C. ch. 121 — Stored Communications Act](https://www.govinfo.gov/content/pkg/USCODE-2025-title18/html/USCODE-2025-title18-partI-chap121.htm)
- [15 U.S.C. § 7001 — E-SIGN](https://www.govinfo.gov/content/pkg/USCODE-2025-title15/html/USCODE-2025-title15-chap96-subchapI-sec7001.htm)
- [DOJ — Guidance on Web Accessibility and the ADA](https://www.ada.gov/resources/web-guidance/)
- [FinCEN — Beneficial Ownership Information](https://www.fincen.gov/boi)

### South Carolina

- [S.C. Code § 39-1-90 — breach notice](https://www.scstatehouse.gov/code/t39c001)
- [S.C. Code ch. 5, tit. 39 — Unfair Trade Practices Act and SHASM Act](https://www.scstatehouse.gov/code/t39c005)
- [S.C. Code § 37-20-190 — secure disposal](https://www.scstatehouse.gov/code/t37c020)
- [S.C. Code ch. 6, tit. 26 — Uniform Electronic Transactions Act](https://www.scstatehouse.gov/code/t26c006)
- [S.C. Code ch. 11, tit. 40 — contractors](https://www.scstatehouse.gov/code/t40c011)
- [S.C. Code ch. 59, tit. 40 — residential builders and specialty contractors](https://www.scstatehouse.gov/code/t40c059)
- [S.C. Code art. 10, ch. 44, tit. 33 — foreign LLCs](https://www.scstatehouse.gov/code/t33c044)
- [S.C. Code ch. 33, tit. 43 — disability/public accommodations](https://www.scstatehouse.gov/code/t43c033)
- [S.C. Code § 42-1-360 — workers' compensation exemptions](https://www.scstatehouse.gov/code/t42c001)

### North Carolina

- [N.C. Gen. Stat. §§ 75-1.1, 75-16 — unfair or deceptive practices](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-1.1.html)
- [N.C. Gen. Stat. §§ 75-64, 75-65 — disposal and breach notice](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-65.html)
- [N.C. Gen. Stat. art. 40, ch. 66 — Uniform Electronic Transactions Act](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/ByArticle/Chapter_66/Article_40.html)
- [N.C. Gen. Stat. ch. 87 — contractor, plumbing/HVAC, and electrical licensing](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/ByChapter/Chapter_87.html)
- [N.C. Gen. Stat. § 74F-3 — locksmith licensing](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_74F/GS_74F-3.html)
- [N.C. Gen. Stat. art. 7, ch. 57D — foreign LLCs](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/ByArticle/Chapter_57D/Article_7.html)
- [N.C. Gen. Stat. ch. 168A — Persons with Disabilities Protection Act](https://www.ncleg.gov/EnactedLegislation/Statutes/HTML/ByChapter/Chapter_168A.html)
- [NC Industrial Commission — workers' compensation coverage requirements](https://www.ic.nc.gov/wcinsrqmt.html)
