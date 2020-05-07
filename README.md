<!-- omit in toc -->
# Developer Documentation

Home for general best practices & developer workflow documentation. Any and all additions to this documentation should come in the form of PR‘s. If you have a thought for a doc but you‘re unsure or have questions, please open an issue.

<!-- omit in toc -->
## Sections

- [1. Getting Started](#1-getting-started)
- [2. Sections](#2-sections)
- [3. Contributing Guidelines](#3-contributing-guidelines)

## 1. Getting Started

Clone the repo.

```sh
git clone https://github.com/EYLatamSouth/docs
cd docs
```

## 2. Sections

1. [Agile methodology for developers](/agile#readme): Documentation on the agile process
2. [Git](/git#readme): Git usage and practices
3. [Standardization](/standardization#readme): Standards for software development
4. [Style Guide](/style-guide#readme): Style guide for coding, documentation, etc.

## 3. Contributing Guidelines

- Open a pull request with the new doc.
- Always use markdown.
- Choose an existing directory to place the new doc in or create a new “section.”
- If the doc has relevant assets (images, pdfs, etc.) please create an assets dir named `<section>/<doc-name>-assets`. For instance:

  ```txt
  git/
  ├── branching-assets/
  │   └── img.png
  └── branching.md
  ```

- If you think the doc is more of a one-off and doesn‘t really fit into a broad enough section, then put it in `/docs`.
- Directories should always be **totally lowercase with dashes separating words**.
- Document filenames should always be **totally lowercase with dashes separating words**, i.e. `name-with-dashes.md`.


> **Disclaimer**: this documentation was based on Developer Documentation of [EY Blockchain Group](https://github.com/EYBlockchain/README). Some files were purged, others updated in order to reflect the actual state of software engineering regarding the Latam South region.