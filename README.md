# Linear Code

Linear Code turns data files and program code into an **interactive live graph
preview** you can zoom, pan, and search. The preview updates as you edit and
supports a compact/detailed toggle for the converted formats.

## Use Cases and Examples

Each example shows the source file (or live page) on the left and the interactive Linear Code graph on the right.

### JSON — nested records as a navigable tree

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_json.jpg" />

`movies.json` walked into a graph: the large `movies` array is bucketed into ranged groups, each movie object expands into property rows, and nested `Ratings` arrays branch out to their own source/value objects — shown here in Detailed view beside the source.

### XML — the element tree with attributes and nested elements

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_xml.jpg" />

`movies.xml` as an element tree: every `Movie` carries its attributes and text as rows and links to its nested `Title`, `Director`, and `Name` elements. Hovering a node pops up its full, untruncated content.

### CSV — table schema, per-column stats, and a data preview

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_csv.jpg" />

`movies.csv` (4,803 rows × 24 columns): a schema node detects each column's type (number, enum, url, date, …) with unique/empty counts, sitting above a top-rows data-preview table.

### HTML — page structure with embedded scripts

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_html.jpg" />

`Google.html` as a page-structure graph: the container hierarchy merged with the functions and call graph parsed out of the page's embedded `<script>` blocks.

### Web — graph a live page straight from its URL

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_web.jpg" />

The **Visual Web** command opens a URL in the built-in browser and graphs its *served* HTML the same way — here `anthropic.com`, with DOM-access rows resolved onto the page's script functions.

## Supported file types

| Format | Extensions | What the graph shows |
|--------|-----------|----------------------|
| **DATA:** |||
| JSON | `.json` | A node/edge graph (auto-detected nodes and edges) or the JSON walked as a tree. |
| XML | `.xml` | The element tree. |
| XSD | `.xsd` | XML schema visualization. |
| DTD | `.dtd` | Document Type Definition visualization. |
| YAML | `.yaml`, `.yml` | The mapping/sequence tree. |
| CSV / TSV | `.csv`, `.tsv` | Table schema plus a top-rows data preview. |
| Parquet | `.parquet` | Table schema and per-column statistic with a data preview. |
| Pickle | `.pkl` | Dict/array schema and a data preview. |
| ORC | `.orc` | Table schema and per-column statistics with a data preview. |
| Avro | `.avro` | Table schema and per-column statistics with a data preview. |
| LOG | `.log` | Log file structure and statistic with top-rows data preview. |
| **DOCUMENTS:** |||
| MD | `.md` | Document structure: metadata header, outline/bookmark + page hierarchy, and detected resources (images, internal/external links). |
| PDF | `.pdf` | Document structure: metadata header, outline/bookmark + page hierarchy, and detected resources (images, internal/external links, embedded files). |
| Graphviz / DOT | `.dot`, `.gv` | The DOT source rendered via d3-graphviz (SVG). |
| RDF/XML | `.rdf` | An OWL/RDFS ontology class diagram (classes as nodes, properties as rows/edges). |
| OWL | `.owl` | The same ontology class diagram (RDF/XML or OWL/XML functional syntax). |
| HTML | `.html`, `.htm` | Page structure (container hierarchy, elements as rows, embedded JS, images, external resources). |
| **PROGRAMS:** |||
| JavaScript / TypeScript | `.js` `.jsx` `.ts` `.tsx` `.mjs` `.cjs` | Program structure + scope-resolved call graph (functions, classes, imports, detected resources). |
| PHP | `.php` | Program structure + type-level relations (classes/interfaces/traits/enums, methods/properties as rows, inheritance, `new`, dependency injection, static calls, and framework/IO resources). |
| Python | `.py`, `.pyw` | Program structure + call graph (functions, classes, imported modules, resources). |
| **OTHER:** |||
| WEB | `url` | Web page open and static structure (html, js) visualization like in HTML. |



## Linear Code features

* Live preview that updates as you type.
* Zoom, pan, and search for nodes in the graph.
* Graph information with compact and detailed view toggle.
* Node hierarchy view and search with interactive navigation in code and visual.
* **DOT** visualization graph with interactive tracing and highlight.
* **Data Files** structure and top rows visualization.
* **Program Files** code and structure interactive visualization with call graph, internal and external resources.
* **Visual Web** command prompts for a URL, opens it in the built-in Simple
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

This extension uses Microsoft VSCode telemetry to collect standard anonymous non-identifying usage data when turned on (default).


## Release Notes

See the [CHANGELOG](./CHANGELOG.md).
