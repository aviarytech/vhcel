# VHCEL

**Verifiable History with Cryptographic Event Log** — version 0.1, an exploratory
editor's draft authored in [ReSpec](https://respec.org/docs/).

**[Read the specification](https://aviarytech.github.io/vhcel/)**

The initial text comes from the [VHCEL design conversation](https://chatgpt.com/share/6aa6418d-191c-83e8-99c0-48a4112da4b4).
It covers the abstract history model, genesis, chaining, state transitions,
authorization, pre-rotation, witnessing, external data, verification, application
profiles, and security and privacy considerations.

Every history has a required genesis-derived SCID. Each subsequent event uses
CEL-style `previousEvent` linkage to the digest of its immediate predecessor.
Event digests are computed; no stored current-event ID or ID-substitution
procedure is required. The exact binding and cryptographic encoding remain
under development.

## Preview and edit

Requires Node.js 24 or newer and Python 3. From this directory:

```sh
npm ci
npm start
```

Open <http://127.0.0.1:8080/>. Edit `index.html` and reload the browser.
ReSpec adds section numbering, the table of contents, definitions, references,
conformance terminology, and an issue summary. The browser preview loads ReSpec
from W3C and requires internet access.

- `index.html` is the editable specification source.
- `respec-config.js` contains publication metadata and bibliography entries.
- `package-lock.json` pins the build dependency tree.
- `EDITORIAL.md` records changes made while importing the conversation.

Use nested `<section>` elements with stable IDs. ReSpec supplies section numbers,
so do not type them into headings. Use `<dfn>` for terms, `<a href="#section-id"></a>`
for automatic section references, and `<p class="issue" id="issue-topic">` for
unresolved decisions. Mark informative sections with `class="informative"`.

## Validate and export

```sh
npm run build
```

This uses the pinned local ReSpec 37.4.0 release, serves the source temporarily on port 8081,
and writes `build/index.html`. The build fails on ReSpec errors or warnings.
Installation may download a browser for ReSpec's exporter. Building can require
internet access for bibliography and styling resources.

The generated HTML needs no ReSpec processing to be read; it still references
external styles. Serve it with the same preview server at
<http://127.0.0.1:8080/build/index.html>. Do not edit generated output.

## Draft status

This is a processing-model draft, not yet a complete interoperable wire protocol.
The inline issues track the CEL binding, canonicalization and proof coverage,
SCID construction, pre-rotation, witness-policy transitions, serialization,
and compatibility tests against existing CEL and did:webvh histories.

## GitHub Pages

The [Pages workflow](.github/workflows/pages.yml) validates and exports the spec
on every push to `main`, then deploys `build/index.html` to
<https://aviarytech.github.io/vhcel/>. Pull requests run the same build without
deploying. The workflow can also be run manually from the Actions tab.

GitHub Pages uses **GitHub Actions** as its publishing source. Generated output
is uploaded as a Pages artifact and is not committed to the repository.

Editors, standards publication venue, and licensing remain provisional.
The ReSpec status is `unofficial`; the copyright placeholder deliberately makes
no W3C ownership claim or license selection.
