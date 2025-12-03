# OAS-Program

OAS-Program defines the **high-level design intent layer** of the Open Architecture Standards.  
While OAS-Core and OAS-Geometry describe *what exists* in a plan, OAS-Program describes *what the plan should achieve*.

This module is typically used by:
- LLMs generating architectural layouts from natural-language prompts
- Automated layout solvers
- User-facing design tools
- Constraint validation systems

OAS-Program allows a design to be expressed in conceptual terms—areas, adjacencies, requirements—without committing to specific geometry.

---

## 1. Purpose of OAS-Program

The goals of OAS-Program are:

1. Represent desired spatial functions  
2. Describe functional relationships between spaces  
3. Encode design constraints  
4. Provide a stable input format for layout generation  
5. Support iterative editing of design intent  

It answers questions like:

- *How big should the living room be?*  
- *Which rooms require daylight?*  
- *Which spaces must be adjacent?*  
- *What are the circulation requirements?*  
- *What are the user’s goals for the design?*

---

## 2. Structure of an OAS-Program Document

A typical OAS-Program document contains:

- **program metadata**
- **design goals**
- **room requirements**
- **adjacency constraints**
- **circulation rules**
- **global constraints**
- **notes & reasoning (optional)**

### Example Structure

```json
{
  "oas_program": "1.0.0",
  "plan_id": "apt_01",
  "design_goal": "Two-bedroom apartment with a south-facing living area.",
  "global_constraints": {
    "target_area_m2": 75,
    "max_area_m2": 85
  },
  "rooms": [
    {
      "id": "living_kitchen",
      "usage": "living_kitchen",
      "desired_area_m2": { "min": 25, "max": 35 },
      "must_have": ["daylight", "balcony_access"],
      "adjacency": {
        "must_touch": ["entry"],
        "nice_to_touch": ["bedroom_1"]
      }
    }
  ]
}
```

---

## 3. Program Metadata

Fields:

- **oas_program** — fixed version string  
- **plan_id** — links program → layout  
- **title** (optional)  
- **description** (optional)  

Metadata should be stable throughout the design lifecycle.

---

## 4. Design Goals

A natural-language sentence describing the intent of the project.

Example:

```
“A compact 2-bedroom layout optimized for daylight and cross-ventilation.”
```

This field helps LLMs maintain context.

---

## 5. Global Constraints

Global constraints describe project-wide requirements.

Common fields:

- **target_area_m2**
- **max_area_m2**
- **min_area_m2**
- **orientation_preference** (e.g., "living spaces south")
- **climate** ("temperate", "hot-dry", etc.)
- **accessibility_level** ("basic", "universal")

Example:

```json
{
  "target_area_m2": 80,
  "orientation_preference": "living rooms facing south"
}
```

---

## 6. Room Requirements

Each room has a block describing its intended purpose and constraints.

### Fields

- **id** — stable identifier  
- **usage** — functional category (bedroom, kitchen, circulation, etc.)  
- **desired_area_m2** — min/max or exact  
- **must_have** — boolean features  
- **should_have** — softer requirements  
- **adjacency** — spatial relationships  
- **avoid** — things this room shouldn't touch  

### Example

```json
{
  "id": "bedroom_1",
  "usage": "bedroom",
  "desired_area_m2": { "min": 10, "max": 14 },
  "must_have": ["daylight"],
  "adjacency": {
    "must_touch": ["corridor"],
    "avoid_touch": ["living_kitchen"]
  }
}
```

---

## 7. Adjacency Rules

Adjacency rules describe spatial relationships qualitatively.

### Relationship Types

- **must_touch** — direct physical adjacency required  
- **should_touch** — recommended  
- **avoid_touch** — should not share a boundary  
- **must_connect_via** — defines circulation paths  

Example:

```json
"adjacency": {
  "must_touch": ["bathroom"],
  "avoid_touch": ["kitchen"]
}
```

---

## 8. Circulation Rules

Defines how rooms should connect through paths.

Common rules:

- `"entry"` must connect to all living spaces  
- Bedrooms must be reachable without passing through other bedrooms  
- Bathrooms must be accessible from shared spaces  

Example:

```json
{
  "circulation": {
    "primary_entry": "entry",
    "rules": [
      "All rooms must connect to entry with at most 3 steps.",
      "Bathroom must be reachable without crossing a bedroom."
    ]
  }
}
```

---

## 9. Constraint Strength

Requirements can be categorized:

- **hard constraints** — must be satisfied
- **soft constraints** — solver/LLM can trade off
- **preferences** — ideal but not necessary

This allows high-quality generative design.

---

## 10. Notes and Reasoning (LLM-friendly)

OAS-Program allows an optional `rationale` field:

```json
"rationale": "Bedroom 1 should touch the corridor for privacy."
```

This helps LLMs maintain context across revisions.

---

## 11. Summary

OAS-Program provides:

- a structured, machine-readable way to describe design intent  
- flexible room-level and global constraints  
- adjacency and circulation rules  
- LLM- and solver-friendly formatting  
- stable IDs for iterative editing  

It is the **starting point** for generating OAS-Layout geometries.
