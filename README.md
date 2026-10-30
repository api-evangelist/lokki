# Lokki

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Lokki is a Grenoble, France rental-management SaaS (getlokki.com) used by 2,500+ equipment rental businesses across bikes, e-bikes, scooters, cars, ski, climbing, surf, paddle, canoe/kayak, boats, event gear, groundskeeping equipment and tooling, paired with the lokki.rent consumer rental marketplace. Lokki publishes a partner-facing read-only REST API — the Lokki External API, seven operations on https://prod.api.eu-west-3.lokki.rent covering stores (rental providers), store items with date-range pricing and stock, and the verticale/category taxonomy — documented on a Mintlify docs host at docs.getlokki.com with an OpenAPI 3.1 specification, llms.txt, an A2A agent card, a provider-authored Agent Skill and an anonymous documentation MCP server. Authentication is an environment-scoped API key in the x-api-key header (lokki_sk_test_ for staging, lokki_sk_live_ for production) issued by a Lokki representative under a partnership agreement, with scopes at domain, action and route level. The same production host also serves an unauthenticated NestJS Swagger document for the 896-operation internal Dashboard / Online Store API. Lokki has raised roughly €6.3M, led by blisce with Racine2 (Serena + makesense), 50 Partners Impact, FJ Labs and Silence VC.

**Areas:** Company · Climate Tech · Circular Economy · Rentals · Equipment Rental · Bike Rental · Marketplace · Booking · Reservations · Inventory · Catalog · Pricing

## Lokki on APIs.io

Everything profiled for Lokki is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/lokki/](https://apis.io/providers/lokki/)** — or go straight to one of the APIs or properties below.

### APIs (97)

- [Lokki Action Log API](https://apis.io/apis/lokki/lokki-action-log-api/) — The Action Log API from Lokki — 3 operation(s) for action log.
- [Lokki Admin API](https://apis.io/apis/lokki/lokki-admin-api/) — The Admin API from Lokki — 70 operation(s) for admin.
- [Lokki Ahrefs API](https://apis.io/apis/lokki/lokki-ahrefs-api/) — The ahrefs API from Lokki — 1 operation(s) for ahrefs.
- [Lokki Ancv API](https://apis.io/apis/lokki/lokki-ancv-api/) — The Ancv API from Lokki — 3 operation(s) for ancv.
- [Lokki Api Key API](https://apis.io/apis/lokki/lokki-api-key-api/) — The Api Key API from Lokki — 5 operation(s) for api key.
- [Lokki Api Key V2 API](https://apis.io/apis/lokki/lokki-api-key-v2-api/) — The Api Key V2 API from Lokki — 2 operation(s) for api key v2.
- [Lokki Auth API](https://apis.io/apis/lokki/lokki-auth-api/) — The Auth API from Lokki — 1 operation(s) for auth.
- [Lokki Aws S3 API](https://apis.io/apis/lokki/lokki-aws-s3-api/) — The Aws S3 API from Lokki — 2 operation(s) for aws s3.
- [Lokki Bookings API](https://apis.io/apis/lokki/lokki-bookings-api/) — The Bookings API from Lokki — 10 operation(s) for bookings.
- [Lokki Business Registry API](https://apis.io/apis/lokki/lokki-business-registry-api/) — The Business Registry API from Lokki — 1 operation(s) for business registry.
- [Lokki Cart Suggestion API](https://apis.io/apis/lokki/lokki-cart-suggestion-api/) — The Cart Suggestion API from Lokki — 4 operation(s) for cart suggestion.
- [Lokki Catalogue API](https://apis.io/apis/lokki/lokki-catalogue-api/) — The Catalogue API from Lokki — 5 operation(s) for catalogue.
- [Lokki Chaos API](https://apis.io/apis/lokki/lokki-chaos-api/) — The Chaos API from Lokki — 6 operation(s) for chaos.
- [Lokki Company API](https://apis.io/apis/lokki/lokki-company-api/) — The Company API from Lokki — 104 operation(s) for company.
- [Lokki Company Payout API](https://apis.io/apis/lokki/lokki-company-payout-api/) — The Company Payout API from Lokki — 1 operation(s) for company payout.
- [Lokki Company Redirect API](https://apis.io/apis/lokki/lokki-company-redirect-api/) — The Company Redirect API from Lokki — 1 operation(s) for company redirect.
- [Lokki Company Signatures API](https://apis.io/apis/lokki/lokki-company-signatures-api/) — The Company Signatures API from Lokki — 1 operation(s) for company signatures.
- [Lokki Customer API](https://apis.io/apis/lokki/lokki-customer-api/) — The Customer API from Lokki — 8 operation(s) for customer.
- [Lokki Customer Model API](https://apis.io/apis/lokki/lokki-customer-model-api/) — The Customer Model API from Lokki — 3 operation(s) for customer model.
- [Lokki Delivery API](https://apis.io/apis/lokki/lokki-delivery-api/) — The Delivery API from Lokki — 13 operation(s) for delivery.
- [Lokki Document API](https://apis.io/apis/lokki/lokki-document-api/) — The Document API from Lokki — 4 operation(s) for document.
- [Lokki Document Model API](https://apis.io/apis/lokki/lokki-document-model-api/) — The Document Model API from Lokki — 3 operation(s) for document model.
- [Lokki Document State API](https://apis.io/apis/lokki/lokki-document-state-api/) — The Document State API from Lokki — 2 operation(s) for document state.
- [Lokki Editorial API](https://apis.io/apis/lokki/lokki-editorial-api/) — The Editorial API from Lokki — 3 operation(s) for editorial.
- [Lokki Email Template API](https://apis.io/apis/lokki/lokki-email-template-api/) — The Email Template API from Lokki — 4 operation(s) for email template.
- [Lokki Employee API](https://apis.io/apis/lokki/lokki-employee-api/) — The Employee API from Lokki — 7 operation(s) for employee.
- [Lokki Export Csv API](https://apis.io/apis/lokki/lokki-export-csv-api/) — The Export Csv API from Lokki — 2 operation(s) for export csv.
- [Lokki External API](https://apis.io/apis/lokki/lokki-external-api/) — The External API from Lokki — 7 operation(s) for external.
- [Lokki External Companies API](https://apis.io/apis/lokki/lokki-external-companies-api/) — The External Companies API from Lokki — 11 operation(s) for external companies.
- [Lokki Fathom API](https://apis.io/apis/lokki/lokki-fathom-api/) — The Fathom API from Lokki — 8 operation(s) for fathom.
- [Lokki G8 API](https://apis.io/apis/lokki/lokki-g8-api-api/) — The G8 Api API from Lokki — 2 operation(s) for g8 api.
- [Lokki Harvestr API](https://apis.io/apis/lokki/lokki-harvestr-api/) — The Harvestr API from Lokki — 1 operation(s) for harvestr.
- [Lokki Health API](https://apis.io/apis/lokki/lokki-health-api/) — The Health API from Lokki — 1 operation(s) for health.
- [Lokki Invoice API](https://apis.io/apis/lokki/lokki-invoice-api/) — The Invoice API from Lokki — 2 operation(s) for invoice.
- [Lokki Login API](https://apis.io/apis/lokki/lokki-login-api/) — The Login API from Lokki — 22 operation(s) for login.
- [Lokki Lokkit API](https://apis.io/apis/lokki/lokki-lokkit-api/) — The Lokkit API from Lokki — 3 operation(s) for lokkit.
- [Lokki Magic Schedule API](https://apis.io/apis/lokki/lokki-magic-schedule-api/) — The Magic Schedule API from Lokki — 2 operation(s) for magic schedule.
- [Lokki Mail API](https://apis.io/apis/lokki/lokki-mail-api/) — The Mail API from Lokki — 7 operation(s) for mail.
- [Lokki Mail V2 API](https://apis.io/apis/lokki/lokki-mail-v2-api/) — The Mail V2 API from Lokki — 1 operation(s) for mail v2.
- [Lokki Maps API](https://apis.io/apis/lokki/lokki-maps-api/) — The Maps API from Lokki — 2 operation(s) for maps.
- [Lokki Marketing API](https://apis.io/apis/lokki/lokki-marketing-api/) — The Marketing API from Lokki — 3 operation(s) for marketing.
- [Lokki Multi Order API](https://apis.io/apis/lokki/lokki-multi-order-api/) — The Multi Order API from Lokki — 3 operation(s) for multi order.
- [Lokki Offline API](https://apis.io/apis/lokki/lokki-offline-api/) — The Offline API from Lokki — 1 operation(s) for offline.
- [Lokki Online Store API](https://apis.io/apis/lokki/lokki-online-store-api/) — The Online Store API from Lokki — 34 operation(s) for online store.
- [Lokki Online Store Text API](https://apis.io/apis/lokki/lokki-online-store-text-api/) — The Online Store Text API from Lokki — 1 operation(s) for online store text.
- [Lokki Order API](https://apis.io/apis/lokki/lokki-order-api/) — The Order API from Lokki — 48 operation(s) for order.
- [Lokki Order Deliveries API](https://apis.io/apis/lokki/lokki-order-deliveries-api/) — The Order Deliveries API from Lokki — 1 operation(s) for order deliveries.
- [Lokki Order Event API](https://apis.io/apis/lokki/lokki-order-event-api/) — The Order Event API from Lokki — 54 operation(s) for order event.
- [Lokki Order Lld API](https://apis.io/apis/lokki/lokki-order-lld-api/) — The Order Lld API from Lokki — 36 operation(s) for order lld.
- [Lokki Order Refusal API](https://apis.io/apis/lokki/lokki-order-refusal-api/) — The Order Refusal API from Lokki — 1 operation(s) for order refusal.
- [Lokki Order Waiting List API](https://apis.io/apis/lokki/lokki-order-waiting-list-api/) — The Order Waiting List API from Lokki — 2 operation(s) for order waiting list.
- [Lokki Pack API](https://apis.io/apis/lokki/lokki-pack-api/) — The Pack API from Lokki — 10 operation(s) for pack.
- [Lokki Password Recovery API](https://apis.io/apis/lokki/lokki-password-recovery-api/) — The Password Recovery API from Lokki — 2 operation(s) for password recovery.
- [Lokki Payment API](https://apis.io/apis/lokki/lokki-payment-api/) — The Payment API from Lokki — 9 operation(s) for payment.
- [Lokki Payment V2 API](https://apis.io/apis/lokki/lokki-payment-v2-api/) — The Payment V2 API from Lokki — 17 operation(s) for payment v2.
- [Lokki Price Rules API](https://apis.io/apis/lokki/lokki-price-rules-api/) — The Price Rules API from Lokki — 2 operation(s) for price rules.
- [Lokki Price Template API](https://apis.io/apis/lokki/lokki-price-template-api/) — The Price Template API from Lokki — 3 operation(s) for price template.
- [Lokki Product Availability API](https://apis.io/apis/lokki/lokki-product-availability-api/) — The Product Availability API from Lokki — 5 operation(s) for product availability.
- [Lokki Product History API](https://apis.io/apis/lokki/lokki-product-history-api/) — The Product History API from Lokki — 5 operation(s) for product history.
- [Lokki Product State Model API](https://apis.io/apis/lokki/lokki-product-state-model-api/) — The Product State Model API from Lokki — 2 operation(s) for product state model.
- [Lokki Product Surveys API](https://apis.io/apis/lokki/lokki-product-surveys-api/) — The Product Surveys API from Lokki — 2 operation(s) for product surveys.
- [Lokki Product Verticale Category API](https://apis.io/apis/lokki/lokki-product-verticale-category-api/) — The Product Verticale Category API from Lokki — 8 operation(s) for product verticale category.
- [Lokki Products API](https://apis.io/apis/lokki/lokki-products-api/) — The Products API from Lokki — 34 operation(s) for products.
- [Lokki Promo Code API](https://apis.io/apis/lokki/lokki-promo-code-api/) — The Promo Code API from Lokki — 5 operation(s) for promo code.
- [Lokki Quote Request API](https://apis.io/apis/lokki/lokki-quote-request-api/) — The Quote Request API from Lokki — 4 operation(s) for quote request.
- [Lokki Reconditioning API](https://apis.io/apis/lokki/lokki-reconditioning-api/) — The Reconditioning API from Lokki — 11 operation(s) for reconditioning.
- [Lokki Rental Place API](https://apis.io/apis/lokki/lokki-rental-place-api/) — The Rental Place API from Lokki — 10 operation(s) for rental place.
- [Lokki Rental Place B2b API](https://apis.io/apis/lokki/lokki-rental-place-b2b-api/) — The Rental Place B2b API from Lokki — 7 operation(s) for rental place b2b.
- [Lokki Rental Place Cart API](https://apis.io/apis/lokki/lokki-rental-place-cart-api/) — The Rental Place Cart API from Lokki — 5 operation(s) for rental place cart.
- [Lokki Rental Place User API](https://apis.io/apis/lokki/lokki-rental-place-user-api/) — The Rental Place User API from Lokki — 13 operation(s) for rental place user.
- [Lokki Search Engine API](https://apis.io/apis/lokki/lokki-search-engine-api/) — The Search Engine API from Lokki — 4 operation(s) for search engine.
- [Lokki Self Test API](https://apis.io/apis/lokki/lokki-self-test-api/) — The Self Test API from Lokki — 2 operation(s) for self test.
- [Lokki Service API](https://apis.io/apis/lokki/lokki-service-api/) — The Service API from Lokki — 11 operation(s) for service.
- [Lokki Session Event API](https://apis.io/apis/lokki/lokki-session-event-api/) — The Session Event API from Lokki — 20 operation(s) for session event.
- [Lokki Shifter API](https://apis.io/apis/lokki/lokki-shifter-api-api/) — The Shifter Api API from Lokki — 2 operation(s) for shifter api.
- [Lokki Shop API](https://apis.io/apis/lokki/lokki-shop-api/) — The Shop API from Lokki — 19 operation(s) for shop.
- [Lokki Skiset API](https://apis.io/apis/lokki/lokki-skiset-api/) — The Skiset API from Lokki — 3 operation(s) for skiset.
- [Lokki Statistics V3 API](https://apis.io/apis/lokki/lokki-statistics-v3-api/) — The Statistics V3 API from Lokki — 1 operation(s) for statistics v3.
- [Lokki Status Model API](https://apis.io/apis/lokki/lokki-status-model-api/) — The Status Model API from Lokki — 4 operation(s) for status model.
- [Lokki Strapi API](https://apis.io/apis/lokki/lokki-strapi-api/) — The Strapi API from Lokki — 11 operation(s) for strapi.
- [Lokki Stripe Connect API](https://apis.io/apis/lokki/lokki-stripe-connect-api/) — The Stripe Connect API from Lokki — 5 operation(s) for stripe connect.
- [Lokki Sub Products API](https://apis.io/apis/lokki/lokki-sub-products-api/) — The Sub Products API from Lokki — 2 operation(s) for sub products.
- [Lokki Theme API](https://apis.io/apis/lokki/lokki-theme-api/) — The Theme API from Lokki — 1 operation(s) for theme.
- [Lokki Trustpilot API](https://apis.io/apis/lokki/lokki-trustpilot-api/) — The Trustpilot API from Lokki — 1 operation(s) for trustpilot.
- [Lokki Tulip V2 API](https://apis.io/apis/lokki/lokki-tulip-v2-api/) — The Tulip V2 API from Lokki — 1 operation(s) for tulip v2.
- [Lokki Universe API](https://apis.io/apis/lokki/lokki-universe-api/) — The Universe API from Lokki — 3 operation(s) for universe.
- [Lokki User API](https://apis.io/apis/lokki/lokki-user-api/) — The User API from Lokki — 7 operation(s) for user.
- [Lokki Visibility API](https://apis.io/apis/lokki/lokki-visibility-api/) — The Visibility API from Lokki — 12 operation(s) for visibility.
- [Lokki Webhook API](https://apis.io/apis/lokki/lokki-webhook-api/) — The Webhook API from Lokki — 1 operation(s) for webhook.
- [Lokki Workshop API](https://apis.io/apis/lokki/lokki-workshop-api/) — The Workshop API from Lokki — 11 operation(s) for workshop.
- [Lokki Workshop Intervention API](https://apis.io/apis/lokki/lokki-workshop-intervention-api/) — The Workshop Intervention API from Lokki — 2 operation(s) for workshop intervention.
- [Lokki Workshop Order API](https://apis.io/apis/lokki/lokki-workshop-order-api/) — The Workshop Order API from Lokki — 5 operation(s) for workshop order.
- [Lokki Workshop Payment API](https://apis.io/apis/lokki/lokki-workshop-payment-api/) — The Workshop Payment API from Lokki — 8 operation(s) for workshop payment.
- [Lokki Workshop Statistics API](https://apis.io/apis/lokki/lokki-workshop-statistics-api/) — The Workshop Statistics API from Lokki — 1 operation(s) for workshop statistics.
- [Lokki Your Order API](https://apis.io/apis/lokki/lokki-your-order-api/) — The Your Order API from Lokki — 9 operation(s) for your order.
- [Lokki Your Order Event API](https://apis.io/apis/lokki/lokki-your-order-event-api/) — The Your Order Event API from Lokki — 8 operation(s) for your order event.
- [Lokki Onboarding API](https://apis.io/apis/lokki/lokki-onboarding-api/) — The Onboarding API from Lokki — 4 operation(s) for onboarding.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [lokki-mcp.yml](https://apis.io/servers/lokki/lokki-mcp-yml/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Lokki Dashboard Api Overlay](https://apis.io/overlays/lokki/lokki-dashboard-api-overlay/)
- [Lokki External Api Overlay](https://apis.io/overlays/lokki/lokki-external-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Lokki Authentication](https://apis.io/security/lokki/lokki-authentication/)
- [Lokki Domain Security](https://apis.io/security/lokki/lokki-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Lokki Plans Pricing](https://apis.io/plans/lokki/lokki-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Lokki Rate Limits](https://apis.io/rate-limits/lokki/lokki-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.lokki.rent/)
- [Documentation](https://docs.getlokki.com/)
- [Getting started](https://docs.getlokki.com/api-reference/getting-started)
- [API reference](https://docs.getlokki.com/api-reference/getting-started)
- [Pricing](https://solutions.lokki.rent/en/tarifs)
- [Sign up](https://app.getlokki.com/welcome)
- [Blog](https://solutions.lokki.rent/en/blog)
- [Terms of service](https://solutions.lokki.rent/legals/conditions-generales-dutilisation)
- [Privacy policy](https://solutions.lokki.rent/legals/politique-de-confidentialite)
- [GitHub](https://github.com/LokkiApp)
- [Status](https://status.getlokki.com/)

## API Evangelist rating

**Kin Score 49.7** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 42.7 |
| Contract governance | 4.5 |
| Operational transparency | 47.4 |
| Developer ergonomics | 71.4 |
| Access clarity | 38.2 |

**Agent readiness 33.9** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | documented (partial credit) |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 24.5** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/lokki/](https://apis.io/providers/lokki/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Lokki: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/lokki/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
