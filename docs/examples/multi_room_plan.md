# Example: Multi-Room OAS Layout

This example demonstrates a **small apartment layout** defined using OAS-Core and OAS-Geometry.  
It includes multiple rooms, walls, and doors, showing how real architectural spaces are expressed in fully resolved geometry.

The purpose of this example is to illustrate:

- multi-room polygons  
- wall configurations  
- door placement using position-along-wall  
- how rooms relate through circulation  
- a consistent mm-based coordinate system  

This example can serve as a reference for testing solvers, renderers, and LLM-driven layout editors.

---

## 1. Description

This example describes a compact apartment consisting of:

- Entry hall  
- Living + kitchen area  
- Bedroom  
- Bathroom  
- Corridor  

Plan dimensions are simple rectangles connected by doors, all placed in mm coordinates.

---

## 2. JSON Example

```json
{
  "oas": "1.0.0",
  "plan_id": "multi_01",
  "title": "Multi-Room Apartment Example",
  "units": { "length": "mm", "angle": "deg" },

  "rooms": [
    {
      "id": "entry",
      "name": "Entry",
      "usage": "circulation",
      "boundary_polygon": {
        "unit": "mm",
        "closed": true,
        "points": [
          { "x": 0, "y": 0 },
          { "x": 2000, "y": 0 },
          { "x": 2000, "y": 1500 },
          { "x": 0, "y": 1500 }
        ]
      },
      "area_m2": 3.0
    },
    {
      "id": "living_kitchen",
      "name": "Living + Kitchen",
      "usage": "living_kitchen",
      "boundary_polygon": {
        "unit": "mm",
        "closed": true,
        "points": [
          { "x": 2000, "y": 0 },
          { "x": 6000, "y": 0 },
          { "x": 6000, "y": 4000 },
          { "x": 2000, "y": 4000 }
        ]
      },
      "area_m2": 16.0
    },
    {
      "id": "bedroom_01",
      "name": "Bedroom",
      "usage": "bedroom",
      "boundary_polygon": {
        "unit": "mm",
        "closed": true,
        "points": [
          { "x": 0, "y": 1500 },
          { "x": 2000, "y": 1500 },
          { "x": 2000, "y": 4000 },
          { "x": 0, "y": 4000 }
        ]
      },
      "area_m2": 5.0
    },
    {
      "id": "bathroom_01",
      "name": "Bathroom",
      "usage": "bathroom",
      "boundary_polygon": {
        "unit": "mm",
        "closed": true,
        "points": [
          { "x": 6000, "y": 1500 },
          { "x": 7500, "y": 1500 },
          { "x": 7500, "y": 2500 },
          { "x": 6000, "y": 2500 }
        ]
      },
      "area_m2": 2.25
    }
  ],

  "walls": [
    {
      "id": "wall_entry_left",
      "from": { "x": 0, "y": 0 },
      "to":   { "x": 0, "y": 4000 },
      "unit": "mm",
      "thickness_mm": 200,
      "adjacent_rooms": ["exterior", "entry", "bedroom_01"]
    },
    {
      "id": "wall_living_south",
      "from": { "x": 2000, "y": 0 },
      "to":   { "x": 6000, "y": 0 },
      "unit": "mm",
      "thickness_mm": 200,
      "adjacent_rooms": ["entry", "living_kitchen"]
    },
    {
      "id": "wall_bedroom_bottom",
      "from": { "x": 0, "y": 1500 },
      "to":   { "x": 2000, "y": 1500 },
      "unit": "mm",
      "thickness_mm": 200,
      "adjacent_rooms": ["entry", "bedroom_01"]
    },
    {
      "id": "wall_bathroom_left",
      "from": { "x": 6000, "y": 1500 },
      "to":   { "x": 6000, "y": 2500 },
      "unit": "mm",
      "thickness_mm": 150,
      "adjacent_rooms": ["living_kitchen", "bathroom_01"]
    }
  ],

  "openings": [
    {
      "id": "door_entry_to_living",
      "opening_type": "door",
      "in_wall": "wall_living_south",
      "connects_rooms": ["entry", "living_kitchen"],
      "position_along_wall_mm": 800,
      "width_mm": 900,
      "height_mm": 2100
    },
    {
      "id": "door_entry_to_bedroom",
      "opening_type": "door",
      "in_wall": "wall_bedroom_bottom",
      "connects_rooms": ["entry", "bedroom_01"],
      "position_along_wall_mm": 600,
      "width_mm": 800,
      "height_mm": 2100
    },
    {
      "id": "door_living_to_bathroom",
      "opening_type": "door",
      "in_wall": "wall_bathroom_left",
      "connects_rooms": ["living_kitchen", "bathroom_01"],
      "position_along_wall_mm": 400,
      "width_mm": 700,
      "height_mm": 2100
    }
  ],

  "openings_examples": [
    {
      "id": "window_living_north",
      "opening_type": "window",
      "is_fixed": false,
      "operation": "sliding",
      "slide_direction": "left-to-right",
      "slider_width_mm": 600,
      "in_wall": "wall_living_north",
      "position_along_wall_mm": 1500,
      "width_mm": 1200,
      "height_mm": 1200,
      "sill_height_mm": 900
    },
    {
      "id": "door_pantry",
      "opening_type": "door",
      "is_fixed": false,
      "operation": "swing",
      "swing_direction": "outward",
      "hinge_side": "right",
      "hinge_offset_mm": 80,
      "in_wall": "wall_kitchen_pantry",
      "position_along_wall_mm": 300,
      "width_mm": 700,
      "height_mm": 2100
    }
  ],

  "connections": [
    { "from": "entry",          "to": "living_kitchen", "type": "direct" },
    { "from": "entry",          "to": "bedroom_01",     "type": "direct" },
    { "from": "living_kitchen", "to": "bathroom_01",    "type": "direct" }
  ]
}
```

---

## 3. Explanation

### Rooms
Each room is defined by:
- a unique ID  
- usage category  
- polygon boundary in mm  
- derived area (m²)  

Geometries are simple rectangles to demonstrate structure.

### Walls
Walls connect the geometry between rooms and define:
- thickness  
- adjacency  
- structural boundary  

### Openings
Doors connect rooms through wall references using:
- `position_along_wall_mm`  
- width & height (mm)  

This demonstrates the OAS approach to parametric opening placement.

### Circulation
Rooms are connected using simple `"direct"` edges.

---

## 4. Visual Schematic (Not to Scale)

```
+-------------+-------------------------+
|   Bedroom   |        Living +         |
|    01       |         Kitchen         |
|             |                         |
+-------------+----- D ----+------------+
|           Entry          | Bathroom   |
|                          |    01      |
+--------------------------+------------+
```

---

## 5. Notes

- All coordinates use mm integers.  
- This example intentionally avoids complexity to keep it readable.  
- Renderers and editors can use this as a baseline dataset.  
- It validates the interplay between rooms, walls, and openings.  

---

## 6. Summary

This example provides a clear demonstration of:

- a multi-room apartment  
- valid OAS room polygons  
- wall and door geometry  
- consistent OAS-Layout structure  
- realistic circulation connections  

It is recommended for testing:
- render pipelines  
- LLM-based design tools  
- layout solvers  
- interoperability between systems
