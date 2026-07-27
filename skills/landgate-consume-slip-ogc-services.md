---
name: Consume Landgate SLIP data through OGC WMS and WFS
description: Use the standards-based OGC surface of SLIP — WMS 1.3.0 for rendered maps and
  WFS 2.0.0 for raw features — including the service-naming rule that decides which endpoint
  answers which request.
api: openapi/landgate-slip-public-ogc-openapi.yml
operations:
  - slipWmsRequest
  - slipWfsRequest
generated: '2026-07-26'
method: generated
source: openapi/landgate-slip-public-ogc-openapi.yml (operations verified live 2026-07-26)
---

# Consume SLIP through OGC WMS / WFS

Base URL: `https://public-services.slip.wa.gov.au/public/services`
(`https://services.slip.wa.gov.au/public/services` serves the same content). Anonymous.

OGC services multiplex every operation onto one endpoint via the `request` parameter, so both
operations here are one path with an enum.

## The rule that trips everyone up

- **WMS** is served by the plain map services: `.../SLIP_Public_Services/Boundaries/MapServer/WMSServer`
- **WFS** is served by the `_WFS` siblings: `.../SLIP_Public_Services/Boundaries_WFS/MapServer/WFSServer`

Asking for WFS on a non-`_WFS` service returns HTTP 400 with an ArcGIS Server HTML error page.

## Steps — rendered maps (WMS)

1. **Get capabilities.** `slipWmsRequest` with `service=WMS&request=GetCapabilities`. The
   response is `WMS_Capabilities version="1.3.0"`; the Boundaries service advertises 56 layers.
   A verbatim copy is in this repo at `openapi/landgate-slip-public-wms-capabilities.xml`.
2. **Render.** `slipWmsRequest` with
   `service=WMS&version=1.3.0&request=GetMap&layers=<n>&styles=&crs=CRS:84&bbox=<w,s,e,n>&width=<px>&height=<px>&format=image/png`.
   Returns `image/png`. Remember WMS 1.3.0 uses `crs`, not `srs`, and axis order follows the
   CRS definition — `CRS:84` is lon/lat.

## Steps — raw features (WFS)

1. **Get capabilities** on the `_WFS` service: `service=WFS&request=GetCapabilities`. The
   Boundaries_WFS service advertises 38 feature types. Verbatim copy:
   `openapi/landgate-slip-public-wfs-capabilities.xml`.
2. **Read the type names.** They carry the custodian agency code, e.g.
   `esri:DFES_Regions__DFES-015_`, `esri:DBCA_Region_Boundaries__DBCA-022_`,
   `esri:Regional_Parks__DBCA-026_` — SLIP's public tier aggregates other WA agencies, not just
   Landgate.
3. **Describe before you fetch.** `service=WFS&version=2.0.0&request=DescribeFeatureType`
   returns an XSD schema for the feature types.
4. **Fetch features.** `service=WFS&version=2.0.0&request=GetFeature&typeNames=<type>` returns a
   GML 3.2 `wfs:FeatureCollection`.

## Size warning

**Do not rely on `count` to limit the response.** A `GetFeature` with `count=1` against
`esri:DFES_Regions__DFES-015_` returned a 1.65 MB FeatureCollection on 2026-07-26. Constrain
with `bbox` (and stream the parse) instead of assuming server-side limiting. If you need
reliable paging, use the ArcGIS REST `/query` operation with `resultOffset`/`resultRecordCount`
instead — see `skills/landgate-query-slip-boundaries.md`.

## Errors

Failures come back as an OGC `ServiceExceptionReport` / `ows:ExceptionReport` in XML, or as an
ArcGIS Server HTML error page with HTTP 400. There is no JSON error envelope on this surface.
See `errors/landgate-problem-types.yml`.
