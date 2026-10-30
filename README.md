# Landgate

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

Landgate is the Western Australian Land Information Authority — the WA government agency that maintains the state land titles register, values every rateable property in Western Australia, and curates the state's foundational location data (cadastre, tenure, property addresses, sales evidence, imagery, elevation, geographic names). In the Australian real estate value chain Landgate sits underneath the listing portals (REA Group's realestate.com.au and Domain) and underneath PEXA's electronic conveyancing rail as the authoritative source of the public land record for WA; since 2019 the automated land titling and registry operations have been operated under a commercial services arrangement while Landgate retains the Registrar of Titles function and the data custodianship. Its API posture is genuinely split and should not be overstated — a real, anonymously callable public surface exists (the SLIP Shared Location Information Platform ArcGIS REST directory plus OGC WMS/WFS services, and the Data WA CKAN Action API that Landgate operates for the whole WA public sector), while the richer registry and subscription data sits behind SLIP subscription, transaction, publication, broker, distributor and value-added-reseller licences that must be signed and, for bulk downloads, behind a MyLandgate account login. There is no developer portal, no published OpenAPI, no API key self-service, and no RESO involvement of any kind — RESO is a North American MLS standard and is absent from this Australian government registry.

**Areas:** Real Estate · Australia · Land Registry · Title · Valuation · Property Data · Open Data · Geospatial · Government · Conveyancing · PropTech

## Landgate on APIs.io

Everything profiled for Landgate is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/landgate/](https://apis.io/providers/landgate/)** — or go straight to one of the APIs or properties below.

### APIs (10)

- [MyLandgate OpenID Connect / OAuth 2.0 (PingFederate)](https://apis.io/apis/landgate/mylandgate-openid-connect/) — Landgate's customer identity provider, running PingFederate. The OpenID Connect discovery document is served anonymously (HTTP 200, 2026-07-26) at…
- [Landgate Datasets API](https://apis.io/apis/landgate/landgate-datasets-api/) — Dataset (package) discovery and retrieval
- [Landgate Discovery API](https://apis.io/apis/landgate/landgate-discovery-api/) — Autocomplete, resource search and the DCAT catalog
- [Landgate Organizations API](https://apis.io/apis/landgate/landgate-organizations-api/) — Publishing organizations and groups
- [Landgate Query API](https://apis.io/apis/landgate/landgate-query-api/) — Feature query, identify and image export
- [Landgate Server API](https://apis.io/apis/landgate/landgate-server-api/) — Server-level information and the services directory
- [Landgate Services API](https://apis.io/apis/landgate/landgate-services-api/) — Map service and layer metadata
- [Landgate Site API](https://apis.io/apis/landgate/landgate-site-api/) — Catalogue-level status and reference lists
- [Landgate WFS API](https://apis.io/apis/landgate/landgate-wfs-api/) — OGC Web Feature Service 2.0.0
- [Landgate WMS API](https://apis.io/apis/landgate/landgate-wms-api/) — OGC Web Map Service 1.3.0

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [landgate](https://apis.io/servers/landgate/landgate/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Landgate Agentic Access](https://apis.io/agentic-access/landgate/landgate-agentic-access/)

#### Collections (6)

Postman and Open Collection request collections.

- [Data WA CKAN Action API (operated by Landgate)](https://apis.io/collections/landgate/open-landgate-data-wa-ckan/)
- [API Collection](https://apis.io/collections/landgate/open-landgate-mylandgate-openid-configuration/)
- [Landgate SLIP Public Services (ArcGIS REST)](https://apis.io/collections/landgate/open-landgate-slip-public-arcgis/)
- [API Collection](https://apis.io/collections/landgate/open-landgate-slip-public-arcgis-rest-services/)
- [Landgate SLIP Public OGC Web Services (WMS / WFS)](https://apis.io/collections/landgate/open-landgate-slip-public-ogc/)
- [API Collection](https://apis.io/collections/landgate/open-landgate-slip-public-services-folder/)

#### Overlays (3)

OpenAPI overlays, including conversational phrasing for each operation.

- [Landgate Data Wa Ckan Overlay](https://apis.io/overlays/landgate/landgate-data-wa-ckan-overlay/)
- [Landgate Slip Public Arcgis Overlay](https://apis.io/overlays/landgate/landgate-slip-public-arcgis-overlay/)
- [Landgate Slip Public Ogc Overlay](https://apis.io/overlays/landgate/landgate-slip-public-ogc-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Landgate Authentication](https://apis.io/security/landgate/landgate-authentication/)
- [Landgate Domain Security](https://apis.io/security/landgate/landgate-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Landgate Scopes](https://apis.io/scopes/landgate/landgate-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.landgate.wa.gov.au/)
- [Documentation](https://www.landgate.wa.gov.au/location-data-and-services/discovering-landgate-data/)
- [Pricing](https://www.landgate.wa.gov.au/location-data-and-services/discovering-landgate-data/licensing/)
- [Support](https://www.landgate.wa.gov.au/help-centre/)
- [Changelog](https://www.landgate.wa.gov.au/about-us/customer-news-and-media/news-and-media-articles/)
- [Blog](https://www.landgate.wa.gov.au/about-us/customer-news-and-media/news-and-media-articles/)
- [Terms of service](https://www.landgate.wa.gov.au/disclaimer)
- [Privacy policy](https://www.landgate.wa.gov.au/privacy)
- [GitHub](https://github.com/Landgate)

## API Evangelist rating

**Kin Score 36.1** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 82.1 |
| Contract quality | 14.5 |
| Contract governance | 4.5 |
| Operational transparency | 18.4 |
| Developer ergonomics | 47.0 |
| Access clarity | 38.2 |

**Agent readiness 36.5** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | na |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | na |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | na |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |

**Regulatory alignment 42.2** — Government & Public Sector

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/landgate/](https://apis.io/providers/landgate/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Landgate: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/landgate/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
