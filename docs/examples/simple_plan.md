# Example: Simple OAS Plan

This example demonstrates the **minimal valid layout** in the Open Architecture Standards (OAS).  
It defines a single rectangular room using millimeter-precise geometry and no additional extensions.

The purpose of this example is to show:
- baseline JSON structure  
- required fields  
- boundary polygon formatting  
- unit conventions  

---

## 1. Description

This example represents a generic room with:

- 4 × 3 meters internal area  
- rectangular geometry  
- no walls defined explicitly (room polygon is enough)  
- no openings  
- minimal metadata  

It shows how to express the smallest meaningful architectural space in OAS.

---

## 2. JSON Example

```json
{
  "oas": "1.0.0",
  "plan_id": "simple_01",
  "title": "Simple Room Example",
  "units": { "length": "mm", "angle": "deg" },

  "rooms": [
    {
      "id": "room_01",
      "name": "Generic Room",
      "usage": "generic",

      "boundary_polygon": {
        "unit": "mm",
        "closed": true,
        "points": [
          { "x": 0, "y": 0 },
          { "x": 4000, "y": 0 },
          { "x": 4000, "y": 3000 },
          { "x": 0, "y": 3000 }
        ]
      },

      "area_m2": 12.0,
      "tags": []
    }
  ]
}
```

---

## 3. Explanation

### **oas**
Specifies the version of the OAS standard used.

### **plan_id**
Unique identifier. Links to potential OAS-Program or OAS-Layout files.

### **units**
Defines:
- millimeters for geometry  
- degrees for angles  

### **rooms**
A list of room objects.  
This example uses only one.

### **boundary_polygon**
Defines the room perimeter using integer millimeter coordinates.

### **area_m2**
Derived value (m²) allowed to be decimal.

---

## 4. Visual Interpretation

The JSON above corresponds to a 4 m × 3 m rectangular room:

```
+------------------------ 4000 mm ------------------------+
|                                                         |
|                                                         |
|                                                         | 3000 mm
|                                                         |
|                                                         |
+---------------------------------------------------------+
```

---

## 5. Notes

- This is the **simplest valid OAS geometric example**.  
- Additional elements (walls, openings, metadata) can be added later.  
- All geometry must remain integer mm values.  

---

## 6. Summary

This example illustrates:

- minimal OAS structure  
- a single rectangular room  
- proper use of OAS-Geometry conventions  
- clean, LLM-friendly JSON formatting  

This template is recommended for testing OAS compliance or starting new plans.
