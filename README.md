# IsoBrowse WASM Modules 🚀

IsoBrowse Modules are blazingly fast, standalone terminal tools written entirely in Rust and compiled to WebAssembly (WASI), designed to do one thing perfectly.

Rooted in the legendary **Unix Philosophy** ("Write programs that do one thing and do it well"), these tools are free from heavy external dependencies and run in a lightweight, isolated environment. They consume data from standard input (stdin), process it, and emit it to standard output (stdout), providing a seamless **Pipeline** experience.

## ⚙️ How It Works

All modules are invoked using the `/run <module_name>` syntax. You can chain modules together using the pipe (`|`) operator to build incredibly powerful data processing workflows.

**Basic Usage:**
> /echo "hello world" | /run rot13 | /run wordwrap 5

---

## 🧰 Module Catalog

Our tools are categorized by their primary use cases:

### 📄 1. Text & Log Processing
* **`awk`**: Micro column formatter. (e.g., `... | /run awk "Name: $1, Age: $2"`)
* **`sed`**: Regex-supported advanced find and replace. (e.g., `... | /run sed "old" "new"`)
* **`grep`**: Filters lines containing a specific keyword.
* **`regex`**: Extracts only the parts of the text that match a Regex pattern (e.g., extracting emails).
* **`wordwrap`**: Wraps long text to a specified character width.
* **`nl`**: Adds line numbers to the beginning of each line, perfect for logs.
* **`tac` / `rev` / `shuffle`**: Reverses line order / reverses characters / shuffles lines randomly.
* **`trim` / `expand` / `stripansi`**: Trims whitespace / converts Tabs to spaces / strips terminal color codes.
* **`camelcase` / `snakecase` / `kebabcase`**: Variable naming formatters.

### 🌐 2. Web & Scraping Tools
* **`htmlclean`**: Strips `<script>`, `<style>`, and comments from HTML.
* **`htmltitle` / `metatags`**: Extracts the page title and SEO meta tags.
* **`linkextract` / `linkdomain`**: Finds external links on a page and filters down to root domains.
* **`tableextract`**: Converts HTML tables (`<table>`) into standard CSV format.
* **`queryparam`**: Parses complex URL parameters like `?id=5&token=abc` into a clean, readable list.

### 📊 3. Data Structures: JSON & CSV
* **`jq`**: Extracts a specific key from JSON. (e.g., `... | /run jq "name"`)
* **`jsonpath`**: Advanced query tool for deep JSON data structures. (e.g., `... | /run jsonpath "$.users[*].email"`)
* **`jsonfilter` / `jsonkeys`**: Filters JSON arrays based on conditions / Lists only data keys.
* **`jsondiff`**: Shows structural differences between two JSON objects.
* **`csvselect` / `csvfilter` / `csvsort`**: Selects specific columns, filters rows, and alphabetically sorts massive CSVs.
* **`csvstats`**: Generates a quick row/column summary of large CSV files.
* **`yaml2json` / `json2yaml` / `env2json`**: Lightning-fast conversions between configuration file formats.

### 📝 4. Markdown Processing
* **`md_toc`**: Reads `# Headers` from README files and generates a hierarchical table of contents.
* **`md_links`**: Extracts `[Text](URL)` links from Markdown documents.
* **`md_strip`**: Strips all Markdown formatting (bold, lists, links) leaving pure text (ideal for LLM data prep).

### 🔐 5. Security, Cryptography & Conversion
* **`md5` / `bcrypt`**: One-way secure text hashing.
* **`base64` / `base58` / `hex`**: Encodes and decodes data in machine formats (use `--decode` or `-d` to reverse).
* **`jwt`**: Decodes JSON Web Tokens into raw JSON (Header and Payload) without breaking the signature.
* **`random`**: Generates secure, random passwords or strings of a specified length. (e.g., `/run random 32`)

### 🛠 6. Developer Debug & Analysis
* **`diff` / `linediff` / `patch`**: Compares texts, generates standard Unified Diffs (Patches), and applies them.
* **`validatejson`**: Checks if JSON data is strictly valid and error-free.
* **`entropy`**: Measures data complexity (useful for detecting encrypted or compressed data payloads).
* **`hexdump` / `bytecount`**: Displays data byte-by-byte with memory offsets and counts exact byte size.
* **`math` / `stats` / `minmax` / `avg`**: Calculates mathematical expressions from the pipe and extracts statistics from number arrays.
* **`histogram`**: Visualizes density data from the pipe using in-terminal ASCII bar charts.

---

## 🍳 Cookbook (Example Scenarios)

The true power of IsoBrowse modules is unleashed when they are chained together. Here are some real-world pipelines:

**1. Fetch API Data and Extract a Specific Field:**
    > /get [https://api.github.com/users/octocat](https://api.github.com/users/octocat) | /run jq "company"

**2. Scrape Links from a Website and Analyze Domains:**
    > /nojs [https://news.ycombinator.com](https://news.ycombinator.com) | /run linkextract | /run linkdomain | /run sort | /run uniq

**3. Filter and Analyze a Messy Log File:**
    > /cat server.log | /run grep "ERROR" | /run stats

**4. Generate a Random Password, Encode, and Hash it:**
    > /run random 16 | /run base64 | /run bcrypt

**5. Extract Specific Columns from a CSV and Sort Them:**
    > /cat users.csv | /run csvselect 2,5 | /run csvsort 1

**6. Decode a JWT and Format the Output:**
    > /echo "eyJhbG..." | /run jwt | /run jsonfmt
