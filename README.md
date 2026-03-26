# IsoBrowse WASM Modules

This repository contains standalone WebAssembly (WASI) modules used by IsoBrowse.

Each module is a single-purpose CLI-style tool compiled to WASM, designed to be executed in a secure sandbox and chained via pipelines. These modules are designed to run inside the IsoBrowse runtime:

👉 https://github.com/yigtumt/isobrowse

## 🧪 Running a Module

**Using IsoBrowse:**
> /echo "HELLO" | /run lowercase

## 🧠 Design Philosophy

- Do one thing well
- Zero dependencies
- Stream-first processing (stdin → stdout)
- Sandbox-first execution

IsoModules aims to become a portable.

---

## 🧰 Catalog

### 📄 1. Text & String Manipulation
* **`awk`**: Micro column formatter for text data.
  `> /echo "John 25" | /run awk "Name: $1, Age: $2"`
* **`camelcase`**: Converts text to `camelCase`.
  `> /echo "hello_world" | /run camelcase`
* **`cut`**: Removes sections from each line of files/pipe.
  `> /echo "a,b,c" | /run cut -d ',' -f 2`
* **`expand`**: Converts Tabs to standard spaces.
  `> /echo "a\tb" | /run expand`
* **`grep`**: Filters lines matching a specific keyword or pattern.
  `> /cat system.log | /run grep "ERROR"`
* **`kebabcase`**: Converts text to `kebab-case`.
  `> /echo "Hello World" | /run kebabcase`
* **`lowercase`**: Converts all text to lowercase.
  `> /echo "HELLO" | /run lowercase`
* **`nl`**: Numbers all lines in the input.
  `> /run lorem 5 | /run nl`
* **`regex`**: Extracts only the parts of text matching a Regex pattern.
  `> /echo "Mail: a@b.com" | /run regex "[a-z]+@[a-z]+\.[a-z]+"`
* **`rev`**: Reverses the characters of each line.
  `> /echo "hello" | /run rev`
* **`rot13`**: Applies the ROT13 substitution cipher to text.
  `> /echo "secret" | /run rot13`
* **`sed`**: Advanced Regex-based find and replace.
  `> /echo "apple" | /run sed "a" "o"`
* **`shuffle`**: Randomly shuffles the input lines.
  `> /echo "1\n2\n3" | /run shuffle`
* **`slugify`**: Converts text into a URL-friendly slug.
  `> /echo "My New Post!" | /run slugify`
* **`snakecase`**: Converts text to `snake_case`.
  `> /echo "Hello World" | /run snakecase`
* **`sort`**: Sorts lines of text alphabetically or numerically.
  `> /echo "z\na\nb" | /run sort`
* **`stripansi`**: Removes terminal ANSI color and formatting codes.
  `> /cat colored_log.txt | /run stripansi`
* **`tac`**: Reverses the order of lines (prints last line first).
  `> /echo "first\nlast" | /run tac`
* **`trim`**: Trims leading and trailing whitespace from lines.
  `> /echo "  padded  " | /run trim`
* **`uniq`**: Filters out repeated, adjacent lines.
  `> /echo "a\na\nb" | /run uniq`
* **`uppercase`**: Converts all text to UPPERCASE.
  `> /echo "hello" | /run uppercase`
* **`wordwrap`**: Wraps long lines of text to a specified character width.
  `> /run lorem 50 | /run wordwrap 40`

### 📂 2. File & Log Utilities
* **`diff`**: Compares two text inputs and shows differences.
  `> /cat old.txt | /run diff "new content here"`
* **`head`**: Outputs the first N lines of the input.
  `> /cat server.log | /run head 10`
* **`linediff`**: Generates a standard Unified Diff (Patch) between texts.
  `> /cat old.txt | /run linediff "new content"`
* **`patch`**: Applies a Unified Diff patch to a text.
  `> /cat source.txt | /run patch "patch_content"`
* **`tail`**: Outputs the last N lines of the input.
  `> /cat server.log | /run tail 15`
* **`wc`**: Counts newlines, words, and bytes (Word Count).
  `> /cat document.txt | /run wc`

### 📊 3. JSON, CSV, YAML & Data Structures
* **`csv2json`**: Converts CSV tables into a JSON array.
  `> /cat data.csv | /run csv2json`
* **`csvfilter`**: Filters CSV rows based on a target column value.
  `> /cat users.csv | /run csvfilter 2 "Active"`
* **`csvselect`**: Extracts specific columns from a CSV file.
  `> /cat data.csv | /run csvselect 1,3,5`
* **`csvsort`**: Sorts a CSV file based on a specific column.
  `> /cat data.csv | /run csvsort 2`
* **`csvstats`**: Generates a row and column summary for large CSVs.
  `> /cat big_data.csv | /run csvstats`
* **`env2json`**: Converts `.env` configuration files to JSON.
  `> /cat .env | /run env2json`
* **`jq`**: Extracts specific keys or values from a JSON object.
  `> /get api.example.com | /run jq "name"`
* **`json2csv`**: Converts a JSON array of objects into a CSV file.
  `> /cat data.json | /run json2csv`
* **`json2yaml`**: Converts JSON objects into human-readable YAML.
  `> /cat config.json | /run json2yaml`
* **`jsondiff`**: Structural comparison between two JSON objects in an array.
  `> /echo "[{\"a\":1}, {\"a\":2}]" | /run jsondiff`
* **`jsonfilter`**: Filters a JSON array based on a key-value condition.
  `> /cat users.json | /run jsonfilter "role" "admin"`
* **`jsonfmt`**: Pretty-prints and formats minified JSON data.
  `> /echo "{\"a\":1}" | /run jsonfmt`
* **`jsonkeys`**: Lists all top-level keys in a JSON object.
  `> /cat data.json | /run jsonkeys`
* **`jsonmerge`**: Merges an array of JSON objects into a single object.
  `> /echo "[{\"a\":1}, {\"b\":2}]" | /run jsonmerge`
* **`jsonpath`**: Deep querying tool for JSON using JSONPath syntax.
  `> /cat data.json | /run jsonpath "$.users[0].email"`
* **`validatejson`**: Strictly checks if the input is a valid JSON string.
  `> /cat data.json | /run validatejson`
* **`yaml2json`**: Converts YAML configurations into JSON.
  `> /cat docker-compose.yml | /run yaml2json`

### 🌐 4. Web, HTML & URL Tools
* **`cssminify`**: Minifies CSS by removing comments and whitespace.
  `> /cat style.css | /run cssminify`
* **`html2text`**: Strips all HTML tags, leaving only readable text.
  `> /get example.com | /run html2text`
* **`htmlclean`**: Strips `<script>`, `<style>`, and HTML comments.
  `> /get example.com | /run htmlclean`
* **`htmltitle`**: Extracts the `<title>` text from an HTML document.
  `> /get example.com | /run htmltitle`
* **`linkdomain`**: Extracts only root domains from a list of URLs.
  `> /cat links.txt | /run linkdomain`
* **`linkextract`**: Scrapes and lists all `href` links from HTML.
  `> /get news.ycombinator.com | /run linkextract`
* **`metatags`**: Extracts SEO meta tags (name and content) from HTML.
  `> /get example.com | /run metatags`
* **`queryparam`**: Parses complex URL query parameters into a list.
  `> /echo "http://site.com?id=5&q=test" | /run queryparam`
* **`tableextract`**: Converts HTML `<table>` elements into CSV data.
  `> /get example.com | /run tableextract`
* **`urlencode`**: Safely encodes text for use in URLs.
  `> /echo "hello world" | /run urlencode`
* **`urlparse`**: Breaks down a URL into its scheme, host, port, and path.
  `> /echo "https://site.com:80/path" | /run urlparse`

### 📝 5. Markdown Processing
* **`md_links`**: Extracts all `[Text](URL)` links from Markdown.
  `> /cat README.md | /run md_links`
* **`md_strip`**: Removes Markdown formatting to extract raw text.
  `> /cat README.md | /run md_strip`
* **`md_toc`**: Generates a Table of Contents from Markdown `# Headers`.
  `> /cat README.md | /run md_toc`
* **`md2html`**: Converts standard Markdown text into HTML.
  `> /cat file.md | /run md2html`

### 🔐 6. Security, Hashing & Encoding
* **`base58`**: Encodes/decodes data using Base58.
  `> /echo "secret" | /run base58`
* **`base64`**: Encodes/decodes data using Base64 format.
  `> /echo "secret" | /run base64`
* **`bcrypt`**: Hashes passwords using the bcrypt algorithm.
  `> /echo "mypassword" | /run bcrypt`
* **`hex`**: Encodes/decodes text to hexadecimal format.
  `> /echo "data" | /run hex`
* **`jwt`**: Decodes JSON Web Tokens (JWT) into readable JSON payloads.
  `> /echo "eyJhb..." | /run jwt`
* **`md5`**: Generates an MD5 hash of the input text.
  `> /echo "data" | /run md5`
* **`random`**: Generates a secure random string.
  `> /run random 16`
* **`sha256`**: Generates a secure SHA-256 hash of the input text.
  `> /echo "data" | /run sha256`
* **`uuid`**: Generates a universally unique identifier (UUID v4).
  `> /run uuid`

### 🛠 7. Math, Analytics & Developer Debug
* **`avg`**: Calculates the average of a list of numbers.
  `> /echo "10 20 30" | /run avg`
* **`bytecount`**: Counts the exact byte size of the data payload.
  `> /cat image.png | /run bytecount`
* **`entropy`**: Calculates Shannon Entropy to detect encrypted/compressed data.
  `> /cat archive.zip | /run entropy`
* **`hexdump`**: Displays raw data byte-by-byte with memory offsets.
  `> /cat binary.dat | /run hexdump`
* **`histogram`**: Visualizes data distribution using ASCII bar charts.
  `> /echo "Error 50\nWarn 20" | /run histogram`
* **`lorem`**: Generates placeholder "Lorem Ipsum" text.
  `> /run lorem 30`
* **`math`**: Evaluates mathematical expressions.
  `> /echo "5 * (10 + 2)" | /run math`
* **`minmax`**: Finds the minimum and maximum values in a number list.
  `> /echo "5 100 2" | /run minmax`
* **`stats`**: Generates basic statistics (sum, mean, count) from numbers.
  `> /echo "10 20 30" | /run stats`
* **`timestamp`**: Outputs the current UNIX epoch timestamp.
  `> /run timestamp`
