# goxgettext

<p align="center">
  <strong>gettext-style extraction workflow for Go and GoHTML projects</strong><br/>
  Extract translation keys, generate POT/PO catalogs, update language files from LINGUAS, and keep POTFILES in sync.
</p>

<p align="center">
  <a href="#-installation"><strong>Install</strong></a>
  ·
  <a href="#-usage"><strong>Usage</strong></a>
  ·
  <a href="#-example"><strong>Example</strong></a>
  ·
  <a href="#-release-binaries"><strong>Release</strong></a>
  ·
  <a href="#license"><strong>License</strong></a>
</p>

> [!TIP]
> Quick start:
>
> ```bash
> goxgettext --all --output-dir po .
> ```

[![Release](https://img.shields.io/github/v/release/gouef/goxgettext?style=for-the-badge)](https://github.com/gouef/goxgettext/releases)
[![Release Date](https://img.shields.io/github/release-date/gouef/goxgettext?style=for-the-badge)](https://github.com/gouef/goxgettext/releases)
[![Downloads](https://img.shields.io/github/downloads/gouef/goxgettext/total?style=for-the-badge)](https://github.com/gouef/goxgettext/releases)
[![License](https://img.shields.io/github/license/gouef/goxgettext?style=for-the-badge)](LICENSE)

[![Tests](https://img.shields.io/github/actions/workflow/status/gouef/goxgettext/tests.yml?style=for-the-badge)](https://github.com/gouef/goxgettext/actions/workflows/tests.yml)
[![Coverage](https://img.shields.io/codecov/c/github/gouef/goxgettext?style=for-the-badge)](https://app.codecov.io/gh/gouef/goxgettext)
[![Commit Lint](https://img.shields.io/github/actions/workflow/status/gouef/goxgettext/commit-lint.yml?style=for-the-badge)](https://github.com/gouef/goxgettext/actions/workflows/commit-lint.yml)
[![Go Version](https://img.shields.io/badge/Go-1.26.5-00ADD8?logo=go&style=for-the-badge)](https://go.dev/)

Lightweight gettext-style extractor for Go projects.

goxgettext scans Go source files and GoHTML/HTML templates, collects translatable strings, and generates POT/PO catalogs for your project.

## ✨ Features

- Extracts messages from Go calls such as `gettext`, `t`, `T`, and `i18n`
- Scans GoHTML and HTML templates for translation calls (keyword-based)
- Supports recursive directory scanning
- Generates POT and PO output
- Can create language-specific PO files and a POTFILES list from `LINGUAS`
- Supports custom keywords and additional file extensions

## 🚀 Installation

Install the latest release binary with Go:

```bash
go install github.com/gouef/goxgettext@latest
```

Install from the repository source:

```bash
make build
```

The binary will be created at ./bin/goxgettext and can be run directly.

Install from a single shell script:

```bash
curl -fsSL https://raw.githubusercontent.com/gouef/goxgettext/main/install.sh -o /tmp/install-goxgettext.sh
sh /tmp/install-goxgettext.sh
```

The script downloads the correct release binary for your platform and installs it to `$HOME/.local/bin/goxgettext` by default. Make sure that directory is on your `PATH`.

No `chmod +x` is required here — the script is intended to be run as `sh /tmp/install-goxgettext.sh`.

If you want a system-wide install, you can override the target directory:

```bash
INSTALL_DIR=/usr/local/bin sh /tmp/install-goxgettext.sh
```

After installation, you can run `goxgettext` directly from your shell.

## 🧪 Usage

The simplest workflow is to generate everything in one step:

```bash
./bin/goxgettext --all --output-dir locale .
```

Language files are generated from entries in `LINGUAS` (for example `cs` and `en`).

This creates:

- a POT file at `locale/messages.pot`
- a PO file at `locale/messages.po`
- language files such as `locale/cs.po`
- a `locale/POTFILES` list

If you only want a POT catalog:

```bash
./bin/goxgettext --output messages.pot .
```

If you only want a PO catalog:

```bash
./bin/goxgettext --format po --output messages.po .
```

If you want to generate language files without writing the POT/PO files:

```bash
./bin/goxgettext --output-dir locale .
```

This also uses `LINGUAS` to decide which language files are generated.

Create release binaries for multiple platforms:

```bash
make release
```

## 📘 Example

Minimal project input:

```text
my-app/
  po/
    LINGUAS
  views/
    navigation.gohtml
  main.go
```

`po/LINGUAS` (one language per line):

```text
cs
en
```

`views/navigation.gohtml`:

```gohtml
<nav>
  <a>{{ i18n "nav.home" }}</a>
  <a>{{ i18n "nav.projects" }}</a>
</nav>
```

Run:

```bash
goxgettext --all --output-dir po .
```

Generated files:

```text
po/messages.pot
po/messages.po
po/cs.po
po/en.po
po/POTFILES
```

`po/messages.pot` contains references with line numbers, for example:

```po
#: /path/to/my-app/views/navigation.gohtml:2
msgid "nav.home"
msgstr ""
```

## 📦 Release binaries

When a tag matching `v*` is pushed, the GitHub Actions workflow in [.github/workflows/release.yml](.github/workflows/release.yml) builds release artifacts for Linux, macOS, and Windows and uploads them to the GitHub Release.

You can also trigger the workflow manually from the Actions tab and choose a tag name.

Download the appropriate binary for your platform from the release page and run it directly.

## ⚙️ Useful flags

- --output: write the generated catalog to a file
- --format: select pot or po output
- --keyword: add custom translation function names
- --extension: include additional file extensions to scan
- --output-dir: write generated language files to a directory
- `LINGUAS`: language list file used for generating/updating language catalogs

## 🛠️ Development

Run the test suite:

```bash
make test
```

Generate a coverage report:

```bash
make coverage
```

## Contributors

<div>
<a href="https://github.com/gouef/goxgettext/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=gouef/goxgettext" />
</a>
</div>

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

This project is licensed under the Apache License 2.0.
See [LICENSE](LICENSE) for details.

