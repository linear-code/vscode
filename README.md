# Linear Code

Linear Code turns source and data files into an **interactive live graph
preview** you can zoom, pan, and search. The preview updates as you edit and
supports a compact/detailed toggle for the converted formats.

## Supported file types

| Format | Extensions | What the graph shows |
|--------|-----------|----------------------|
| **Graphviz / DOT** | `.dot`, `.gv` | The DOT source rendered via d3-graphviz (SVG). |
| **JSON** | `.json` | A node/edge graph (auto-detected `nodes[]`+`edges[]`) or the JSON walked as a tree. |
| **XML** | `.xml` | The element tree. |
| **YAML** | `.yaml`, `.yml` | The mapping/sequence tree. |
| **RDF/XML** | `.rdf` | An OWL/RDFS ontology class diagram (classes as nodes, properties as rows/edges). |
| **OWL** | `.owl` | The same ontology class diagram (RDF/XML or OWL/XML functional syntax). |
| **JavaScript / TypeScript** | `.js` `.jsx` `.ts` `.tsx` `.mjs` `.cjs` | Program structure + scope-resolved call graph (functions, classes, imports, detected resources). |
| **HTML** | `.html`, `.htm` | Page structure (container hierarchy, elements as rows, embedded JS, images, external resources). |
| **Python** | `.py`, `.pyw` | Program structure + call graph (functions, classes, DataFrames, imported modules, resources). |
| **PHP** | `.php` | Program structure + type-level relations (classes/interfaces/traits/enums, methods/properties as rows, inheritance, `new`, dependency injection, static calls, and framework/IO resources). |
| **CSV / TSV** | `.csv`, `.tsv` | Table schema plus a top-rows data preview. |
| **Parquet** | `.parquet` | Table schema and per-column statistics. |
| **Pickle** | `.pkl` | Dict/array schema and a data preview. |
| **ORC** | `.orc` | Table schema and per-column statistics. |
| **PDF** | `.pdf` | Document structure: metadata header, outline/bookmark + page hierarchy, and detected resources (images, internal/external links, embedded files). |



## Linear Code features

* Live preview that updates as you type.
* Zoom, pan, and search for nodes in the graph.
* Graph information with compact and detailed view toggle.
* Node hierarchy view and search with interactive navigation in code and visual.
* **DOT** visualization graph: interactive edge tracing search and highlight.
* **Data Files** structure and top rows visualization.
* **Program Files** code and structure visualization with call graph and external resources.
* **Visual Web** command — prompts for a URL, opens it in the built-in Simple
  Browser, fetches the *served* HTML, and graphs it through the HTML converter
  (served HTML only; client-rendered SPA content won't appear).

## Usage

Open a supported file in the active editor. With `linear-code.openAutomatically`
enabled (the default) the preview opens on its own; otherwise trigger it via:

* the graph icon in the editor title bar, or
* the editor context menu → **Visual**, or
* the command palette (<kbd>cmd/ctrl</kbd>+<kbd>shift</kbd>+<kbd>p</kbd>) →
  **LinearCode: Visual** (command `linear-code.visualCode`).

To visualize a live web page, run command (<kbd>cmd/ctrl</kbd>+<kbd>shift</kbd>+<kbd>p</kbd>) → **LinearCode: Visual Web**
(command `linear-code.visualWeb`).


## Notes

This extension uses
[`@vscode/extension-telemetry`](https://github.com/microsoft/vscode-extension-telemetry)
(Microsoft Application Insights) to collect anonymous usage data. Only coarse, non-identifying events such as activate, preview, and webview are collected when default telemetry is turned on. Document contents, file names/paths, and URLs are never collected.
Telemetry follows your VS Code setting: `"telemetry.telemetryLevel"`.


## Release Notes

See the [CHANGELOG](./CHANGELOG.md).
