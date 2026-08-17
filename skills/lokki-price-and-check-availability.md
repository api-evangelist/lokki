---
name: Price a rental and check availability for a date range
description: Retrieve a store's items with real prices and real stock for a specific rental window, using the from/to parameters that change what pricing and stock actually mean.
api: openapi/lokki-external-api-openapi.json
operations:
  - external__getOneStore
  - external__getManyStoreItems
  - external__getOneStoreItem
generated: '2026-08-17'
method: generated
source: >-
  Grounded in operationIds verified verbatim in openapi/lokki-external-api-openapi.json, the pricing and
  stock semantics documented at https://docs.getlokki.com/api-reference/store-items/about, and
  conventions/lokki-conventions.yml.
---

# Price a rental and check availability for a date range

This is the flow that gets it wrong most often, because the same fields mean different things
depending on whether you sent a date range.

## The one rule

`from` and `to` are optional parameters that change the **semantics** of the response, not just its
values:

| Field | Without `from`/`to` | With `from`/`to` |
|---|---|---|
| `pricing.basis` | `LOWEST_PRICE` | `RANGE_COMPUTED` |
| `pricing.price` | "starting from" — the lowest price available on any duration | the price for the requested window |
| `stock.availableQuantity` | maximum theoretical stock | real availability for the requested window |

If you are showing a booking, always send both. If you are showing a "from €X/day" teaser, omit them
and label it as such. Check `pricing.basis` before you render a number.

## Steps

1. **Resolve the store.** Call `external__getOneStore` — `GET /v2/external/stores/{id}` — with an
   ObjectId or a slug. Use `fields` to keep it small, and read `pricing.currency` (ISO code + symbol),
   `temporal.timezone`, and `booking` (instant booking, lead time, fixed durations) — those constrain
   which windows are even bookable.

   If the store has multiple rental points, pass `rentalPointSlug` semantics through `geo.locations`
   and pick the point you are pricing.

2. **List priced items for the window.** Call `external__getManyStoreItems` —
   `GET /v2/external/stores/{slug}/items` — with `from`, `to`, `lang`, and optionally `verticale`,
   `verticaleCategoryIds`, `ids`, `sortBy`, `limit`, `skip`, `fields`.

   Note the path takes the store **slug**, not its id.

3. **Read each item correctly.**
   - `type`: `product` (limited stock) or `service` (unlimited stock — insurance, delivery, and similar
     add-ons come back through this same list).
   - `rentalType`: `LCD` for short-term (hourly/daily), `LLD` for long-term (monthly). Do not mix them
     in one basket without saying so.
   - `pricing`: `price`, `basePrice`, `discount`, `deposit`, `vat`, `pricingTable`. `basePrice` is
     pre-discount; `price` is what the customer pays.
   - `time`: `duration` (min/max allowed) and `ranges` (predefined windows with their own prices).
     Validate the requested window against these before quoting.
   - `stock`: `availableQuantity` vs `totalQuantity`.
   - `modules`: optional features such as insurance, when enabled for the item.

4. **Fetch one item when you need everything.** Call `external__getOneStoreItem` —
   `GET /v2/external/stores/{slug}/items/{itemId}` — with the same `from`/`to`. Use it on the detail
   page rather than over-fetching the list.

5. **Respect the deposit.** `pricing.deposit` is the security deposit the provider takes; it is a
   separate amount from `price` and must be surfaced, not folded in.

## Failure modes

| Status | Meaning | Do this |
|---|---|---|
| 401 | Missing/invalid token, or wrong header name (`x-api-key`) | Fix the header; check the environment key prefix |
| 403 | Key lacks the `items` domain / `read` action scope | Ask your Lokki representative to widen the scope |
| 404 | Unknown store slug or item id | Re-resolve the slug from `external__getManyStores` |
| 400 | Unparsable `from`/`to`, or an out-of-range `limit`/`skip` | `message` is an array of validation strings |

## Notes

- Prices are quoted in the store's currency (`pricing.currency`), which is per-store — do not assume EUR
  across a multi-country result set.
- Nothing here books anything. There is no write surface on the partner API: no order, cart, customer or
  payment operation exists. Booking lives in Lokki's internal Dashboard API, which is not a partner
  product. See `data-model/lokki-data-model.yml`.
- The partner API is read-only, so every call is safe to retry; there is no idempotency key and none is
  needed.
