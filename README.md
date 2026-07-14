# Linear Code

**See any file as an interactive graph - 25+ formats, live, without leaving your editor.**

Open a file and Linear Code draws its *structure* beside the source: a JSON tree, a
CSV schema, a Parquet footer, a Python call graph, an OWL ontology, a PDF outline.
The graph is interactive - zoom, pan, search, and click a node to jump to the line
that produced it. It re-renders as you type, and one toggle switches between a
compact overview and a detailed view with every attribute, row, and column statistic.

Use it to:

* **Read a data file you can't read by eye.** CSV, Parquet, ORC, Avro, Pickle, RDS,
  and log files open as a schema with per-column types, unique/empty counts, and a
  top-rows preview - including the binary ones. No pandas, no notebook, no conversion step.
* **Understand code you didn't write.** Python, JavaScript/TypeScript, PHP, R, Shell,
  and Jupyter notebooks become a call graph: functions and classes as nodes, calls as
  edges, plus the imports, database/URL/file resources, and CLI args each one touches.
* **Inspect a schema or spec at a glance.** OpenAPI/Swagger as an endpoint map, XSD as
  a class diagram, RDF/OWL/Turtle as an ontology, and DTD, GraphML, DOT/Graphviz, XML,
  YAML, Markdown, PDF, and HTML each rendered in the shape that suits them.
* **See what an MCP server actually exposes.** Point **Visual MCP** at an MCP URL and
  get its tools with their input schemas, prompts, and resources - plus, on request,
  the real result of calling a read-only tool.
* **Graph a live web page or REST API.** Point **Visual Web** or **Visual API** at a URL
  and read the served page, or the API's endpoints and live response data.

Everything renders locally in a VS Code webview - no server, no export step, and your
files never leave the editor.

## Install

Search **Linear Code** in the Extensions view (<kbd>cmd/ctrl</kbd>+<kbd>shift</kbd>+<kbd>x</kbd>),
or run `ext install linearcode.linearcode` in the command palette. Then open any
supported file - see [Usage](#usage) below.

## Use Cases and Examples

Each example shows the source file (or live page) on the left and the interactive Linear Code graph on the right.

### MCP - an MCP server's tools, schemas, prompts and resources

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_mcp.jpg" />

The **Visual MCP** command opens a session against an MCP server and maps everything it exposes - here Hugging Face's `@huggingface/mcp-services` (7 tools, 4 prompts, 26 resources), in Detailed view. Each violet tool node lists its parameters and the behavior hints the server itself declares (`annotations: readOnly, openWorld`), and links to a green `input` schema node carrying every argument's full description - plus an `output` node for the tools that declare one. Orange nodes are prompts, teal nodes are resources with their `uri` and `mimeType`, and the header panel holds the server's version, capabilities and usage instructions. Hover any node for its untruncated text. Tools are never called unless you pick them and type their arguments; the result then renders as its own node.

### API - a live REST API straight from its URL

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_oapi.jpg" />

The **Visual API** command finds an API's OpenAPI/Swagger descriptor from just its base URL - here Context7's public API (OpenAPI 3.0.0, 16 endpoints across 6 tags), in Compact view. Blue tag nodes group the violet endpoint nodes, each badged with its HTTP method and carrying its summary, auth, request body and response codes; the green schema nodes show the request/response structures and link to each other by field, so `SearchResponse` points at `Library` along its `results` field. Detailed view adds the real JSON the API returned when scanned.

### Web - graph a live page straight from its URL
<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_web.jpg" />

The **Visual Web** command opens a URL in the built-in browser and graphs its *served* HTML the same way - here `anthropic.com`, with DOM-access rows resolved onto the page's script functions.

### HTML - page structure with embedded scripts

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_html.jpg" />

`Google.html` as a page-structure graph: the container hierarchy merged with the functions and call graph parsed out of the page's embedded `<script>` blocks.

### JSON - nested records as a navigable tree

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_json.jpg" />

`movies.json` walked into a graph: the large `movies` array is bucketed into ranged groups, each movie object expands into property rows, and nested `Ratings` arrays branch out to their own source/value objects - shown here in Detailed view beside the source.

### XML - the element tree with attributes and nested elements

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_xml.jpg" />

`movies.xml` as an element tree: every `Movie` carries its attributes and text as rows and links to its nested `Title`, `Director`, and `Name` elements. Hovering a node pops up its full, untruncated content.

### CSV - table schema, per-column stats, and a data preview

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_csv.jpg" />

`movies.csv` (4,803 rows × 24 columns): a schema node detects each column's type (number, enum, url, date, …) with unique/empty counts, sitting above a top-rows data-preview table.


## Supported file types

| Format | Extensions | What the graph shows |
|--------|-----------|----------------------|
| **DATA:** |||
| JSON | `.json` | A node/edge graph (auto-detected nodes and edges) or the JSON walked as a tree. |
| XML | `.xml` | The element tree visualization. |
| XSD | `.xsd` | XML schema visualization. |
| DTD | `.dtd` | Document Type Definition visualization. |
| GraphML | `.graphml` | A node/edge graph hierarchy visualization. |
| YAML | `.yaml`, `.yml` | The mapping/sequence tree. |
| OpenAPI / Swagger | `.yaml`, `.json` | An endpoint map: tags as roots, one node per operation (method, path, parameters, responses). |
| CSV / TSV | `.csv`, `.tsv` | Table schema plus a top-rows data preview. |
| Parquet | `.parquet` | Table schema and per-column statistic with a data preview. |
| Pickle | `.pkl` | Dict/array schema and a data preview. |
| ORC | `.orc` | Table schema and per-column statistics with a data preview. |
| Avro | `.avro` | Table schema and per-column statistics with a data preview. |
| R Data File | `.rds` | R data file - data.frame / matrix / vector table schema, per-column statistics, and a data preview. |
| LOG | `.log` | Log file structure and statistic with top-rows data preview. |
| **DOCUMENTS:** |||
| Markdown | `.md`, `.markdown` | Document structure: the heading outline as a section tree, with content rows and detected resources (images, links). |
| PDF | `.pdf` | Document structure: metadata header, outline/bookmark + page hierarchy, and detected resources (images, internal/external links, embedded files). |
| Graphviz / DOT | `.dot`, `.gv` | The DOT source rendered via d3-graphviz (SVG). |
| RDF/XML | `.rdf` | An OWL/RDFS ontology class diagram (classes as nodes, properties as rows/edges). |
| OWL | `.owl` | The same ontology class diagram (RDF/XML or OWL/XML functional syntax). |
| Turtle | `.ttl` | An RDF resource (instance) graph: resources as nodes with their type and attributes, and labeled relations between them. |
| HTML | `.html`, `.htm` | Page structure (container hierarchy, elements as rows, embedded JS, images, external resources). |
| **PROGRAMS:** |||
| JavaScript / TypeScript | `.js` `.jsx` `.ts` `.tsx` `.mjs` `.cjs` | Program structure + scope-resolved call graph (functions, classes, imports, detected resources) visualization. |
| PHP | `.php` | Program structure + type-level relations and resources visualization. |
| Shell | `.sh`, `.bash`, `.zsh`, `.ksh` | Shell script structure, call graph and resources visualization. |
| Python | `.py`, `.pyw` | Program structure + call graph (functions, classes, imported modules, resources) visualization. |
| R | `.R`, `.r` | Program structure + call graph (functions, modules, library calls, data frames with columns, file/URL resources, args/env) visualization. |
| Jupyter Notebook | `.ipynb` | Notebook and program structure with call graph and resources. |
| **OTHER:** |||
| WEB | `url` | Web page open and static structure (html, js) visualization like in HTML. |
| REST API | `url` | REST API endpoints and structure visualization. |
| MCP server | `url` | MCP server map: tools with their input schemas, plus prompts and resources. |



## Linear Code features

* Live preview that updates as you type.
* Zoom, pan, and search for nodes in the graph.
* Graph information with compact and detailed view toggle.
* Node hierarchy view and search with interactive navigation in code and visual.
* **Document Files** visualization with interactive tracing and highlight.
* **Graph Files** visualization with interactive tracing and highlight.
* **Data Files** structure and top rows visualization.
* **Program Files** code and structure interactive visualization with call graph, internal and external resources.
* **Visual Web** command prompts for a URL, opens it in the built-in Simple
  Browser, fetches the *served* HTML, and graphs it through the HTML converter
  (served HTML only; client-rendered SPA content won't appear).
* **Visual API** command prompts for a URL, fetches the *served* API document, and
  graphs its endpoints through the OpenAPI converter.
* **Visual MCP** command prompts for an MCP server URL (and an optional API key),
  opens an MCP session and graphs the server's tools with their input/output
  schemas, plus its prompts and resources. Detailed view expands each tool's input
  schema and can show a real tool result: you pick which read-only tools to run and
  type their arguments.

## Usage

Open a supported file in the active editor. With `linear-code.openAutomatically`
enabled (the default) the preview opens on its own; otherwise trigger it via:

* the graph icon in the editor title bar, or
* the editor context menu → **Visual**, or
* the command palette (<kbd>cmd/ctrl</kbd>+<kbd>shift</kbd>+<kbd>p</kbd>) →
  **LinearCode: Visual** (command `linear-code.visualCode`).

To visualize a live web page, run command (<kbd>cmd/ctrl</kbd>+<kbd>shift</kbd>+<kbd>p</kbd>) → **LinearCode: Visual Web**
(command `linear-code.visualWeb`).

To visualize a live REST API, run command (<kbd>cmd/ctrl</kbd>+<kbd>shift</kbd>+<kbd>p</kbd>) → **LinearCode: Visual API**
(command `linear-code.visualApi`).

To visualize a live MCP server, run command (<kbd>cmd/ctrl</kbd>+<kbd>shift</kbd>+<kbd>p</kbd>) → **LinearCode: Visual MCP**
(command `linear-code.visualMcp`).

## Notes

This extension uses Microsoft VSCode telemetry to collect standard anonymous non-identifying usage data when turned on (default).


## Release Notes

See the [CHANGELOG](./CHANGELOG.md).
