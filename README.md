# Point of Sale

The common point-of-sale vocabulary -- the store locations that sell, the terminals and registers at the counter, the sales rung up on them and the shifts worked behind them -- distilled from the APIs that already exist. Products belong to the commerce context and staff to HR. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Point-of-Sale, POS, Point of Sale, Retail POS, In-Store, Payments Terminal in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| store_location | 11 | 10 | name 90%, phone 80%, address 70%, id 70%, status 70%, country 50%, currency 50%, latitude 50%, location_id 50%, longitude 50%, time_zone 50% | locations 7, stores 4, store 1, location 1 |
| terminal | 4 | 4 | id 75%, name 75% | readers 2, terminals 2, registers 1 |
| sale | 20 | 18 | id 67%, customer_id 50% | sales 9, receipts 5, transactions 3, checks 2 |
| shift | 5 | 5 | employee_id 100%, created_at 60%, id 60%, location_id 60%, updated_at 60%, version 60% | shifts 4, timecards 2, shift 1 |

Cohort: 84 providers with harvested OpenAPI, 20 crosswalks. Of the providers exposing a store_location: 64% create, 100% list, 82% fetch, 55% update, 36% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A store location agrees on name, address, phone, status, country, currency and time zone -- the most complete location core in the commons, because a POS needs every one of them to ring a sale.
- A sale agrees only on an id and the customer -- POS systems call it a sale, a transaction, a check, a ticket or an order, and carry items, taxes and tenders under as many names.
- Terminals are thin (4 providers, agreeing only on id and name); shifts (5) agree on the employee, the location and timestamps.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Store locations are `/store-locations`: `/locations` means a work site in HR and a restaurant in food ordering.
- A sale covers sales, receipts, checks and POS transactions and orders.
- A shift covers cash-drawer shifts, register closures and timecards.
- Singular `/register` is an action and does not count as a terminal.
- Products are commerce's and staff are HR's; POS does not duplicate them.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
