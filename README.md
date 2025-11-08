# Markdown Renderer

A standalone client-side Markdown renderer with support for mathematical equations (KaTeX) and Mermaid diagrams.

## Features

- **Standard Markdown**: Full support for headings, lists, bold, italic, code blocks, and more
- **Mathematical Equations**: Render inline (`$...$`) and block (`$$...$$`) math using KaTeX
- **Mermaid Diagrams**: Create flowcharts, sequence diagrams, and other visualizations
- **Live Preview**: Edit Markdown in real-time with instant rendering
- **Zero Dependencies**: All libraries loaded from CDN - no build step required

## Quick Start

### Option 1: Open Directly in Browser

Simply open `index.html` in any modern web browser.

### Option 2: Run Development Server

```bash
npm run dev
```

The server will start on port 8000. Visit `http://localhost:8000` in your browser.

## Architecture

This implementation uses the [Unified.js](https://unifiedjs.com/) ecosystem to create a sophisticated processing pipeline:

1. **remarkParse**: Parses Markdown text into an Abstract Syntax Tree (AST)
2. **remarkMath**: Extends the parser to recognize TeX math syntax
3. **remarkRehype**: Bridges Markdown AST to HTML AST
4. **Custom Plugin**: Adds compatibility layer for Mermaid diagrams
5. **rehypeMermaid**: Prepares Mermaid code blocks for client-side rendering
6. **rehypeKatex**: Transforms math nodes into KaTeX HTML
7. **rehypeStringify**: Converts the final AST to HTML string

### Two-Part Rendering Process

**Part 1 - Unified Pipeline**: Pure data transformation (String → String)
- Processes Markdown through the plugin chain
- Generates HTML with prepared math and diagram elements

**Part 2 - DOM Rendering**: Client-side visualization
- Injects HTML into the DOM
- Triggers Mermaid.js to render diagrams as SVGs
- KaTeX math renders automatically via CSS

## Example Usage

```markdown
# Sample Document

## Math Equations

Inline math: The lift force $L$ depends on $C_L$.

Block math:

$$
L = \frac{1}{2} \rho v^2 S C_L
$$

## Mermaid Diagram

\`\`\`mermaid
graph TD;
    A[Start] --> B{Decision};
    B -->|Yes| C[Success];
    B -->|No| D[Retry];
\`\`\`
```

## Technical Details

### Dependencies (CDN)

All dependencies are loaded as ES modules from [esm.sh](https://esm.sh):

- unified@11
- remark-parse@11
- remark-math@6
- remark-rehype@11
- rehype-katex@7
- rehype-mermaid@2
- rehype-stringify@10
- unist-util-visit@5
- mermaid@10
- katex@0.16.10 (CSS)

### Browser Compatibility

Requires a modern browser with ES module support:
- Chrome/Edge 89+
- Firefox 89+
- Safari 15+

## License

MIT
