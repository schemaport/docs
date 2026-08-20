# SchemaPort documentation

The unified documentation site for [SchemaPort](https://github.com/schemaport),
built with the open-source [Thally](https://docs.thally.app) runtime.

SchemaPort lets you define an AI tool schema once and use it safely across
OpenAI, Anthropic, Gemini and MCP. The product is built across six independent
repositories; this site documents them as one product.

## Run locally

```bash
npm install
npm run dev
```

Open [http://localhost:3040](http://localhost:3040).

## Validate

```bash
npx thally check    # content, navigation, links
npm test
npm run build
```

`thally check` reports broken links and orphaned pages. Treat both as errors.

## What you edit

| Path | Purpose |
| --- | --- |
| `src/content/**/*.mdx` | Pages. The file path becomes the URL. |
| `docs.json` | Navigation tabs and groups, navbar, footer. |
| `src/data/site.ts` | Product identity, description, links, branding. |
| `public/` | Images, logos, favicons. |

Everything else is the Thally runtime, generated as a pinned snapshot and
tracked in `starter-release.json`. Do not hand-edit runtime-owned paths.

## Documentation ownership

Each page describes behaviour owned by one of the six source repositories.
When source behaviour changes, the corresponding pages must change with it.

| Repository | Documents |
| --- | --- |
| [`core`](https://github.com/schemaport/core) | `/concepts/*`, `/reference/tool-format`, `/reference/diagnostics` |
| [`cli`](https://github.com/schemaport/cli) | `/commands/*`, `/reference/configuration`, `/reference/exit-codes`, `/reference/manifest`, `/guides/*` |
| [`provider-openai`](https://github.com/schemaport/provider-openai) | `/providers/openai` |
| [`provider-anthropic`](https://github.com/schemaport/provider-anthropic) | `/providers/anthropic` |
| [`provider-gemini`](https://github.com/schemaport/provider-gemini) | `/providers/gemini` |
| [`provider-mcp`](https://github.com/schemaport/provider-mcp) | `/providers/mcp` |

`/providers/compatibility-matrix` and `/changelog` aggregate all six.

## Writing

See [`AGENTS.md`](AGENTS.md) for the content model, canonical terminology, and
the accuracy rules that apply to this product — in particular that
documentation must never describe behaviour the source repositories do not
implement, and must never imply a live provider API result was observed.

## License

MIT
