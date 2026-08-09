# Repository instructions

## Content link paths

These rules apply to every document under `./content`.

- Use Markdown links in the form `[label](target)` for all internal document links.
- Do not use wiki link syntax (`[[target|label]]` or `[[target]]`).
- Treat `./content` as the root directory for every internal document link.
- Write the target's full path relative to `./content`, regardless of the source document's location.
- Do not include the `content/` prefix in the link target.
- Do not use a basename-only link, a shortest-path link, or a path relative to the current document.
- Omit the `.md` extension from Quartz internal links.
- If the target is an `index.md` file, omit `index.md` and use the full path of its containing directory.
- Do not create a placeholder document only to satisfy a link unless the user explicitly requests it.

Examples:

- `content/03_Resource/04_network/index.md`
  - Markdown: `[Network](03_Resource/04_network)`
- `content/03_Resource/04_network/01_tcp.md`
  - Markdown: `[TCP/IP와 연결](03_Resource/04_network/01_tcp)`
- `content/03_Resource/04_network/02_tcpip_ts.md`
  - Markdown: `[TCP 연결 장애 사례](03_Resource/04_network/02_tcpip_ts)`

Do not write links in these forms:

- `[TCP](01_tcp)`
- `[Index](index)`
- `[TCP](../01_tcp)`
- `[Network](content/03_Resource/04_network/index.md)`

Before finishing a content edit, resolve each newly added or changed internal link from `./content` and confirm that an `index.md` target uses its directory path.

## Slash usage in content

These rules apply to every document under `./content`.

- Do not use `/` as a separator or conjunction between terms in prose, headings, link labels, tables, diagrams, or comments.
- Use a natural conjunction such as `와`, `과`, `및`, `또는`, or a comma instead.
- Preserve `/` when it is intrinsic to an established technical notation such as `TCP/IP`, `HTTP/2`, or `I/O`.
- Preserve `/` in URLs, file paths, command arguments, media types, source code, and mathematical expressions.
- Before finishing a content edit, check changed text for separator-style slash usage and replace it unless one of the exceptions applies.
