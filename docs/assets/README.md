# Assets Directory

This directory is for storing documentation assets such as:

- SVG diagrams (e.g., `floor-plan.svg`, `diagram.svg`)
- Draw.io files (e.g., `layout.drawio`, `architecture.drawio`)
- Images and screenshots
- Other media files

## Adding SVG Diagrams

SVG files placed here can be referenced in Markdown documentation:

```markdown
![Floor Plan](../assets/floor-plan.svg)
```

SVG format is natively supported by browsers and MkDocs Material.

## Adding Draw.io Diagrams

Draw.io files (`.drawio` extension) can be placed here and referenced in documentation:

```markdown
![Architecture Diagram](../assets/architecture.drawio)
```

**Note**: To enable automatic conversion of Draw.io files to images during build:
1. Install Draw.io desktop application
2. Uncomment the `drawio-exporter` plugin in `mkdocs.yml`
3. Configure the path to your Draw.io executable

Without the Draw.io executable, you can manually export diagrams as PNG or SVG and reference those instead.

## Example Files

You can add example files here as you develop the specification, such as:
- Architecture overview diagrams
- Layout examples
- Component diagrams
- Process flows
