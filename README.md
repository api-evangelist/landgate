# Landgate (landgate)

Landgate is the Western Australian Land Information Authority — the WA government agency that maintains the state land titles register, values every rateable property in Western Australia, and curates the state's foundational location data (cadastre, tenure, property addresses, sales evidence, imagery, elevation, geographic names). In the Australian real estate value chain Landgate sits underneath the listing portals (REA Group's realestate.com.au and Domain) and underneath PEXA's electronic conveyancing rail as the authoritative source of the public land record for WA; since 2019 the automated land titling and registry operations have been operated under a commercial services arrangement while Landgate retains the Registrar of Titles function and the data custodianship. Its API posture is genuinely split and should not be overstated — a real, anonymously callable public surface exists (the SLIP Shared Location Information Platform ArcGIS REST directory plus OGC WMS/WFS services, and the Data WA CKAN Action API that Landgate operates for the whole WA public sector), while the richer registry and subscription data sits behind SLIP subscription, transaction, publication, broker, distributor and value-added-reseller licences that must be signed and, for bulk downloads, behind a MyLandgate account login. There is no developer portal, no published OpenAPI, no API key self-service, and no RESO involvement of any kind — RESO is a North American MLS standard and is absent from this Australian government registry.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/landgate/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/landgate/refs/heads/main/apis.yml)

## Tags

- Real Estate
- Australia
- Land Registry
- Title
- Valuation
- Property Data
- Open Data
- Geospatial
- Government
- Conveyancing
- PropTech

## Timestamps

- **Created:** 2026-07-26
- **Modified:** 2026-07-26

## APIs

### SLIP Public Services (ArcGIS REST)

The public tier of Landgate's Shared Location Information Platform (SLIP), served as an Esri ArcGIS Server 12.1 REST services directory. Confirmed anonymously reachable on 2026-07-26 with HTTP 200 and `authInfo.isTokenBasedSecurity` false — 65 map services across five folders (SLIP_Public_Services with 57 services, plus Landgate_Public_Maps, Landgate_Public_Imagery, Land_Monitor and Utilities), covering cadastre, administrative and LGA boundaries, buildings and structures, bushfire prone areas, climate, disaster, transport and marine layers. A live layer query returned real LGA boundary features without any credential.

- **Human URL:** [https://www.landgate.wa.gov.au/location-data-and-services/programs-and-initiatives/slip/](https://www.landgate.wa.gov.au/location-data-and-services/programs-and-initiatives/slip/)
- **Base URL:** `https://public-services.slip.wa.gov.au/public/rest/services`

#### Tags

- Geospatial
- Cadastre
- Boundaries
- Open Access
- ArcGIS

#### Properties

- [ArcGIS REST services directory](openapi/landgate-slip-public-arcgis-rest-services.json)
- [ArcGIS SLIP_Public_Services folder](openapi/landgate-slip-public-services-folder.json)
- [API Reference](https://public-services.slip.wa.gov.au/public/rest/services?f=json)
- [Documentation](https://www.landgate.wa.gov.au/location-data-and-services/programs-and-initiatives/slip/)
- [Locate map viewer](https://maps.slip.wa.gov.au/landgate/locate/)

### SLIP Public OGC Web Services (WMS / WFS)

OGC-standard web services fronting the same SLIP public data. A WMS 1.3.0 GetCapabilities document (56 layers) and a WFS 2.0.0 GetCapabilities document (38 feature types) were both retrieved anonymously with HTTP 200 on 2026-07-26 and are saved verbatim. These GetCapabilities documents are the machine-readable contract for this surface — there is no OpenAPI and no OData `$metadata` anywhere on the Landgate estate.

- **Human URL:** [https://www.landgate.wa.gov.au/location-data-and-services/programs-and-initiatives/slip/](https://www.landgate.wa.gov.au/location-data-and-services/programs-and-initiatives/slip/)
- **Base URL:** `https://public-services.slip.wa.gov.au/public/services`

#### Tags

- Geospatial
- OGC
- WMS
- WFS
- Open Access

#### Properties

- [WMS 1.3.0 GetCapabilities](openapi/landgate-slip-public-wms-capabilities.xml)
- [WFS 2.0.0 GetCapabilities](openapi/landgate-slip-public-wfs-capabilities.xml)
- [Live WMS GetCapabilities](https://services.slip.wa.gov.au/public/services/SLIP_Public_Services/Boundaries/MapServer/WMSServer?request=GetCapabilities&service=WMS)
- [Documentation](https://www.landgate.wa.gov.au/location-data-and-services/discovering-landgate-data/)

### Data WA CKAN Action API

Landgate leads implementation of the WA Whole of Government Open Data Policy and operates data.wa.gov.au, whose catalogue runs CKAN with the standard `/api/3/action` surface exposed anonymously. Confirmed 2026-07-26 — `status_show`, `package_search`, `package_list` and `organization_show` all returned HTTP 200 without credentials; the catalogue holds 2,872 datasets, of which 395 are published by the Landgate organization. A DCAT JSON-LD catalog is served at `/catalog.jsonld`. Note honestly that the API is open but most Landgate datasets in it carry a custom Landgate licence rather than an open licence (371 of 395 are `custom_other`; only 2 are public domain and 5 are CC non-commercial).

- **Human URL:** [https://www.data.wa.gov.au/](https://www.data.wa.gov.au/)
- **Base URL:** `https://catalogue.data.wa.gov.au/api/3/action`

#### Tags

- Open Data
- Catalog
- CKAN
- DCAT
- Government

#### Properties

- [CKAN status_show](https://catalogue.data.wa.gov.au/api/3/action/status_show)
- [API Reference (help_show)](https://catalogue.data.wa.gov.au/api/3/action/help_show?name=package_search)
- [DCAT JSON-LD catalog](https://catalogue.data.wa.gov.au/catalog.jsonld)
- [Documentation](https://www.landgate.wa.gov.au/location-data-and-services/programs-and-initiatives/data-wa/)
- [Dataset catalogue](https://catalogue.data.wa.gov.au/dataset)

### MyLandgate OpenID Connect / OAuth 2.0 (PingFederate)

Landgate's customer identity provider, running PingFederate. The OpenID Connect discovery document is served anonymously (HTTP 200, 2026-07-26) at `/.well-known/openid-configuration` and is saved verbatim. It is a real, machine-readable authorization-server contract — but it is the sign-on for MyLandgate, Land Enquiry Services and SLIP subscriber accounts, not a public developer API. There is no public client registration endpoint, no published scope catalogue beyond the standard openid/profile/email/address/phone plus an ATO scope, and no developer documentation. Listed because the artifact is genuine, not because it is self-serve.

- **Human URL:** [https://land-enquiry.app.landgate.wa.gov.au/](https://land-enquiry.app.landgate.wa.gov.au/)
- **Base URL:** `https://sign-on.app.landgate.wa.gov.au`

#### Tags

- Authentication
- OpenID Connect
- OAuth 2.0
- Gated

#### Properties

- [OpenID configuration (harvested)](openapi/landgate-mylandgate-openid-configuration.json)
- [OpenID configuration (live)](https://sign-on.app.landgate.wa.gov.au/.well-known/openid-configuration)
- [Login](https://land-enquiry.app.landgate.wa.gov.au/)

## Common Properties

- [Website](https://www.landgate.wa.gov.au/)
- [About](https://www.landgate.wa.gov.au/about-us/)
- [Documentation](https://www.landgate.wa.gov.au/location-data-and-services/discovering-landgate-data/)
- [Pricing / Licensing](https://www.landgate.wa.gov.au/location-data-and-services/discovering-landgate-data/licensing/)
- [Support](https://www.landgate.wa.gov.au/help-centre/)
- [Data WA portal](https://www.data.wa.gov.au/)

## RESO Posture

No RESO reference found. RESO Web API and Data Dictionary certification are North American MLS/broker constructs administered by an industry body; Landgate is an Australian state land registry and is neither an MLS nor a listing portal. No RESO certification directory listing, no OData `$metadata`, and no Universal Property Identifier (UPI) are present. Landgate identifies land by WA cadastral identifiers instead — lot on plan, Certificate of Title volume/folio, and LGATE-nnn product codes.

## Access Gate

**licence-agreement.** The open SLIP and CKAN tier needs no signup at all, but everything of substance requires a signed Landgate licence: SLIP Subscription, Location Information Subscription, Transaction, Publication, Broker Agreement, Distributor Agreement, Value Added Reseller (VAR) Agreement, or a Trial Licence. Bulk downloads additionally require a MyLandgate account. There is no self-serve API key, no application form for developers, and onboarding runs through Landgate Customer Experience by phone and email.

## Maintainers

- **Kin Lane** — kin@apievangelist.com
