# Simple Plan Example

This example demonstrates a basic single-room layout using OAS.

## Overview

This example shows a simple rectangular office space with basic walls and one entrance door. It's the most straightforward OAS document you can create.

## Complete Example

```json
{
  "version": "1.0.0",
  "metadata": {
    "title": "Simple Office",
    "description": "A basic single-room office space",
    "author": "OAS Tutorial"
  },
  "layout": {
    "id": "simple-office",
    "name": "Single Office",
    "units": "mm",
    "rooms": [
      {
        "id": "office-1",
        "name": "Office",
        "program": "office",
        "boundaries": [
          {"x": 0, "y": 0},
          {"x": 4000, "y": 0},
          {"x": 4000, "y": 3000},
          {"x": 0, "y": 3000}
        ],
        "area": 12000000
      }
    ],
    "walls": [
      {
        "id": "wall-north",
        "thickness": 200,
        "start": {"x": 0, "y": 0},
        "end": {"x": 4000, "y": 0},
        "height": 2800,
        "material": "drywall"
      },
      {
        "id": "wall-east",
        "thickness": 200,
        "start": {"x": 4000, "y": 0},
        "end": {"x": 4000, "y": 3000},
        "height": 2800,
        "material": "drywall"
      },
      {
        "id": "wall-south",
        "thickness": 200,
        "start": {"x": 4000, "y": 3000},
        "end": {"x": 0, "y": 3000},
        "height": 2800,
        "material": "drywall"
      },
      {
        "id": "wall-west",
        "thickness": 200,
        "start": {"x": 0, "y": 3000},
        "end": {"x": 0, "y": 0},
        "height": 2800,
        "material": "drywall"
      }
    ],
    "openings": [
      {
        "id": "entry-door",
        "type": "door",
        "wall_id": "wall-south",
        "position": {"x": 2000, "y": 3000},
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

## Breakdown

### Document Root

```json
{
  "version": "1.0.0",
  "metadata": {...},
  "layout": {...}
}
```

Every OAS document starts with these three elements:
- `version`: The OAS specification version
- `metadata`: Optional information about the document
- `layout`: The actual architectural content

### Metadata

```json
{
  "title": "Simple Office",
  "description": "A basic single-room office space",
  "author": "OAS Tutorial"
}
```

Metadata helps identify and describe the document. While optional, it's recommended for production documents.

### Layout Container

```json
{
  "id": "simple-office",
  "name": "Single Office",
  "units": "mm",
  "rooms": [...],
  "walls": [...],
  "openings": [...]
}
```

The layout contains:
- Unique identifier
- Human-readable name
- Unit specification (millimeters)
- Arrays of rooms, walls, and openings

### Room Definition

```json
{
  "id": "office-1",
  "name": "Office",
  "program": "office",
  "boundaries": [
    {"x": 0, "y": 0},
    {"x": 4000, "y": 0},
    {"x": 4000, "y": 3000},
    {"x": 0, "y": 3000}
  ],
  "area": 12000000
}
```

This defines a rectangular room:
- 4000mm (4m) wide
- 3000mm (3m) deep
- Area: 12 square meters (12,000,000 square millimeters)
- Program: "office" (office space)

### Wall Definitions

Each wall is defined by its start and end points:

**North Wall** (along X-axis at Y=0):
```json
{
  "id": "wall-north",
  "thickness": 200,
  "start": {"x": 0, "y": 0},
  "end": {"x": 4000, "y": 0},
  "height": 2800
}
```

Walls form a rectangle around the room:
- North: (0,0) to (4000,0)
- East: (4000,0) to (4000,3000)
- South: (4000,3000) to (0,3000)
- West: (0,3000) to (0,0)

### Opening Definition

```json
{
  "id": "entry-door",
  "type": "door",
  "wall_id": "wall-south",
  "position": {"x": 2000, "y": 3000},
  "width": 900,
  "height": 2100,
  "properties": {
    "swing": "inward"
  }
}
```

A standard office door:
- Located on the south wall
- Centered at X=2000mm (middle of 4000mm wall)
- 900mm wide (standard door width)
- 2100mm tall (standard door height)
- Swings inward into the office

## Visualization

Here's a simple ASCII representation:

```
North (Y=0)
┌─────────────────────────┐
│                         │ East (X=4000)
│       Office            │
│      4m × 3m            │
│                         │
│         [Door]          │
└────────────┬────────────┘
West (X=0)   South (Y=3000)
```

## Variations

### Add a Window

Add a window to the east wall:

```json
{
  "id": "window-1",
  "type": "window",
  "wall_id": "wall-east",
  "position": {"x": 4000, "y": 1500},
  "width": 1200,
  "height": 1000,
  "properties": {
    "sill-height": 900
  }
}
```

### Change Room Size

To make it a larger office (5m × 4m):

```json
{
  "boundaries": [
    {"x": 0, "y": 0},
    {"x": 5000, "y": 0},
    {"x": 5000, "y": 4000},
    {"x": 0, "y": 4000}
  ],
  "area": 20000000
}
```

### Add Custom Properties

Add furniture information:

```json
{
  "id": "office-1",
  "name": "Office",
  "program": "office",
  "boundaries": [...],
  "x-furniture": [
    {
      "type": "desk",
      "position": {"x": 2000, "y": 1500},
      "dimensions": {"width": 1500, "length": 750}
    }
  ]
}
```

## Best Practices

!!! tip "Start Simple"
    Begin with a single room and add complexity gradually

!!! tip "Check Coordinates"
    Verify that wall coordinates match room boundaries

!!! tip "Use Standards"
    Standard door width: 900mm, height: 2100mm

!!! tip "Validate"
    Ensure the room forms a closed polygon

## Next Steps

- View the [Multi-Room Plan](multi_room_plan.md) for a more complex example
- Review [Geometry](../geometry.md) for coordinate system details
- Learn about [Layout](../layout.md) for complete layout structures
- Explore [Program](../program.md) for room types

## Common Mistakes

### Unclosed Polygon

```json
// ❌ Wrong - doesn't close
"boundaries": [
  {"x": 0, "y": 0},
  {"x": 4000, "y": 0},
  {"x": 4000, "y": 3000}
  // Missing the fourth point!
]
```

### Wall Mismatch

```json
// ❌ Wrong - wall doesn't match room boundary
"start": {"x": 0, "y": 0},
"end": {"x": 3500, "y": 0}  // Room goes to x=4000!
```

### Invalid Reference

```json
// ❌ Wrong - references non-existent wall
{
  "type": "door",
  "wall_id": "wall-middle",  // This wall doesn't exist!
  ...
}
```

## File Download

[Download this example as JSON](simple_plan.json){ .md-button }

---

*This is a basic example to help you get started with OAS. For more complex layouts, see the [Multi-Room Plan Example](multi_room_plan.md).*
