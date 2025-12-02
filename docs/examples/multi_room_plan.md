# Multi-Room Plan Example

This example demonstrates a multi-room residential layout with rooms, walls, doors, and windows.

## Overview

This example shows a small apartment with three interconnected rooms:
- Living area (main space)
- Kitchen (cooking area)
- Bathroom (full bath)

## Complete Example

```json
{
  "version": "1.0.0",
  "metadata": {
    "title": "Studio Apartment",
    "description": "Compact studio apartment with separate kitchen and bathroom",
    "author": "OAS Tutorial",
    "created": "2024-01-01T00:00:00Z"
  },
  "layout": {
    "id": "studio-apartment-01",
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
        ],
        "area": 20000000,
        "x-ceiling-height": 2800
      },
      {
        "id": "kitchen",
        "name": "Kitchen",
        "program": "kitchen",
        "boundaries": [
          {"x": 5000, "y": 0},
          {"x": 7500, "y": 0},
          {"x": 7500, "y": 3000},
          {"x": 5000, "y": 3000}
        ],
        "area": 7500000,
        "x-ceiling-height": 2800
      },
      {
        "id": "bathroom",
        "name": "Bathroom",
        "program": "bathroom",
        "boundaries": [
          {"x": 5000, "y": 3000},
          {"x": 7500, "y": 3000},
          {"x": 7500, "y": 4000},
          {"x": 5000, "y": 4000}
        ],
        "area": 2500000,
        "x-ceiling-height": 2800
      }
    ],
    "walls": [
      {
        "id": "exterior-north",
        "thickness": 250,
        "start": {"x": 0, "y": 0},
        "end": {"x": 7500, "y": 0},
        "height": 2800,
        "material": "concrete",
        "x-insulation": "R-19"
      },
      {
        "id": "exterior-east",
        "thickness": 250,
        "start": {"x": 7500, "y": 0},
        "end": {"x": 7500, "y": 4000},
        "height": 2800,
        "material": "concrete",
        "x-insulation": "R-19"
      },
      {
        "id": "exterior-south",
        "thickness": 250,
        "start": {"x": 7500, "y": 4000},
        "end": {"x": 0, "y": 4000},
        "height": 2800,
        "material": "concrete",
        "x-insulation": "R-19"
      },
      {
        "id": "exterior-west",
        "thickness": 250,
        "start": {"x": 0, "y": 4000},
        "end": {"x": 0, "y": 0},
        "height": 2800,
        "material": "concrete",
        "x-insulation": "R-19"
      },
      {
        "id": "partition-kitchen",
        "thickness": 100,
        "start": {"x": 5000, "y": 0},
        "end": {"x": 5000, "y": 4000},
        "height": 2800,
        "material": "drywall"
      },
      {
        "id": "partition-bathroom",
        "thickness": 100,
        "start": {"x": 5000, "y": 3000},
        "end": {"x": 7500, "y": 3000},
        "height": 2800,
        "material": "drywall"
      }
    ],
    "openings": [
      {
        "id": "entry-door",
        "type": "door",
        "wall_id": "exterior-south",
        "position": {"x": 2500, "y": 4000},
        "width": 900,
        "height": 2100,
        "properties": {
          "swing": "inward",
          "material": "steel",
          "lockable": true
        }
      },
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
          "swing": "inward",
          "material": "wood",
          "privacy": true
        }
      },
      {
        "id": "living-window",
        "type": "window",
        "wall_id": "exterior-west",
        "position": {"x": 0, "y": 2000},
        "width": 1500,
        "height": 1200,
        "properties": {
          "sill-height": 800,
          "operable": true,
          "glass-type": "double-pane"
        }
      },
      {
        "id": "kitchen-window",
        "type": "window",
        "wall_id": "exterior-east",
        "position": {"x": 7500, "y": 1500},
        "width": 1200,
        "height": 1000,
        "properties": {
          "sill-height": 900,
          "operable": true,
          "glass-type": "double-pane"
        }
      }
    ]
  }
}
```

## Floor Plan

ASCII representation of the layout:

```
        North (Y=0)
   0        5000      7500
   ┌────────┬──────────┐
   │        │ Kitchen  │ 0
   │ Living │    ┌W┐   │
   │  Area  ├────┘ └───┤ 3000
   │   ┌W┐  │ Bathroom │
   │   └─┘  │    [D]   │
   └───[D]──┴──────────┘ 4000
   West    South    East

W = Window
[D] = Door
├──┘ = Passage
```

## Dimensions

| Room | Width | Depth | Area |
|------|-------|-------|------|
| Living Area | 5000mm (5m) | 4000mm (4m) | 20 m² |
| Kitchen | 2500mm (2.5m) | 3000mm (3m) | 7.5 m² |
| Bathroom | 2500mm (2.5m) | 1000mm (1m) | 2.5 m² |
| **Total** | | | **30 m²** |

## Key Features

### Room Adjacency

The layout demonstrates proper room adjacency:
- Kitchen adjacent to living area via open passage
- Bathroom adjacent to both kitchen and living area
- Entry door opens to living area

### Wall Types

**Exterior Walls** (250mm thick):
- Concrete construction
- R-19 insulation
- Weather-resistant

**Interior Partitions** (100mm thick):
- Drywall construction
- Sound dampening between spaces

### Opening Variety

**Entry Door**:
- 900mm wide (standard)
- Steel construction
- Lockable for security

**Kitchen Passage**:
- 1000mm wide opening
- No door (open plan)
- Enhanced flow between spaces

**Bathroom Door**:
- 800mm wide (bathroom standard)
- Privacy lock
- Wood construction

**Windows**:
- Living area: Large 1500mm window for natural light
- Kitchen: 1200mm window over sink area
- Both double-pane and operable

## Extensions Used

This example demonstrates several custom extensions:

### Ceiling Height
```json
"x-ceiling-height": 2800
```

### Insulation
```json
"x-insulation": "R-19"
```

### Door Properties
```json
"properties": {
  "swing": "inward",
  "material": "steel",
  "lockable": true
}
```

## Variations

### Add Closet Storage

```json
{
  "id": "closet",
  "name": "Storage Closet",
  "program": "storage",
  "boundaries": [
    {"x": 0, "y": 0},
    {"x": 1000, "y": 0},
    {"x": 1000, "y": 800},
    {"x": 0, "y": 800}
  ]
}
```

### Separate Bedroom

Convert to one-bedroom by partitioning the living area:

```json
{
  "id": "partition-bedroom",
  "thickness": 100,
  "start": {"x": 2500, "y": 0},
  "end": {"x": 2500, "y": 3000},
  "material": "drywall"
}
```

### Add Furniture

Kitchen appliances:

```json
{
  "id": "kitchen",
  "x-appliances": [
    {
      "type": "refrigerator",
      "position": {"x": 7000, "y": 200},
      "dimensions": {"width": 800, "depth": 700}
    },
    {
      "type": "stove",
      "position": {"x": 5500, "y": 200},
      "dimensions": {"width": 600, "depth": 600}
    },
    {
      "type": "sink",
      "position": {"x": 6500, "y": 200},
      "dimensions": {"width": 800, "depth": 500}
    }
  ]
}
```

## Design Considerations

### Code Compliance

!!! info "Building Codes"
    This layout follows typical residential building codes:
    - Bathroom ventilation via window
    - Kitchen work triangle consideration
    - Egress door width (900mm)
    - Window sizes for natural light

### Accessibility

To make this layout ADA-compliant:
- Widen bathroom door to 900mm
- Increase bathroom size to 1500mm × 2000mm
- Widen passage to 1200mm
- Add accessible bathroom fixtures

### Energy Efficiency

Features for energy efficiency:
- Exterior wall insulation (R-19)
- Double-pane windows
- Compact layout reduces heating/cooling needs

## Real-World Applications

This example demonstrates:

1. **Multi-room coordination**: Proper wall and room relationships
2. **Different opening types**: Doors, passages, windows
3. **Material specifications**: Different materials for different walls
4. **Custom properties**: Extended metadata for specific needs
5. **Proper references**: Opening-to-wall relationships

## Next Steps

- Compare with [Simple Plan](simple_plan.md) example
- Learn about [Program](../program.md) for room types
- Explore [Layout](../layout.md) for advanced features
- Review [Extensions](../extensions.md) for custom properties

## Validation Checklist

✅ All rooms have closed boundaries
✅ Wall coordinates match room boundaries
✅ Openings reference valid walls
✅ All IDs are unique
✅ Measurements are in millimeters
✅ Required properties are present

---

*This example represents a typical small apartment layout. Adjust dimensions and rooms to fit your specific needs.*
