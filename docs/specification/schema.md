# Schema Reference

This page provides a detailed reference for all OAS schema elements.

## Document Structure

### Root Object

The root object of an OAS document.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `version` | string | Yes | OAS specification version (e.g., "1.0.0") |
| `metadata` | object | No | Document metadata |
| `layout` | object | Yes | The architectural layout definition |

### Metadata Object

Optional metadata about the document.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `title` | string | No | Document title |
| `description` | string | No | Document description |
| `author` | string | No | Document author |
| `created` | string | No | Creation date (ISO 8601) |
| `modified` | string | No | Last modification date (ISO 8601) |

### Layout Object

The main layout definition.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `id` | string | Yes | Unique layout identifier |
| `name` | string | No | Human-readable layout name |
| `units` | string | No | Measurement units (default: "mm") |
| `rooms` | array | No | Array of room objects |
| `walls` | array | No | Array of wall objects |
| `openings` | array | No | Array of opening objects |

## Room Object

Defines a space or room in the layout.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `id` | string | Yes | Unique room identifier |
| `name` | string | No | Room name |
| `program` | string | No | Room program/type (e.g., "bedroom", "kitchen") |
| `boundaries` | array | Yes | Array of coordinate points defining the room boundary |
| `area` | number | No | Room area in square millimeters |
| `properties` | object | No | Additional custom properties |

### Boundaries Array

Array of coordinate points that define a room's boundary.

```json
"boundaries": [
  {"x": 0, "y": 0},
  {"x": 5000, "y": 0},
  {"x": 5000, "y": 4000},
  {"x": 0, "y": 4000}
]
```

## Wall Object

Defines a wall in the layout.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `id` | string | Yes | Unique wall identifier |
| `thickness` | number | Yes | Wall thickness in millimeters |
| `start` | object | Yes | Starting coordinate point |
| `end` | object | Yes | Ending coordinate point |
| `height` | number | No | Wall height in millimeters |
| `material` | string | No | Wall material type |

### Coordinate Object

Represents a point in 2D space.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `x` | number | Yes | X-coordinate in millimeters |
| `y` | number | Yes | Y-coordinate in millimeters |

## Opening Object

Defines doors, windows, and other openings.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `id` | string | Yes | Unique opening identifier |
| `type` | string | Yes | Opening type ("door", "window", "passage") |
| `wall_id` | string | Yes | Reference to parent wall |
| `position` | object | Yes | Position along the wall |
| `width` | number | Yes | Opening width in millimeters |
| `height` | number | No | Opening height in millimeters |
| `properties` | object | No | Additional properties (e.g., swing direction) |

## Example Schema

Here's a complete example showing all elements:

```json
{
  "version": "1.0.0",
  "metadata": {
    "title": "Sample Apartment Layout",
    "author": "OAS User",
    "created": "2024-01-01T00:00:00Z"
  },
  "layout": {
    "id": "apartment-01",
    "name": "Two Bedroom Apartment",
    "units": "mm",
    "rooms": [
      {
        "id": "living-room",
        "name": "Living Room",
        "program": "living",
        "boundaries": [
          {"x": 0, "y": 0},
          {"x": 6000, "y": 0},
          {"x": 6000, "y": 5000},
          {"x": 0, "y": 5000}
        ],
        "area": 30000000
      },
      {
        "id": "bedroom-01",
        "name": "Master Bedroom",
        "program": "bedroom",
        "boundaries": [
          {"x": 6000, "y": 0},
          {"x": 10000, "y": 0},
          {"x": 10000, "y": 4000},
          {"x": 6000, "y": 4000}
        ],
        "area": 16000000
      }
    ],
    "walls": [
      {
        "id": "wall-01",
        "thickness": 200,
        "start": {"x": 0, "y": 0},
        "end": {"x": 10000, "y": 0},
        "height": 2800,
        "material": "concrete"
      },
      {
        "id": "wall-02",
        "thickness": 100,
        "start": {"x": 6000, "y": 0},
        "end": {"x": 6000, "y": 5000},
        "height": 2800,
        "material": "drywall"
      }
    ],
    "openings": [
      {
        "id": "door-01",
        "type": "door",
        "wall_id": "wall-02",
        "position": {"x": 6000, "y": 2000},
        "width": 900,
        "height": 2100,
        "properties": {
          "swing": "inward",
          "material": "wood"
        }
      }
    ]
  }
}
```

## Data Types

### String
Text values, enclosed in double quotes.

### Number
Numeric values (integer or floating-point).

### Object
Key-value pairs enclosed in curly braces `{}`.

### Array
Ordered list of values enclosed in square brackets `[]`.

## Validation Rules

!!! warning "Required Properties"
    All properties marked as "Required: Yes" must be present in the document. Missing required properties will cause validation errors.

!!! tip "Coordinate Units"
    Always use millimeters for coordinates and dimensions. This ensures consistency across different implementations.

## Extensions

Custom properties can be added using the `x-` prefix:

```json
{
  "id": "room-01",
  "name": "Kitchen",
  "x-custom-property": "custom value",
  "x-furniture": ["table", "chairs"]
}
```
