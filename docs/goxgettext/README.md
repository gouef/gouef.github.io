# goxgettext

A lightweight gettext-style extractor for Go projects.

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

Generate a single language file explicitly:

```bash
./bin/goxgettext --output-dir locale --language cs .
```

Build release binaries for multiple platforms:

```bash
make release
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
- --language: generate or update a specific language file

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

