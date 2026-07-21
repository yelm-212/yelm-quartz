# Repository instructions

## Content link paths

These rules apply to every document under `./content`.

- Treat `./content` as the root directory for every internal document link.
- Write the target's full path relative to `./content`, regardless of the source document's location.
- Do not include the `content/` prefix in the link target.
- Do not use a basename-only link, a shortest-path link, or a path relative to the current document.
- Omit the `.md` extension from Quartz internal links.
- If the target is an `index.md` file, omit `index.md` and use the full path of its containing directory.
- Do not create a placeholder document only to satisfy a link unless the user explicitly requests it.

Examples:

- `content/03_Resource/04_network/01_tcp/index.md`
  - Markdown: `[TCP/IP와 연결](03_Resource/04_network/01_tcp)`
  - Wiki link: `[[03_Resource/04_network/01_tcp|TCP/IP와 연결]]`
- `content/03_Resource/04_network/01_tcp/troubleshooting.md`
  - Markdown: `[TCP 연결 장애 사례](03_Resource/04_network/01_tcp/troubleshooting)`
  - Wiki link: `[[03_Resource/04_network/01_tcp/troubleshooting|TCP 연결 장애 사례]]`

Do not write links in these forms:

- `[[01_tcp]]`
- `[[index]]`
- `[[../01_tcp]]`
- `[[content/03_Resource/04_network/01_tcp/index.md]]`

Before finishing a content edit, resolve each newly added or changed internal link from `./content` and confirm that an `index.md` target uses its directory path.
