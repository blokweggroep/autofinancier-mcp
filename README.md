# DeAutofinancier Vehicle Search MCP

**MCP server for searching the used vehicle inventory of De Autofinancier (The Netherlands).**

- **Endpoint:** `https://mcp.deautofinancier.nl/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** None required
- **Protocol:** [Model Context Protocol](https://modelcontextprotocol.io)

Search approximately 97,000 second-hand vehicles listed by affiliated car
dealers across the Netherlands, including asking prices and monthly payment
estimates for consumer finance and financial lease.

## Tools

### `search_vehicles`

Search the vehicle inventory. All filters are optional and freely
combinable. Filter values are lowercase English codes.

Key filters (19 total):

| Filter | Example values |
|---|---|
| `make`, `model` | `kia`, `e-niro` |
| `fuelType` | `electricity`, `hybrid`, `petrol`, `diesel` |
| `color` | `blue`, `black`, `white` |
| `bodyType` | `suv`, `stationwagon`, `sedan` |
| `priceMin` / `priceMax` | EUR amounts |
| `monthlyPaymentMax` | maximum monthly payment in EUR |
| `financeProduct` | `consumer-finance`, `financial-lease` |
| `sort` | `price-asc`, `monthly-payment-asc`, `year-desc`, ... |

Full parameter descriptions, including all valid values, are provided in the
tool's input schema.

### `list_filter_values`

Returns all valid filter values (makes, models, colors, fuel types, etc.)
from the official taxonomy.

## Usage notes for AI agents

1. **Call `list_filter_values` first** if you are not certain which code a
   make, model or filter value has. The search API silently ignores unknown
   values — an invalid filter may cause the full inventory to be returned.
2. **Kia Niro naming:** the electric Niro is `e-niro` (model years up to 2023)
   and `niro` (2023 onwards, "Niro EV"). For recent electric Niros, combine
   `model=niro` with `fuelType=electricity`.
3. Multiple values per filter are comma-separated: `make=audi,bmw`.

## Example call

```json
{
  "make": "kia",
  "model": "niro",
  "color": "blue",
  "fuelType": "electricity",
  "odometerMax": 60000
}
```

Returns matching vehicles with year, mileage, price, monthly payment
estimates and a direct link to the listing.

## Related resources

- [Website](https://www.deautofinancier.nl)
- [llms.txt](https://www.deautofinancier.nl/llms.txt) — documentation for AI agents
- [OpenAPI 3.1 specification](https://www.deautofinancier.nl/api/openapi.json) — the underlying HTTP API
- [Vehicle taxonomy](https://www.deautofinancier.nl/.well-known/vehicle-taxonomy) — all valid filter values

## About

This repository publishes the [server.json](./server.json) manifest for the
official MCP Registry. The server is hosted by
[De Autofinancier](https://www.deautofinancier.nl); source code is not part
of this repository.

---

*MCP server — DeAutofinancier Vehicle Search — De Autofinancier, Netherlands*
