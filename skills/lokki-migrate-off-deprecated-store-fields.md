---
name: Migrate off the deprecated flat store fields
description: Move an existing Lokki integration from the pre-modular flat store fields to the modular structure, using Lokki's published mapping table, before the deprecated fields are removed.
api: openapi/lokki-external-api-openapi.json
operations:
  - external__getOneStore
  - external__getManyStores
generated: '2026-08-17'
method: generated
source: >-
  Grounded in operationIds verified verbatim in openapi/lokki-external-api-openapi.json, the 21
  properties marked deprecated:true in its Deprecated_External_Store /
  Deprecated_External_StoreCurrency / Deprecated_External_StoreAddressComponents schemas, and the
  published migration guide at https://docs.getlokki.com/api-reference/stores/deprecations.
---

# Migrate off the deprecated flat store fields

Lokki reorganized the store document from a flat field list into modules. The old fields still return
data, and Lokki says plainly they "will be removed in future versions of the API" — with no date, no
version number, and no `Sunset` header to detect it. That means the removal will arrive without a
runtime signal, so migrate on your own schedule rather than waiting for one.

## Mapping

| Deprecated field | Read this instead |
|---|---|
| `name` | `profile.name` |
| `verticales` | `profile.verticales` |
| `logoURL` | `branding.logoURL` |
| `bannerURL` | `branding.banners.urls` |
| `address` | `geo.location.address` |
| `lat` | `geo.location.point.lat` |
| `lng` | `geo.location.point.lng` |
| `addressComponents` | `geo.location.components` |
| `googleRating` | `reviews.google.rating` |
| `googleReviewsNb` | `reviews.google.total` |
| `currency` | `pricing.currency` |

The nested currency and address-component objects are deprecated too:
`Deprecated_External_StoreCurrency` (`isoName`, `symbol`) and
`Deprecated_External_StoreAddressComponents` (`administrativeAreaLevel1`, `administrativeAreaLevel2`,
`city`, `country`, `placeId`, `postalCode`, `street`, `streetNumber`) — 21 deprecated properties in
total across the three schemas.

## Steps

1. **Find your reads.** Grep your integration for the flat names above. They appear on the responses of
   `external__getOneStore` (`GET /v2/external/stores/{id}`) and `external__getManyStores`
   (`GET /v2/external/stores`) — the two operations that return the store document.

2. **Switch to modular paths.** Replace each read using the table. The modules are `profile`,
   `localization`, `contact`, `branding`, `geo`, `temporal`, `pricing`, `reviews`, `booking`, `modules`
   and `metadata`.

3. **Update your `fields` projections.** If you send `fields`, the values are field paths — a projection
   asking for `name,logoURL,address` must become `profile,branding,geo` (or the specific sub-paths).
   Missing this is why a migration silently returns empty objects.

4. **Fix your response parsing, not just your field names.** The structure changes depth: it is
   `response.profile.name`, not `response.name`. Anything that flattens the payload into a model needs
   the mapping applied in one place, not per call site.

5. **Verify against staging first.** Point at `https://staging.api.eu-west-3.lokki.rent` with a
   `lokki_sk_test_` key and diff the modular reads against the flat ones on the same store; they should
   agree today. When they diverge, the flat field has started being retired.

6. **Do not rely on the schema name.** The response schema for both operations is still called
   `Deprecated_External_Store` in the published spec. That is the current partner store document; only
   the flagged properties inside it are deprecated.

## Notes

- No `Deprecation` or `Sunset` response header is emitted (no RFC 8594), no changelog exists
  (`https://docs.getlokki.com/changelog` returns 404), and no removal version is published. The
  migration guide page is the only notice channel — watch it.
- The machine-readable form of this mapping is in `lifecycle/lokki-lifecycle.yml` and is applied to the
  spec as `x-field-mapping` in `overlays/lokki-external-api-overlay.yaml`.
