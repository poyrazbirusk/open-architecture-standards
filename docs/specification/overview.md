# Specification Overview

The Open Architecture Standards (OAS) specification defines a comprehensive schema for representing architectural designs in a machine-readable format.

## Design Principles

The OAS specification is built on these core principles:

### 1. Simplicity First

- Use standard JSON format
- Minimize nested complexity
- Clear and intuitive property names

### 2. LLM-Friendly

- Natural language-compatible structure
- Consistent naming conventions
- Self-documenting schemas

### 3. Precision

- Millimeter-accurate coordinates
- Explicit dimensional properties
- No ambiguity in measurements

### 4. Extensibility

- Support for custom properties
- Modular design
- Forward-compatible versioning

## Specification Structure

The OAS specification is organized into these main sections:

### Document Root

Every OAS document starts with metadata:

- `version`: Specification version
- `metadata`: Optional document information
- `layout`: The main architectural content

### Layout Definition

The layout contains:

- `id`: Unique identifier
- `name`: Human-readable name
- `rooms`: Array of room definitions
- `walls`: Array of wall definitions
- `openings`: Array of doors, windows, etc.

### Coordinate System

!!! info "Coordinate Reference"
    All coordinates in OAS use millimeters (mm) as the base unit. The origin point (0,0) typically represents a reference corner or center point of the layout.

### Diagrams

You can include diagrams using various formats:

#### SVG Example

SVG images are natively supported by MkDocs Material:

```markdown
![Architecture Diagram](../assets/diagram.svg)
```

#### Draw.io Example

Draw.io diagrams can be embedded directly:

```markdown
![Layout Example](../assets/layout.drawio)
```

The Draw.io exporter plugin will automatically convert these to images during the build process.

## Validation

OAS documents should be validated against the JSON schema to ensure correctness. The schema provides:

- Type checking
- Required property validation
- Value range constraints
- Format verification

## Versioning

The specification uses semantic versioning:

- **Major**: Breaking changes
- **Minor**: New features, backward compatible
- **Patch**: Bug fixes and clarifications

Current version: **1.0.0**

## Next Steps

- Explore the detailed [Schema](schema.md)
- See practical [Examples](examples.md)
- Review the JSON Schema definition

## Notes on Extensions

!!! note "Custom Properties"
    While OAS defines a standard set of properties, you can add custom properties for specific use cases. Custom properties should be prefixed with `x-` to avoid conflicts with future standard properties.
