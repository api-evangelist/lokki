---
name: Lokki
description: Use when building integrations with rental providers, querying store information, retrieving rental items and pricing, filtering by categories and sectors, or managing rental marketplace data. Agents should reach for this skill when working with rental provider APIs, building search/discovery features, or integrating rental inventory systems.
metadata:
    mintlify-proj: lokki
    version: "1.0"
---

# Lokki Skill Reference

## Product summary

Lokki is a REST API for accessing rental provider data, inventory, and pricing. Use it to query stores (rental providers), their items (products/services), categories, and availability across rental sectors like bikes, cars, boats, and equipment. The API uses standard HTTP methods, JSON payloads, and requires API key authentication via the `x-api-key` header. Base URLs: Staging (`https://staging.api.eu-west-3.lokki.rent/`) and Production (`https://prod.api.eu-west-3.lokki.rent/`). Primary docs: https://docs.getlokki.com

## When to use

Reach for this skill when:
- Building integrations with rental marketplaces or provider networks
- Querying store information (locations, hours, reviews, booking rules)
- Retrieving rental items with pricing and availability for specific date ranges
- Filtering stores or items by verticale (sector) or category
- Implementing search/discovery features for rental products
- Handling deprecation migrations from flat to modular data structures
- Troubleshooting authentication or scope errors (401/403 responses)

## Quick reference

### Authentication
All requests require the `x-api-key` header with an access token. Tokens are environment-specific:
- Staging: `lokki_sk_test_...`
- Production: `lokki_sk_live_...`

### Core endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/v2/external/stores` | GET | List stores with filtering, sorting, pagination |
| `/v2/external/stores/{id}` | GET | Get one store by ID or slug |
| `/v2/external/stores/{slug}/items` | GET | Get items for a store |
| `/v2/external/stores/{slug}/items/{id}` | GET | Get one item from a store |
| `/v2/external/verticales` | GET | List all top-level sectors (BIKE, CAR, etc.) |
| `/v2/external/categories` | GET | List categories within a verticale |

### Common query parameters

| Parameter | Type | Purpose | Example |
|-----------|------|---------|---------|
| `lang` | string | Response language (fr, en, nl, de, it, pt, es, pl) | `en` |
| `from` | date | Rental start date (required for accurate pricing/stock) | `2024-01-15` |
| `to` | date | Rental end date (required for accurate pricing/stock) | `2024-01-20` |
| `verticale` | string | Filter by sector | `BIKE` |
| `verticaleCategoryIds` | string[] | Filter by category IDs | `mountain-bike,electric-bike` |
| `lat`, `lng` | float | Geographic coordinates for location filtering | `48.8566, 2.3522` |
| `limit`, `offset` | int | Pagination controls | `limit=20&offset=0` |

### Verticales (sectors)
BIKE, ELECTRIC_BIKE, MOPED, MOTORCYCLE, CAR, SCOOTER, SKI, CLIMBING, SNOWSHOES, SURF, PADDLE, CANOE_KAYAK, BOAT, EVENT, MOTOCULTURE, TOOLING

### Store data structure (modular)
- `profile`: name, description, verticales
- `branding`: logoURL, banners
- `geo`: location (address, lat/lng, placeId), locations (all rental points)
- `temporal`: timezone, schedule (hours, low season, closed ranges)
- `pricing`: currency, tax settings, discounts
- `reviews`: Google ratings and comments
- `booking`: instantBooking, leadTime, fixedDurations
- `modules`: delivery, insurance, cancellation policies

### Store item data structure
- `infos`: localized name and description
- `media`: images, videos, documents
- `pricing`: price, basePrice, appliedDiscounts, basis (LOWEST_PRICE or RANGE_COMPUTED)
- `stock`: quantity available for selected period
- `time`: min/max rental duration, predefined time ranges
- `modules`: optional features (insurance, etc.)

## Decision guidance

| Scenario | Use | Reason |
|----------|-----|--------|
| Need store details | `/v2/external/stores/{id}` | Single store with full modular data |
| Building search/filter | `/v2/external/stores` with filters | Supports location, verticale, pagination |
| Getting accurate pricing | Include `from`/`to` dates | Without dates, returns "starting from" price only |
| Getting actual stock | Include `from`/`to` dates | Without dates, shows theoretical max stock |
| Filtering items by type | Use `verticale` + `verticaleCategoryIds` | Verticale is broad (BIKE), categories are specific (Mountain Bike) |
| Migrating old integration | Use new modular paths | Old flat fields (name, address, etc.) are deprecated |
| Handling 403 errors | Check token scopes | Token may lack domain/action/route permissions |

## Workflow

1. **Obtain credentials**: Contact your Lokki representative for API keys (separate tokens for Staging and Production).

2. **Set up authentication**: Store tokens in environment variables. Never expose in client-side code or public repos.

3. **Understand the data model**: Review the modular structure (profile, geo, branding, etc.). If working with existing code, check for deprecated flat fields and plan migration.

4. **Query stores**: Call `/v2/external/stores` with filters (location, verticale, pagination). Use `slug` from response for item queries.

5. **Fetch items for a store**: Call `/v2/external/stores/{slug}/items` with `from`/`to` dates for accurate pricing and stock. Include `lang` for localization.

6. **Filter by category**: Call `/v2/external/verticales` and `/v2/external/categories` first to get IDs, then use `verticaleCategoryIds` in item queries.

7. **Handle responses**: Parse modular structure (e.g., `response.profile.name` not `response.name`). Check `pricing.basis` to understand if price is lowest available or date-specific.

8. **Test in Staging**: Verify all queries and response parsing before moving to Production.

## Common gotchas

- **Missing `from`/`to` dates**: Pricing returns "starting from" (lowest available), and stock shows theoretical max, not actual availability. Always include date range for bookings.
- **Using deprecated fields**: Old flat fields like `name`, `address`, `logoURL` still work but will be removed. Use modular paths: `profile.name`, `geo.location.address`, `branding.logoURL`.
- **Wrong header name**: Must be `x-api-key`, not `x-api-token` or `Authorization`. Incorrect header returns 401.
- **Token scope errors**: 403 Forbidden means your token lacks permissions for that endpoint. Check domain (stores, items), action (read, write), and route (GET, POST) scopes with your Lokki representative.
- **Environment token mismatch**: Staging tokens (`lokki_sk_test_...`) don't work on Production and vice versa. Use correct token for environment.
- **Language parameter**: Defaults to French (`fr`). Explicitly set `lang=en` or other codes for different languages.
- **Pagination**: Default limit may be low. Always specify `limit` and `offset` for large result sets.
- **Verticale vs Category confusion**: Verticale is the broad sector (BIKE), Category is the specific type (Mountain Bike). Use both for precise filtering.
- **Stock without dates**: Shows max theoretical stock, not actual availability for your rental period. Always include `from`/`to`.

## Verification checklist

Before submitting work:

- [ ] API key is stored in environment variables, not hardcoded
- [ ] Correct header name used: `x-api-key`
- [ ] Token matches environment (Staging vs Production)
- [ ] All item queries include `from` and `to` date parameters
- [ ] Using modular data paths (e.g., `profile.name`, not `name`)
- [ ] Language parameter set explicitly if non-French output needed
- [ ] Pagination parameters included for large result sets
- [ ] Error handling covers 401 (auth), 403 (scope), and 404 (not found)
- [ ] Tested in Staging before Production deployment
- [ ] Response parsing handles nested modular structure correctly

## Resources

- **Comprehensive navigation**: https://docs.getlokki.com/llms.txt
- **API Getting Started**: https://docs.getlokki.com/api-reference/getting-started
- **Authentication Guide**: https://docs.getlokki.com/api-reference/authentication
- **Stores API**: https://docs.getlokki.com/api-reference/stores/about
- **Store Items API**: https://docs.getlokki.com/api-reference/store-items/about
- **Categories & Verticales**: https://docs.getlokki.com/api-reference/categories/about
- **Deprecation Guide**: https://docs.getlokki.com/api-reference/stores/deprecations

---

> For additional documentation and navigation, see: https://docs.getlokki.com/llms.txt