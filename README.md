# CamperMate MCP

The Model Context Protocol server for [CamperMate](https://campermate.com) — Australia and New Zealand's leading travel app for campers, caravanners, and road-trippers.

Gives MCP-compatible AI assistants (Claude Desktop, Cursor, Windsurf, etc.) access to thousands of campsites, freedom camps, walking trails, scenic spots, and tourist attractions across AU/NZ — with reviews, ratings, deals, and tracked booking links.

## Endpoint

```
https://mcp.campermate.com/mcp
```

Transport: Streamable HTTP (stateless). Protocol version: `2025-06-18`. No auth required. Rate limit: 60 requests/minute per IP.

Server info: <https://mcp.campermate.com/.well-known/mcp-info>

## Install

### Claude Desktop

Add to `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{
  "mcpServers": {
    "campermate": {
      "type": "http",
      "url": "https://mcp.campermate.com/mcp"
    }
  }
}
```

If your client doesn't support HTTP transport directly, use `mcp-remote` as a bridge:

```json
{
  "mcpServers": {
    "campermate": {
      "command": "npx",
      "args": ["mcp-remote", "https://mcp.campermate.com/mcp"]
    }
  }
}
```

### Other clients

Any MCP client that speaks Streamable HTTP — Cursor, Windsurf, Continue, custom agents — can point at the endpoint above. Consult your client's docs for the exact config shape.

## Tools

| Tool | What it does |
| --- | --- |
| `search_pois` | Search POIs by text, geo (lat/lng + radius), category, features, bookability, deals, ratings, price. |
| `get_poi` | Full detail for a POI by uuid — description, pricing, amenities, hours, contact, social, reviews. |
| `find_nearby` | Find POIs near a given POI — e.g. dump stations, supermarkets, attractions near a campsite. |
| `compare_pois` | Side-by-side comparison of 2–5 POIs by uuid. |
| `list_categories` | All POI categories with counts, grouped by parent category. |
| `list_features` | All amenities/features (Wi-Fi, pet-friendly, etc.) with counts. |
| `list_regions` | Tourism regions with counts — maps fuzzy input ("South Island", "Tasmania") to concrete regions. |

## Resources

- `campermate://categories` — POI category taxonomy
- `campermate://features` — amenity taxonomy
- `campermate://regions/nz` — NZ tourism regions
- `campermate://regions/au` — AU tourism regions
- `campermate://guide/freedom-camping` — rules and etiquette for freedom camping in AU/NZ
- `campermate://about` — what CamperMate covers and what this MCP exposes vs. app-only features

## Prompts

- `plan_camping_trip` — multi-stop trip planner (destination, days, vehicle, budget)
- `find_freedom_camping` — discover free/freedom camping along a route or near a location

## Example queries

Once installed, try asking your assistant:

- "Plan me a 5-night campervan trip from Auckland to Wellington with a moderate budget."
- "Find paid campsites near Byron Bay with at least a 4-star rating."
- "What walking trails are within 20km of Lake Tekapo?"
- "Compare the top three freedom camping spots on the Coromandel."
- "I'm self-contained — where can I freedom-camp near Queenstown tonight?"
- "Show me scenic spots and tourist attractions along the Great Ocean Road."

## Scope

Covers Australia and New Zealand. Categories accessible via MCP:

- **Accommodation** — paid campsites (including holiday parks) and free/freedom campsites
- **Activities** — tourist attractions, scenic spots, scenic flights, walking and hiking, water activities, cultural places, museums, food & beverage
- **Deals and bookings** from partner operators

Not exposed via MCP (app-only): amenity POIs (dump stations, potable water, toilets, supermarkets, bakeries, fuel), live availability, offline maps, trip save, full-resolution community photos, real-time deal updates. The MCP responses include tracked links to the CamperMate iOS and Android apps for users who want the full experience.

## Attribution and privacy

- No PII is collected. The server logs the user-agent string for analytics only.
- Tool responses include tracked short URLs (`link`, `booking_link`) that record clicks for attribution. Users see a normal CamperMate destination URL after redirect.
- Booking links to partner sites are tagged with `user_id=anonymous_mcp` and the POI id.

## Support

- App store listings: [iOS](https://apps.apple.com/au/app/campermate-australia-nz/id465040067) · [Android](https://play.google.com/store/apps/details?id=nz.co.campermate)
- Website: <https://campermate.com>
- Issues: file an issue on this repo

## License

MIT
