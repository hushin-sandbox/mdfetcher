# mdfetcher

CLI tool that fetches a web page, extracts its main content, and saves it as Markdown.

## Installation

### Method 1: Use the install script (recommended)

```bash
curl -fsSL https://raw.githubusercontent.com/hushin-sandbox/mdfetcher/main/scripts/install.sh | bash
```

### Method 2: Manually download the binary

[Releases](https://github.com/hushin-sandbox/mdfetcher/releases/latest) page from which you can download the binary for your platform.

#### Linux/macOS

```bash
# Download (Example: for Linux x64)
curl -L https://github.com/hushin-sandbox/mdfetcher/releases/download/v1.0.0/mdfetcher-linux-x64 -o mdfetcher
# Grant execution permission
chmod +x mdfetcher
# Move to a directory included in your PATH
mv mdfetcher ~/.local/bin/
```

#### Windows

Download the .exe file, place it in a directory included in your PATH, or run it directly.

## Usage

```bash
mdfetcher [URL] [options]
```

### Options

| Option                   | Description                                               |
| ------------------------ | --------------------------------------------------------- |
| `-o, --output-dir <dir>` | Specify the output directory (default: current directory) |
| `--overwrite`            | Overwrite existing files                                  |
| `--skip`                 | Skip existing files                                       |
| `-h, --help`             | Display help                                              |
| `-v, --version`          | Display version                                           |

### Examples

```bash
# Process a single URL
mdfetcher https://example.com/article

# Specify the output directory
mdfetcher -o ~/documents https://example.com/article

# Process multiple URLs from standard input (one URL per line)
cat urls.txt | mdfetcher
```

### Output format

The output file will be in the following format:

- Path: `{domain}/{pathname}.md`
- Frontmatter metadata
  - title: Page title
  - url: Original URL
  - fetchDate: Date and time
  - author: Author (if available)
  - description: Description (if available)

Example:

```markdown
---
title: 'Article Title'
url: https://example.com/article
fetchDate: '2024-01-01T12:34:56.789Z'
author: 'Author Name'
description: 'Article description'
---

Content...
```

## Developer Information

### Setting up the development environment

```bash
# Clone the repository
git clone https://github.com/hushin-sandbox/mdfetcher.git
cd mdfetcher

# Install dependencies
bun install

# Run locally
bun run index.ts

# Build
bun run build
```

### Release procedure

1. Update the version

```bash
npm version patch # or minor, major
```

2. GitHub Actions will automatically build and release

### Technology stack

- [Bun](https://bun.sh/) - JavaScript/TypeScript runtime
- [@mozilla/readability](https://github.com/mozilla/readability) - Extracts main content from web pages
- [turndown](https://github.com/mixmark-io/turndown) - Converts HTML to Markdown
- [commander](https://github.com/tj/commander.js) - CLI interface

## License

MIT
