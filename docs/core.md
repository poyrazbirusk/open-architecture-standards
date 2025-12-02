# Core Concepts

This page defines the core concepts and fundamental elements of the Open Architecture Standards (OAS).

## Overview

OAS provides a structured way to represent architectural designs using JSON. The specification is built around several core concepts that work together to describe complete architectural layouts.

## Document Structure

Every OAS document follows a standard structure:

```json
{
  "version": "1.0.0",
  "metadata": {...},
  "layout": {...}
}
```

### Version

The `version` field specifies which version of the OAS specification the document conforms to. This allows for backward compatibility and evolution of the standard.

- **Type**: string
- **Required**: Yes
- **Format**: Semantic versioning (e.g., "1.0.0")

### Metadata

The `metadata` object contains document-level information:

```json
{
  "metadata": {
    "title": "Document Title",
    "description": "Document description",
    "author": "Author name",
    "created": "2024-01-01T00:00:00Z",
    "modified": "2024-01-01T00:00:00Z"
  }
}
```

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `title` | string | No | Document title |
| `description` | string | No | Document description |
| `author` | string | No | Document author |
| `created` | string | No | Creation date (ISO 8601) |
| `modified` | string | No | Last modification date (ISO 8601) |

### Layout

The `layout` object is the main container for all architectural data. It contains rooms, walls, openings, and other elements that define the architectural design.

## Base Properties

All OAS elements share common base properties:

### Identifier

Every element must have a unique identifier within its scope.

```json
{
  "id": "unique-identifier"
}
```

### Name

Elements can have human-readable names:

```json
{
  "name": "Living Room"
}
```

### Properties

Elements can have custom properties using the `x-` prefix:

```json
{
  "x-custom-property": "value"
}
```

## Units

All measurements in OAS use millimeters (mm) as the base unit. This provides:

- Consistent precision across all elements
- Compatibility with architectural standards
- Easy conversion to other units

## Data Types

OAS uses standard JSON data types:

### String

Text values, used for identifiers, names, and descriptive fields.

```json
"id": "room-1"
```

### Number

Numeric values for coordinates, dimensions, and measurements.

```json
"thickness": 200
```

### Object

Key-value pairs for structured data.

```json
{
  "x": 0,
  "y": 0
}
```

### Array

Ordered lists of values.

```json
[
  {"x": 0, "y": 0},
  {"x": 5000, "y": 0}
]
```

### Boolean

True or false values.

```json
"visible": true
```

## Validation

OAS documents should be validated to ensure:

1. Required properties are present
2. Data types are correct
3. Values are within acceptable ranges
4. References between elements are valid

## Best Practices

!!! tip "Naming Conventions"
    Use descriptive, kebab-case identifiers: `living-room`, `north-wall`, `main-entrance`

!!! tip "Organization"
    Group related elements together in the JSON structure for better readability

!!! tip "Documentation"
    Include metadata in all production documents to track versions and changes

## Next Steps

- Learn about [Geometry](geometry.md) for coordinate systems and shapes
- Understand [Program](program.md) for room types and usage
- Explore [Layout](layout.md) for complete architectural designs
