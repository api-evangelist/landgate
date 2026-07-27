---
name: Query Western Australian boundaries and cadastral layers on SLIP
description: Walk the anonymous SLIP ArcGIS REST directory from folders to services to layers,
  then query real features — WA local government areas, administrative boundaries and other
  public geospatial layers — without any credential.
api: openapi/landgate-slip-public-arcgis-openapi.yml
operations:
  - getSlipServerInfo
  - listSlipRootServices
  - listSlipFolderServices
  - getSlipMapService
  - getSlipLayer
  - querySlipLayerFeatures
  - identifySlipFeatures
generated: '2026-07-26'
method: generated
source: openapi/landgate-slip-public-arcgis-openapi.yml (operations verified live 2026-07-26)
---

# Query SLIP public geospatial layers

Base URL: `https://public-services.slip.wa.gov.au/public/rest`. Everything in this skill is
anonymous — `getSlipServerInfo` reports `authInfo.isTokenBasedSecurity: false`.

**Always append `f=json`.** The ArcGIS default is `f=html`; without the parameter you get a web
page, not data.

## Steps

1. **Confirm the surface is open.** `getSlipServerInfo` (`GET /info?f=json`) returns
   `currentVersion` and `authInfo`. If `isTokenBasedSecurity` is ever true, you are on the
   subscription host and need a licensed credential — stop.
2. **List folders.** `listSlipRootServices` (`GET /services?f=json`) returns the five folders:
   `Land_Monitor`, `Landgate_Public_Imagery`, `Landgate_Public_Maps`, `SLIP_Public_Services`,
   `Utilities`. Most public thematic data is in `SLIP_Public_Services`.
3. **List services in a folder.** `listSlipFolderServices`
   (`GET /services/SLIP_Public_Services?f=json`). Note the naming convention: a service and its
   OGC sibling appear as a pair, e.g. `Boundaries` and `Boundaries_WFS`.
4. **Get the service and its layer list.** `getSlipMapService`
   (`GET /services/SLIP_Public_Services/Boundaries/MapServer?f=json`). Record `maxRecordCount`
   (10000 on this service) — it caps every query response.
5. **Get the layer's fields before querying.** `getSlipLayer`
   (`GET /services/SLIP_Public_Services/Boundaries/MapServer/14?f=json`) returns `fields[]`,
   `geometryType` and `extent`. Layer 14 is WA local government area boundaries; its fields
   include `name`, `abs_lga_number`, `postcode`, `land_area`.
6. **Count first, then fetch.** Call `querySlipLayerFeatures` with
   `where=1=1&returnCountOnly=true&f=json` to size the result (139 for LGA boundaries), then
   re-query with `outFields=*` and `returnGeometry=false` if you only need attributes.
7. **Page with `resultOffset` / `resultRecordCount`.** Check `exceededTransferLimit` in the
   response; keep the page size at or under `maxRecordCount`.
8. **Point lookups** use `identifySlipFeatures` — it needs `geometry`, `geometryType`,
   `tolerance`, `mapExtent` and `imageDisplay` together; omitting any of them fails.

## Error handling — read this before writing a client

This server returns **HTTP 200 with an error body**. An unknown layer returns
`200 {"error":{"code":404,"details":[],"message":"Layer not found"}}`. Status-code-only error
handling will treat that as success. Always check for an `error` key first. See
`errors/landgate-problem-types.yml`.

## Boundaries of this skill

- The subscription host `services.slip.wa.gov.au/arcgis/rest/services` returns HTTP 401
  anonymously. Do not attempt it without a signed SLIP licence.
- Titles, tenure, ownership, sales evidence and valuations are **not** on this surface.
- Licensing for the data is not implied by the openness of the endpoint — check the matching
  dataset in `data.wa.gov.au` and the Landgate licensing page.
