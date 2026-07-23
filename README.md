# Linear Code

**See any file as an interactive graph - 30+ formats, live, without leaving your editor.**

Open a file and Linear Code draws its *structure* beside the source: a JSON tree, a
CSV schema, a Parquet footer, a Python call graph, an OWL ontology, a PDF outline.
The graph is interactive - zoom, pan, search, and click a node to jump to the line
that produced it. It re-renders as you type, and one toggle switches between a
compact overview and a detailed view with every attribute, row, and column statistic.

Use it to:

* **Read a data file you can't read by eye.** CSV, Parquet, ORC, Avro, Pickle, RDS,
  and log files open as a schema with per-column types, unique/empty counts, and a
  top-rows preview - including the binary ones. No pandas, no notebook, no conversion step.
* **Understand code you didn't write.** Python, JavaScript/TypeScript, C/C++, Go, Rust, PHP, R, Ruby/Rails,
  Shell, and Jupyter notebooks become a call graph: functions and classes as nodes, calls as
  edges, plus the imports, database/URL/file resources, and CLI args each one touches. Rails
  apps also get their ActiveRecord models and associations, routes, and views.
* **Get your bearings in an unfamiliar repo.** Point **Visual Project** at a folder and
  it maps the structure: directories as nodes carrying per-file-type counts and total
  size, files color-coded by type - so you can see a codebase's shape before opening
  a single file.
* **Inspect a schema or spec at a glance.** OpenAPI/Swagger as an endpoint map, XSD as
  a class diagram, RDF/OWL/Turtle as an ontology, and DTD, GraphML, DOT/Graphviz, XML,
  YAML, Markdown, PDF, and HTML each rendered in the shape that suits them.
* **See what an MCP server actually exposes.** Point **Visual MCP** at an MCP URL and
  get its tools with their input schemas, prompts, and resources - plus, on request,
  the real result of calling a read-only tool.
* **Graph a live web page or REST API.** Point **Visual Web** or **Visual API** at a URL
  and read the served page, or the API's endpoints and live response data.
* **See what a package really pulls in - before you install it.** **Visual Package**
  takes a name from PyPI, npm, crates.io, or RubyGems and draws its dependency tree:
  versions and version requirements, the optional extras each one hides behind a
  feature flag, and - on request - the packages that depend on it.

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

### PACKAGE - dependencies in Python PyPi, Javascript NPM, Ruby Gem or Rust Crates repositories

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_package.gif" />

The **Visual Package** command takes a package name from PyPI, npm, crates.io, or RubyGems and maps its dependency tree straight from the registry - each node a package with its version, and edges labeled with the version requirement. A shared dependency is a single reused node, so you see what's actually pulled in. Compact shows the direct runtime dependencies; Detailed adds the optional/feature-gated ones and one tier deeper, and can pull in the packages that depend *on* yours (in green). Node color separates the primary dependencies from optional and not-yet-resolved ones at a glance.

### Web - graph a live page straight from its URL
<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_web.jpg" />

The **Visual Web** command opens a URL in the built-in browser and graphs its *served* HTML the same way - here `anthropic.com`, with DOM-access rows resolved onto the page's script functions.

### HTML - page structure with embedded scripts

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_html.jpg" />

`Google.html` as a page-structure graph: the container hierarchy merged with the functions and call graph parsed out of the page's embedded `<script>` blocks.

### PROJECT - folder and file structure

<img src="https://raw.githubusercontent.com/linear-code/vscode/main/media/ex_project.gif" />

The **Visual Project** command walks a folder and maps its structure: each directory is a node carrying its per-file-type counts and total size, linked to its children. Files are color-coded by type - program, data, doc, image, config, and so on - so a codebase's shape and where its weight sits are visible before you open anything. Compact shows the folder tree alone; Detailed adds the individual files.

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
| C / C++ | `.c` `.h` `.cpp` `.cc` `.cxx` `.hpp` `.hxx` `.hh` `.ino` | Program structure + call graph (functions, classes/structs/enums with members, inheritance, methods, `#include` modules, file/URL resources, `getenv`/`#define`) visualization. |
| Go | `.go` | Program structure + call graph (functions, methods, structs/interfaces with fields and embedding, `import` modules, `pkg.Func` external calls, file/HTTP resources, `os.Getenv`/`flag`) visualization. |
| Rust | `.rs` | Program structure + call graph (functions, structs/enums/traits with fields and variants, `impl` methods and trait implementations, `use`/`mod` modules, `Type::fn` and macro external calls, file/HTTP resources, `env::var`/args) visualization. |
| PHP | `.php` | Program structure + type-level relations and resources visualization. |
| Shell | `.sh`, `.bash`, `.zsh`, `.ksh` | Shell script structure, call graph and resources visualization. |
| Python | `.py`, `.pyw` | Program structure + call graph (functions, classes, imported modules, resources) visualization. |
| R | `.R`, `.r` | Program structure + call graph (functions, modules, library calls, data frames with columns, file/URL resources, args/env) visualization. |
| Ruby / Rails | `.rb`, `.rake`, `.gemspec` | Program structure + call graph (classes, modules, methods), ActiveRecord models with associations, named hash/array data objects with create/read/write relations, and HTTP/file/route/view resources. |
| Jupyter Notebook | `.ipynb` | Notebook and program structure with call graph and resources. |
| **OTHER:** |||
| WEB | `url` | Web page open and static structure (html, js) visualization like in HTML. |
| REST API | `url` | REST API endpoints and structure visualization. |
| MCP server | `url` | MCP server map: tools with their input schemas, plus prompts and resources. |
| NPM package | `name` | **Visual Package: NPM** — search a package on npmjs.com, resolve its latest manifest, and map the dependency tree: packages as nodes (version, engines, and `core packages`/`extra packages` lists with counts) linked by `depends` relations labeled with the semver range; shared dependencies are reused nodes. Compact shows the package and its `dependencies`; Detailed adds `peerDependencies`/`optionalDependencies` (edge-labeled `peer`/`optional`) and one deeper tier, fetched lazily only when you switch. `devDependencies` are excluded. Optionally adds **dependant counts** — npm publishes no list of dependent names, only totals. |
| Gem package | `name` | **Visual Package: Gem** — search a gem on rubygems.org, resolve its latest version, and map the dependency tree: gems as nodes (version, summary, license, and a `core packages` list with count) linked by `depends` relations labeled with the requirement; shared dependencies are reused nodes. RubyGems has no optional-dependency concept, so `development` dependencies are excluded and there is no extra tier — Detailed adds the deeper layer. Optionally adds one layer of green **dependant** gems; the API returns names only, so the first N are shown with the true total as a row. |
| Crates package | `name` | **Visual Package: Crates** — search a crate on crates.io, resolve its latest non-yanked version from Cargo's sparse index, and map the dependency tree: crates as nodes (version, rust-version, and `core packages`/`extra packages` lists with counts) linked by `depends` relations labeled with the version requirement; shared dependencies are reused nodes. Compact shows the crate and its normal dependencies; Detailed adds the **optional, feature-gated** ones — each edge labeled with the Cargo feature that enables it (`derive`) — plus one deeper tier, fetched lazily. `dev` and `build` dependencies are excluded. Optionally adds one layer of green **dependant** crates — the crates that depend on this one, most-depended-on first. |
| PyPI package | `name` | **Visual Package: PyPI** — search a package, resolve its latest-version dependency metadata from pypi.org, and map the dependency tree: packages as nodes (version, requires-python, summary, and `core packages`/`extra packages` lists with counts) linked by `depends` relations labeled with the version specifier; shared dependencies are reused nodes. Compact shows the package and its direct runtime dependencies; Detailed adds the optional (extra-gated) dependencies and one deeper tier — fetched lazily only when you switch to Detailed. Optionally adds **dependant counts** — PyPI publishes no list of dependent names, only totals. |


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
* **Visual Project** command prompts for a folder (default: the workspace root) and
  maps its folder/file structure — each folder is a node showing its per-file-type
  counts, file count and total size, and each file is a leaf node colored by its
  type group (program, data, doc, image, config, graph, web). File leaf nodes appear
  in Detailed view; Compact shows the folder tree alone. Noise dirs (`.git`,
  `node_modules`, build outputs) are skipped.
* **Visual Package: (PyPi | Crates | Npm | Gems):** command prompts for a package name, connects to package management repository and
  maps its dependent packages structure to graph nodes and relation.


## Notes

This extension uses Microsoft VSCode telemetry to collect standard anonymous non-identifying usage data when turned on (default).


## Release Notes

See the [CHANGELOG](./CHANGELOG.md).
