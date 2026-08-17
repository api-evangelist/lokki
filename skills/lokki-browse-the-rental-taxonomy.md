---
name: Browse the rental taxonomy and filter by sector
description: Load Lokki's two-level verticale/category taxonomy and use it to filter stores and items precisely, instead of guessing at free-text search that the API does not offer.
api: openapi/lokki-external-api-openapi.json
operations:
  - external__getManyVerticales
  - external__getManyCategories
  - external__getManyStoreItems
generated: '2026-08-17'
method: generated
source: >-
  Grounded in operationIds verified verbatim in openapi/lokki-external-api-openapi.json and the
  taxonomy documented at https://docs.getlokki.com/api-reference/categories/about.
---

# Browse the rental taxonomy and filter by sector

Lokki has no keyword search. Every precise query goes through the taxonomy, so load it once and cache
it.

## The two levels

- **Verticale** — the broad sector. A fixed 16-value enum, not a database id:
  `BIKE`, `ELECTRIC_BIKE`, `MOPED`, `MOTORCYCLE`, `CAR`, `SCOOTER`, `SKI`, `CLIMBING`, `SNOWSHOES`,
  `SURF`, `PADDLE`, `CANOE_KAYAK`, `BOAT`, `EVENT`, `MOTOCULTURE`, `TOOLING`.
- **Category** — the specific type inside a verticale (Mountain Bike, Road Bike, City Bike under
  `BIKE`). An ObjectId, so it must be fetched, never hardcoded.

Confusing the two is the most common filtering mistake: `verticale=BIKE` is a sector,
`verticaleCategoryIds=<id>` is a product type.

## Steps

1. **Load the verticales.** Call `external__getManyVerticales` — `GET /v2/external/verticales` — with
   `lang`. Each entry is `{ id, infos }` where `id` is the enum value and `infos` carries the localized
   `name` and `description`. Render `infos.name`, filter on `id`.

2. **Load the categories.** Call `external__getManyCategories` —
   `GET /v2/external/verticales/categories` — with `lang`, and narrow with `verticale.equals` or
   `verticale.in`. The envelope is `{ total, docs }`; also accepts `limit`, `skip`, `sort`, `fields`,
   `verticale.notEquals` and `verticale.notIn`.

   Each category is `{ id, infos: { name, verticale }, meta: { isOptions, isDefault } }`. `meta.isOptions`
   marks a category used for add-on options rather than primary inventory — exclude it from a browse
   grid. `meta.isDefault` marks the fallback category for its verticale.

3. **Cache it.** The verticale list is an enum in the spec and the category list changes rarely. There is
   no changelog and no event feed to tell you when it moves, so refresh on a schedule rather than per
   request.

4. **Apply it.** Pass `verticale` and `verticaleCategoryIds` to `external__getManyStoreItems`
   (`GET /v2/external/stores/{slug}/items`) to filter inventory. For stores, use the operator forms —
   `verticale.equals`, `verticale.in` — on `external__getManyStores`; store-level filtering is by
   verticale only, because a store's `profile.verticales` is a list of sectors, not categories.

5. **Localize once.** `lang` accepts `fr`, `en`, `nl`, `de`, `it`, `pt`, `es`, `pl` and defaults to `fr`.
   Cache the taxonomy per language, since `infos.name` is what changes.

## Failure modes

| Status | Meaning | Do this |
|---|---|---|
| 401 | Missing/invalid token, or wrong header name (`x-api-key`) | Fix the header |
| 403 | Key lacks the required domain/action/route scope | Ask your Lokki representative to widen the scope |

## Notes

- `verticale` values are stable enum members in the published spec, so they are safe to switch on in code.
  Category ids are not — always resolve them.
- The categories operation lives under `/v2/external/verticales/categories`, not `/v2/external/categories`,
  even though the documentation page is titled "Get Categories".
