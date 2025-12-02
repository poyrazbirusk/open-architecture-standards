# Layout

This page describes how to define complete architectural layouts using OAS.

## Overview

A **layout** is the top-level container for all architectural elements in an OAS document. It combines geometry, program, and metadata to represent a complete design.

## Layout Object

The layout object is the main content container in an OAS document:

```json
{
  "version": "1.0.0",
  "layout": {
    "id": "apartment-layout",
    "name": "Two Bedroom Apartment",
    "units": "mm",
    "rooms": [...],
    "walls": [...],
    "openings": [...]
  }
}
```

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `id` | string | Yes | Unique layout identifier |
| `name` | string | No | Human-readable layout name |
| `units` | string | No | Measurement units (default: "mm") |
| `rooms` | array | No | Array of room objects |
| `walls` | array | No | Array of wall objects |
| `openings` | array | No | Array of opening objects |

## Rooms

Rooms are enclosed spaces within the layout, defined by their boundaries.

### Room Object

```json
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
}
```

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `id` | string | Yes | Unique room identifier |
| `name` | string | No | Room name |
| `program` | string | No | Room program/type |
| `boundaries` | array | Yes | Array of points defining room boundary |
| `area` | number | No | Room area in square millimeters |
| `properties` | object | No | Additional custom properties |

### Room Example

```json
{
  "id": "bedroom-1",
  "name": "Master Bedroom",
  "program": "bedroom",
  "boundaries": [
    {"x": 0, "y": 0},
    {"x": 4000, "y": 0},
    {"x": 4000, "y": 4000},
    {"x": 0, "y": 4000}
  ],
  "area": 16000000,
  "x-floor-material": "hardwood",
  "x-ceiling-height": 2800
}
```

## Walls

Walls are linear elements that define boundaries and partitions.

### Wall Object

```json
{
  "id": "wall-1",
  "thickness": 200,
  "start": {"x": 0, "y": 0},
  "end": {"x": 6000, "y": 0},
  "height": 2800,
  "material": "concrete"
}
```

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `id` | string | Yes | Unique wall identifier |
| `thickness` | number | Yes | Wall thickness in millimeters |
| `start` | object | Yes | Starting coordinate point |
| `end` | object | Yes | Ending coordinate point |
| `height` | number | No | Wall height in millimeters |
| `material` | string | No | Wall material type |

### Wall Types

**Exterior Walls**: Typically 200-300mm thick
```json
{
  "id": "exterior-north",
  "thickness": 250,
  "material": "concrete",
  "start": {"x": 0, "y": 0},
  "end": {"x": 10000, "y": 0}
}
```

**Interior Walls**: Typically 100-150mm thick
```json
{
  "id": "partition-1",
  "thickness": 100,
  "material": "drywall",
  "start": {"x": 5000, "y": 0},
  "end": {"x": 5000, "y": 8000}
}
```

**Glass Walls**:
```json
{
  "id": "glass-partition",
  "thickness": 12,
  "material": "glass",
  "x-transparency": 0.9,
  "start": {"x": 3000, "y": 2000},
  "end": {"x": 6000, "y": 2000}
}
```

## Openings

Openings are gaps in walls for doors, windows, and passages.

### Opening Object

```json
{
  "id": "door-1",
  "type": "door",
  "wall_id": "wall-1",
  "position": {"x": 3000, "y": 0},
  "width": 900,
  "height": 2100,
  "properties": {
    "swing": "inward",
    "material": "wood"
  }
}
```

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `id` | string | Yes | Unique opening identifier |
| `type` | string | Yes | Opening type (door, window, passage) |
| `wall_id` | string | Yes | Reference to parent wall |
| `position` | object | Yes | Position along the wall |
| `width` | number | Yes | Opening width in millimeters |
| `height` | number | No | Opening height in millimeters |
| `properties` | object | No | Additional properties |

### Opening Types

**Doors**:
```json
{
  "id": "entry-door",
  "type": "door",
  "wall_id": "exterior-south",
  "position": {"x": 5000, "y": 0},
  "width": 1000,
  "height": 2200,
  "properties": {
    "swing": "inward",
    "material": "steel",
    "lockable": true
  }
}
```

**Windows**:
```json
{
  "id": "window-1",
  "type": "window",
  "wall_id": "exterior-east",
  "position": {"x": 2000, "y": 8000},
  "width": 1500,
  "height": 1200,
  "properties": {
    "sill-height": 900,
    "operable": true
  }
}
```

**Passages** (open connections):
```json
{
  "id": "passage-1",
  "type": "passage",
  "wall_id": "partition-1",
  "position": {"x": 5000, "y": 3000},
  "width": 1200,
  "height": 2400
}
```

## Complete Layout Example

```json
{
  "version": "1.0.0",
  "metadata": {
    "title": "Studio Apartment",
    "description": "Compact studio with separate kitchen",
    "author": "OAS User",
    "created": "2024-01-01T00:00:00Z"
  },
  "layout": {
    "id": "studio-01",
    "name": "Studio Apartment Layout",
    "units": "mm",
    "rooms": [
      {
        "id": "living-area",
        "name": "Living Area",
        "program": "living",
        "boundaries": [
          {"x": 0, "y": 0},
          {"x": 5000, "y": 0},
          {"x": 5000, "y": 4000},
          {"x": 0, "y": 4000}
        ]
      },
      {
        "id": "kitchen",
        "name": "Kitchen",
        "program": "kitchen",
        "boundaries": [
          {"x": 5000, "y": 0},
          {"x": 7000, "y": 0},
          {"x": 7000, "y": 3000},
          {"x": 5000, "y": 3000}
        ]
      },
      {
        "id": "bathroom",
        "name": "Bathroom",
        "program": "bathroom",
        "boundaries": [
          {"x": 5000, "y": 3000},
          {"x": 7000, "y": 3000},
          {"x": 7000, "y": 4000},
          {"x": 5000, "y": 4000}
        ]
      }
    ],
    "walls": [
      {
        "id": "partition-kitchen",
        "thickness": 100,
        "start": {"x": 5000, "y": 0},
        "end": {"x": 5000, "y": 4000}
      },
      {
        "id": "partition-bathroom",
        "thickness": 100,
        "start": {"x": 5000, "y": 3000},
        "end": {"x": 7000, "y": 3000}
      }
    ],
    "openings": [
      {
        "id": "kitchen-passage",
        "type": "passage",
        "wall_id": "partition-kitchen",
        "position": {"x": 5000, "y": 1500},
        "width": 1000,
        "height": 2200
      },
      {
        "id": "bathroom-door",
        "type": "door",
        "wall_id": "partition-bathroom",
        "position": {"x": 6000, "y": 3000},
        "width": 800,
        "height": 2100,
        "properties": {
          "swing": "inward"
        }
      }
    ]
  }
}
```

## Layout Validation

A valid layout should:

1. **Have unique IDs**: All elements must have unique identifiers
2. **Valid references**: Opening `wall_id` must reference existing walls
3. **Closed boundaries**: Room boundaries must form closed polygons
4. **Non-overlapping rooms**: Rooms should not overlap (unless intentional)
5. **Consistent units**: All measurements in the same unit system

## Layout Properties

Additional layout-level properties can be specified:

```json
{
  "layout": {
    "id": "building-a",
    "name": "Building A - Ground Floor",
    "units": "mm",
    "x-floor-level": 0,
    "x-building-code": "IBC-2021",
    "x-gross-area": 150000000,
    "x-net-area": 120000000,
    "rooms": [...],
    "walls": [...],
    "openings": [...]
  }
}
```

## Multi-Level Layouts

For multi-story buildings, use separate layout documents or custom properties:

```json
{
  "layouts": [
    {
      "id": "ground-floor",
      "name": "Ground Floor",
      "x-level": 0,
      "rooms": [...]
    },
    {
      "id": "second-floor",
      "name": "Second Floor",
      "x-level": 1,
      "rooms": [...]
    }
  ]
}
```

## Best Practices

!!! tip "Organization"
    Group related elements together in your JSON structure

!!! tip "IDs"
    Use descriptive, consistent ID naming: `bedroom-1`, `bedroom-2`, etc.

!!! tip "Metadata"
    Always include metadata for production layouts

!!! tip "Validation"
    Validate layouts before use to catch errors early

## Next Steps

- See [Examples](examples/simple_plan.md) for complete layout examples
- Learn about [Render](render.md) for visualization
- Explore [Extensions](extensions.md) for advanced features
