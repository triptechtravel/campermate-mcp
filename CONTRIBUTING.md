# Contributing

This repo is documentation for the [CamperMate MCP](https://campermate.com), a hosted Model Context Protocol server. The server itself is closed source — there's nothing to compile or run locally.

## We welcome issues for

- **Bug reports** — wrong tool output, broken behaviour, or incorrect responses
- **Feature requests** — new tools, resources, or guides
- **Integration help** — when you're stuck wiring it into Claude Desktop, Cursor, Windsurf, or another MCP client
- **Documentation fixes** — clarifications, typos, install issues (PRs to the README are welcome)

## We don't accept

- **Source-code PRs** — the server isn't in this repo and isn't public
- **POI data corrections** — for "this campsite's hours are wrong" or "this attraction has closed", use the CamperMate app's POI report flow or [contact form](https://campermate.com/contact) — those flow into the editorial pipeline. Issues here won't reach the data team.

## What makes a good bug report

- **MCP client** you're using (Claude Desktop, Cursor, Windsurf, etc.) and version
- **Tool called** (e.g. `search_pois`, `get_poi`) and the arguments
- **Expected** vs **actual** behaviour
- The **request id** from the response, if your client surfaces it
- A **minimal prompt** that reproduces the issue, where applicable

The issue template will guide you through these.

## Triage

We aim to triage issues within a few business days. The MCP runs on Cloudflare Workers and most fixes ship the same day they're identified.
