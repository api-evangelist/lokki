---
name: Find rental providers near a location
description: Search the Lokki network for rental providers (stores) by sector and geography, count the matches before paging through them, and resolve each store's slug for follow-on item queries.
api: openapi/lokki-external-api-openapi.json
operations:
  - external__getCountStores
  - external__getManyStores
generated: '2026-08-17'
method: generated
source: >-
  Grounded in operationIds verified verbatim in openapi/lokki-external-api-openapi.json. Conventions
  from conventions/lokki-conventions.yml; failure modes from errors/lokki-problem-types.yml.
---

# Find rental providers near a location

Lokki's partner API is read-only. This flow answers "which rental businesses in the Lokki
network rent this kind of equipment near here", and hands you the `slug` every other flow needs.

## Before you start

- Send your key in the `x-api-key` header. The published spec names `x-access-token`; the docs,
  the getting-started page and Lokki's own Agent Skill all say `x-api-key`, and a wrong header
  name returns 401. See `authentication/lokki-authentication.yml`.
- Base URL: `https://prod.api.eu-west-3.lokki.rent` (staging: `https://staging.api.eu-west-3.lokki.rent`).
  Keys do not cross environments.
- Set `lang` explicitly. The default is `fr`.

## Steps

1. **Count first.** Call `external__getCountStores` — `GET /v2/external/stores/count` — with the
   filters you intend to use. It returns only `{ total }`, so it is the cheap way to decide whether
   the filter set is worth paging.

   Filters accepted: `verticale.equals`, `verticale.in`, `verticale.notEquals`, `verticale.notIn`,
   and the geospatial triple `position.latitude`, `position.longitude`, `position.radius`.

2. **List the matches.** Call `external__getManyStores` — `GET /v2/external/stores` — with the same
   filters plus `limit`, `skip`, `sort`, `fields` and `lang`. The response envelope is
   `{ total, docs }`.

   Always set `limit` and `skip` yourself: the default page size is small and is not published.

3. **Narrow with the taxonomy, not with free text.** There is no keyword search. `verticale` is the
   broad sector (one of `BIKE`, `ELECTRIC_BIKE`, `MOPED`, `MOTORCYCLE`, `CAR`, `SCOOTER`, `SKI`,
   `CLIMBING`, `SNOWSHOES`, `SURF`, `PADDLE`, `CANOE_KAYAK`, `BOAT`, `EVENT`, `MOTOCULTURE`,
   `TOOLING`). Categories are the finer level and apply to items, not to stores — see
   `lokki-browse-the-rental-taxonomy.md`.

4. **Trim the payload.** Each store document is large — ten embedded modules. Use `fields` to project
   only what you render, for example `fields=slug,profile,geo,reviews`.

5. **Read the modular paths.** Take the name from `profile.name`, the logo from `branding.logoURL`,
   the address from `geo.location.address`, the coordinates from `geo.location.point`, and the rating
   from `reviews.google.rating`. The flat equivalents (`name`, `logoURL`, `address`, `lat`, `lng`,
   `googleRating`) still return data but are deprecated and slated for removal.

6. **Keep the `slug`.** Item queries are addressed by store slug, not by store id:
   `/v2/external/stores/{slug}/items`. `external__getOneStore` accepts either an ObjectId or a slug,
   but the item routes accept only the slug.

## Failure modes

| Status | Meaning | Do this |
|---|---|---|
| 401 | Missing/invalid token, or wrong header name | Send `x-api-key`; check the environment prefix (`lokki_sk_test_` vs `lokki_sk_live_`) |
| 403 | Key lacks the `stores` domain / `read` action / `GET` route scope | Ask your Lokki representative to widen the key scope |
| 429 | Rate limit exhausted (undocumented) | Back off until the epoch second in `x-ratelimit-reset`; there is no `Retry-After` |

An anonymous call returns 403 `{"statusCode":403,"message":"Forbidden resource","error":"Forbidden"}`,
not 401 — handle both.

## Notes

- No error responses are declared in the published spec, so a generated client will have no typed
  error models. Handle the envelope `{ statusCode, message, error }` yourself.
- There is no cursor and no `has_more`; page with `skip`/`limit` against `total`.
- There is no webhook or event feed, so store data must be polled.
