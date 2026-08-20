# Documentation project instructions

## Repository role

This repository is the unified documentation site for **SchemaPort**, published
with Thally. SchemaPort itself is not built here — it lives in six independent
repositories under the [`schemaport`](https://github.com/schemaport)
organisation. This site assembles them into one product.

| Repository | Owns |
| --- | --- |
| [`core`](https://github.com/schemaport/core) | Canonical tool format, loading, diagnostics, compile policy, diff engine |
| [`cli`](https://github.com/schemaport/cli) | The four commands, flags, output formats, exit codes, configuration |
| [`provider-openai`](https://github.com/schemaport/provider-openai) | OpenAI rules, transformations, probing |
| [`provider-anthropic`](https://github.com/schemaport/provider-anthropic) | Anthropic rules, transformations, probing |
| [`provider-gemini`](https://github.com/schemaport/provider-gemini) | Gemini rules, transformations, probing |
| [`provider-mcp`](https://github.com/schemaport/provider-mcp) | MCP rules, compilation, local validation |

**Never document behaviour that is not implemented in those repositories.**
When a source repository changes, the pages that describe it must change with
it. A new compatibility rule in `provider-openai`, for example, affects
`/providers/openai`, `/providers/compatibility-matrix`,
`/reference/diagnostics`, and `/changelog`.

Runtime-owned files in this repository are a generated Thally snapshot, not a
second implementation. Never hand-apply a runtime fix here. Run the **Sync
Thally runtime** workflow, review its generated pull request, and let CI prove
that the snapshot matches the exact runtime commit in `starter-release.json`.

## Project boundaries

- Pages are MDX files in `src/content/`.
- Navigation and portable product features are configured in `docs.json`.
- Site identity and versioned brand defaults live in `src/data/site.ts`.
- `starter-release.json` and runtime-owned paths listed in it are
  machine-managed; do not hand-edit them.
- Runtime changes belong in `thallylabs/thally` and arrive here only through
  the generated synchronization pull request.
- Never place credentials in source files. Use `.env.local` locally and secret
  storage in the deployment platform.

## Writing standards

- Address the reader as “you” and use active voice.
- Lead with the outcome, then state prerequisites and the shortest working path.
- Use sentence-case headings and concise paragraphs.
- Format commands, files, configuration keys, and code with backticks.
- Tell readers what success looks like and link the next useful task.
- Keep advanced or optional paths outside the primary workflow.

## Content model

- Every page needs `title` and `description` frontmatter.
- Keep page slugs stable once published.
- Add pages to `docs.json`; do not leave useful pages orphaned.
- Update `openapi.yaml` when API behavior changes.
- Run `npm ci --ignore-scripts --prefix .github/thally-tooling`, then
  `.github/thally-tooling/node_modules/.bin/thally check --ci .`, `npm test`,
  and `npm run build` before publishing.

## Product context

SchemaPort lets a developer define an AI tool schema once and use it across
OpenAI, Anthropic, Gemini and MCP. It is a local-first CLI with four commands:
`check`, `compile`, `probe` and `diff`.

### Canonical terminology

- **Canonical tool** — the single source schema, in SchemaPort's format
  (`name`, `description`, `inputSchema`). Never "source schema" or "input tool".
- **Target** / **provider** — one of `openai`, `anthropic`, `gemini`, `mcp`.
- **Transformation** — one recorded change compile made, carrying `lossy: true`
  or `lossy: false`.
- **Lossy** — the compiled schema accepts inputs the canonical schema rejects,
  because a constraint was dropped. Refused unless `--allow-lossy`.
- **Diagnostic** — one finding from `check`, with a severity and a namespaced
  code such as `openai/strict-optional-property`.

### Content boundaries

- Diagnostic codes, transformation codes, flags and exit codes are the stable
  interface. Quote them exactly; verify against the source repositories.
- **No live provider API call has been run.** Probe is fully implemented and
  tested against mocked SDK clients, but no API keys have ever been present.
  Documentation must never imply a live result was observed.
- Where a provider's own documentation is ambiguous, SchemaPort reports the
  uncertainty rather than resolving it. Preserve that hedging; do not "clean it
  up" into a confident claim.
- The npm packages are not yet published. Do not present
  `npm install -g schemaport` as a working install path.
- Pages carry `lastVerified` and `verifiedVersion`. Update them when you
  re-confirm a page against the product.
