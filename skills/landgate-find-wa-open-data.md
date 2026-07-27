---
name: Find Western Australian open data through Data WA
description: Search the WA whole-of-government open data catalogue that Landgate operates,
  find the datasets a question needs, and check their licence before using them.
api: openapi/landgate-data-wa-ckan-openapi.yml
operations:
  - ckanPackageSearch
  - ckanPackageShow
  - ckanOrganizationShow
  - ckanLicenseList
  - ckanResourceSearch
  - ckanHelpShow
generated: '2026-07-26'
method: generated
source: openapi/landgate-data-wa-ckan-openapi.yml (operations verified live 2026-07-26)
---

# Find WA open data through Data WA

Landgate operates `data.wa.gov.au` for the whole WA public sector. Its CKAN Action API is
anonymous and read-only. Base URL: `https://catalogue.data.wa.gov.au`.

## Authentication

None. Do not send an Authorization header — read actions are open, and no public API key is
issued. See `authentication/landgate-authentication.yml`.

## Steps

1. **Search the catalogue.** Call `ckanPackageSearch`
   (`GET /api/3/action/package_search`) with `q` for free text and `rows`/`start` for
   pagination (default 10, maximum 1000). To restrict to Landgate's own publishing, add
   `fq=organization:landgate` — 395 of the 2,872 datasets on 2026-07-26.
2. **Read the envelope, not the status alone.** Every response is
   `{"help": "...", "success": true|false, "result": ...}`. Treat `success: false` as failure
   even on a 200.
3. **Open the dataset.** Call `ckanPackageShow` with `id` set to the `name` or `id` from the
   search hit. The result carries `resources[]` — the actual files and service URLs.
4. **Check the licence before you use anything.** Read `license_id` on the package and resolve
   it with `ckanLicenseList`. Do not assume open: 371 of Landgate's 395 datasets are
   `license_id: custom_other`, a Landgate licence with conditions. Only 2 are public domain
   and 5 are CC non-commercial.
5. **Expect gated resources.** A `resources[].url` may point at
   `services.slip.wa.gov.au/arcgis/...`, which returns HTTP 401 anonymously. A catalogued
   resource is not necessarily a reachable one. If you get a 401, the dataset needs a signed
   SLIP licence — report that rather than retrying.
6. **Search distributions directly** when you want a format rather than a topic: call
   `ckanResourceSearch` with e.g. `query=name:cadastre`.
7. **When unsure of a parameter**, call `ckanHelpShow` with `name=<action>` — CKAN returns its
   own parameter reference. This is the only parameter documentation that exists.

## Error handling

- `409` with `{"error": {"<field>": ["Missing value"], "__type": "Validation Error"}}` — a
  required parameter is missing.
- `400` with a bare JSON string `"Bad request - Action name not known: ..."` — the action does
  not exist on this deployment.
- **Soft-404 trap:** any unknown path on `catalogue.data.wa.gov.au` returns HTTP 200 with a
  20,499-byte `text/html` page. Check `content-type` before parsing.

See `errors/landgate-problem-types.yml` and `conventions/landgate-conventions.yml`.

## Idempotency and rate limits

There is no idempotency contract (the surface is read-only) and no published rate limit or
rate-limit header. Be conservative: page with `rows`/`start` rather than pulling large result
sets at once.
