# Agent Guide — Nord for Zed

## What this repo is

A single-variant dark theme for the Zed editor, structured as a Zed extension. The only output file that matters is `themes/nord.json`.

## File structure

```
nord-zed/
├── extension.toml      # Zed extension manifest
├── themes/nord.json    # The theme (only file an AI should edit)
├── swatches.svg        # Color palette reference, embedded in README
├── LICENSE
└── README.md
```

> **Maintenance note:** If any color assignment in `themes/nord.json` changes, update `swatches.svg` to match. The SVG is the canonical visual reference embedded in the README and must stay in sync with the theme.

## How to test locally

1. Open Zed's Extensions panel (`cmd+shift+x`)
2. Click **Install Dev Extension** → select this directory
3. Open theme picker (`cmd+k cmd+t`) → select **Nord**
4. Edit `themes/nord.json`, then **Reload Extensions** in the Extensions panel

## Nord color palette

| Name | Hex | Role in this theme |
|---|---|---|
| nord0 | `#2e3440` | Editor bg, sidebar bg, panel bg, inactive tabs |
| nord1 | `#3b4252` | Status bar, active tab, section headers, elevated surfaces |
| nord2 | `#434c5e` | Selection, active line, scrollbar thumb |
| nord3 | `#4c566a` | Borders, indent guides |
| `#616e88` | *(custom)* | Line numbers, comments, disabled text, ignored files |
| nord4 | `#d8dee9` | Primary text, icons, editor foreground |
| nord5 | `#e5e9f0` | Terminal ANSI white |
| nord6 | `#eceff4` | Punctuation, bold emphasis, terminal bright white |
| nord7 | `#8fbcbb` | Types, classes, attributes, enums, namespaces |
| nord8 | `#88c0d0` | Functions, selectors, links, accent color |
| nord9 | `#81a1c1` | Keywords, operators, tags, booleans, constructors |
| nord10 | `#5e81ac` | Preprocessor directives |
| nord11 | `#bf616a` | Errors, deleted |
| nord12 | `#d08770` | Decorators, annotations, conflicts |
| nord13 | `#ebcb8b` | Warnings, regex, string escapes, constants |
| nord14 | `#a3be8c` | Strings, success, added |
| nord15 | `#b48ead` | Numbers |

`#616e88` is not a standard Nord palette color. It appears in the official VSCode Nord theme as the syntax comment color and is used here as the general subdued-UI color.

## Key decisions and rationale

**`text` and `text.muted` are both nord4.**
VSCode Nord uses `#d8dee9` for all sidebar/list foreground with no muted variant. Visual hierarchy comes from background differences (active tab = nord1, selected item = nord2), not from dimming text.

**`#616e88` for line numbers, not nord3.**
VSCode Nord uses nord3 for `editorLineNumber.foreground`, but `#616e88` is more readable against the nord0 background. Deliberate deviation.

**`#616e88` for disabled, placeholder, and ignored states.**
Nord3 is too dark against nord0 for UI elements. `#616e88` provides a readable subdued level.

**Booleans use nord9, not nord15.**
VSCode Nord maps `constant.language` (true/false/null) to `#81a1c1` — the same as keywords. Nord15 is reserved for numeric literals.

**Constructor uses nord9, not nord8.**
VSCode Nord maps `support.function.construct` to `#81A1C1`, not the general function color.

**`string.regex` and `string.escape` use nord13, not nord14.**
Regex and escape sequences get the yellow (nord13) to distinguish them from plain string content (nord14/green).

## Cross-reference source

The authoritative color reference is the [official VSCode Nord theme](https://github.com/nordtheme/vscode) at `themes/nord-color-theme.json`. When making color decisions, check `tokenColors` for syntax and `colors` for UI elements.

The Zed schema reference is the One Dark built-in theme at `zed-one-builtin/one.json` (in the parent workspace), which defines all valid color keys.
