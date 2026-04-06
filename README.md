# IsoBrowse WASM Modules

This repository contains standalone WebAssembly (WASI) tools used by IsoBrowse.

Each module is a small, single-purpose CLI-style utility compiled to WASM.
They are designed to run in a sandbox and be chained together using pipelines.

👉 https://github.com/igtumt/isobrowse

---

## ⚡ Example

```bash
/echo "hello world" | /run uppercase
```

```bash
/get news.ycombinator.com | /run htmlclean | /run linkextract | /run sort
```

```bash
/get https://httpbin.org/json | /run jq "slideshow.title""
```

---

## 🧪 Usage

Run any module inside IsoBrowse:

```bash
/echo "HELLO" | /run lowercase
```

---

## 🧠 Design Philosophy

* Zero dependencies
* Stream-first processing (`stdin → stdout`)
* Sandbox-first and Local execution
* Do one thing well

---

## 🧰 Modules (Quick Overview)

IsoBrowse includes ~80 WASM tools for text processing, data parsing, web scraping, encoding, and more.

For more detail examples check wasm-tool-examples.txt

Below are some commonly used ones:

### 📄 Text

```bash
/echo "hello" | /run uppercase
/read ~/Desktop/test/server.log | /run grep "ERROR"
/echo "a,b,c" | /run cut -d ',' -f 2
```

### 📊 JSON

```bash
/get https://jsonplaceholder.typicode.com/users | /run jq "0.name"
/echo "{\"a\":1}" | /run jsonfmt
```

### 🌐 Web

```bash
/get example.com | /run htmlclean
/get news.ycombinator.com | /run linkextract
```

### 🔐 Encoding

```bash
/echo "secret" | /run base64
/echo "data" | /run sha256
```

---

## 📦 Full Tool List (80)

In Isobrowse terminal
Full list: /catalog
<img width="1512" height="972" alt="catalog" src="https://github.com/user-attachments/assets/80e2c488-5856-4cb2-8a1b-856d0016afac" />

<details>
<summary>Click to expand full module list</summary>

### 📄 Text & String

awk, camelcase, cut, expand, grep, kebabcase, lowercase, nl, regex, rev, rot13, sed, shuffle, slugify, snakecase, sort, stripansi, tac, trim, uniq, uppercase, wordwrap

### 📂 File & Log

diff, head, linediff, tail, wc

### 📊 Data (JSON / CSV / YAML)

csv2json, csvfilter, csvselect, csvsort, csvstats, env2json, jq, json2csv, json2yaml, jsondiff, jsonfilter, jsonfmt, jsonkeys, jsonmerge, jsonpath, validatejson, yaml2json

### 🌐 Web & HTML

cssminify, html2text, htmlclean, htmltitle, linkdomain, linkextract, metatags, queryparam, tableextract, urlencode, urlparse

### 📝 Markdown

md_links, md_strip, md_toc, md2html

### 🔐 Encoding & Security

base58, base64, bcrypt, hex, jwt, md5, random, sha256, uuid

### 🛠 Utilities

avg, bytecount, entropy, hexdump, histogram, lorem, math, minmax, stats, timestamp

</details>

---

## 🧩 Notes

* All tools operate on streamed input
* No tool has access to your local system
* Tools can be chained freely using pipelines
* No dependencies

---

## 🤝 Contributing

Contributions are welcome.

New tools should follow:

* single responsibility
* stdin → stdout
* no external dependencies

---

## License

MIT + Apache 2.0
