# OAS-Extensions

OAS-Extensions defines the **modular expansion system** for the Open Architecture Standards.  
While OAS-Core establishes the essential schema, Extensions allow projects to add **domain-specific functionality** without altering the core standard.

Extensions ensure that OAS can evolve to support:
- furniture
- MEP (mechanical, electrical, plumbing)
- 3D geometry
- site plans
- materials
- environmental data
- accessibility metadata
- custom organization-specific modules

Each extension is versioned independently and integrates cleanly with OAS-Core and OAS-Geometry.

---

## 1. Purpose of OAS Extensions

Extensions serve to:

- Add optional capabilities  
- Remain backward-compatible  
- Avoid bloating the core specification  
- Enable specialized workflows  
- Allow communities to define their own modules  

OAS encourages a **modular ecosystem**, similar to:
- OpenAPI extensions  
- IFC partial schemas  
- Web standards “levels”  

Extensions must never break the guarantees provided by OAS-Core.

---

## 2. Extension Naming & Versioning

Extensions use the following naming pattern:

```
oas-{domain}-{version}
```

Examples:

- `oas-furniture-1.0.0`
- `oas-mep-1.0.0`
- `oas-3d-1.0.0`
- `oas-materials-1.1.0`
- `oas-site-0.9.0`

### Versioning Rules
- Must follow **semantic versioning** (semver).  
- Must specify compatibility with `oas` core version.  
- Minor versions may add fields.  
- Major versions may break extension internals, but never OAS-Core rules.

---

## 3. Extension Declaration

An OAS document may include extensions via the `extensions` field.

### Example:

```json
{
  "oas": "1.0.0",
  "extensions": [
    { "name": "oas-furniture", "version": "1.0.0" },
    { "name": "oas-3d", "version": "1.0.0" }
  ]
}
```

The presence of an extension implies:

- Additional fields may be used  
- Additional entities may be allowed  
- Renderers/editors should load the relevant extension handlers  

Documents must still remain valid OAS regardless of extensions.

---

## 4. Extension Structure Requirements

Every extension must include:

### 4.1 Metadata
- extension name  
- version  
- description  
- authors (optional)

### 4.2 Entities
The extension must define its own entities using OAS-style patterns:
- JSON objects  
- snake_case keys  
- mm-based coordinates (when geometric)  
- integer geometry rules must be respected

### 4.3 Integration Rules
Extensions must define:
- what core entities they modify or reference  
- how they interact with layout or render modules  
- any conflicts or invariants  

---

## 5. Official OAS Extensions (Initial Set)

Below are recommended baseline extensions that the ecosystem may adopt.

---

### 5.1 OAS-Furniture

Defines furniture elements placed inside rooms.

Includes:
- bounding polygons or footprints  
- rotation  
- clearance zones  
- category (bed, sofa, table)  

Example furniture entity:

```json
{
  "type": "bed",
  "id": "bed_01",
  "position": { "x": 1200, "y": 2400 },
  "rotation_deg": 0,
  "footprint": {
    "points": [
      { "x": 0, "y": 0 },
      { "x": 2000, "y": 0 },
      { "x": 2000, "y": 1600 },
      { "x": 0, "y": 1600 }
    ]
  }
}
```

---

### 5.2 OAS-MEP

Mechanical, electrical, plumbing representations.

May include:
- ducts  
- pipes  
- electrical circuits  
- fixtures  
- mechanical units  
- diagrams for drainage or supply  

All geometry still uses mm integer rules.

---

### 5.3 OAS-3D

Adds a 3D layer using extrusions and heights.

Includes:
- floor heights  
- ceiling heights  
- extruded wall geometry  
- vertical openings  
- 3D furniture  

Example:

```json
{
  "wall_height_mm": 2800,
  "ceiling_height_mm": 2550
}
```

---

### 5.4 OAS-Materials

Describes materials, finishes, and construction types.

Examples:
- wall materials  
- flooring types  
- reflectivity parameters  
- thermal properties  

Example:

```json
{
  "material_id": "wall_paint_white",
  "type": "paint",
  "color_hex": "#ffffff",
  "reflectance": 0.72
}
```

---

### 5.5 OAS-Site

Defines the building context:

- property boundaries  
- setbacks  
- orientation (north arrow)  
- slope data  
- topography  
- access points  

Example:

```json
{
  "north_angle_deg": 0,
  "site_boundary_polygon": { ... }
}
```

---

## 6. Custom Extensions

Projects may define custom extensions:

Example:

```
oas-hospital
oas-retail
oas-lab
oas-classroom
```

Custom modules should:

- follow naming conventions  
- use semver  
- not break OAS-Core invariants  
- provide clear documentation  

---

## 7. Render Integrations

Extensions may include *render hints*, such as:

```json
{
  "color_hex": "#55aaff",
  "icon": "furniture-bed"
}
```

These are optional and renderer-specific.

---

## 8. Interaction With OAS-Core, Geometry, Layout

### Extensions **may not**:

- override core geometry rules  
- change mm-integer coordinate rules  
- redefine base types (room, wall, opening)

### Extensions **may**:

- attach metadata to core entities  
- introduce new entity types  
- define reference relationships  
- add new layers for visualization  

---

## 9. Summary

OAS-Extensions provide a structured, modular way to expand the core Open Architecture Standards without breaking compatibility.

Extensions:
- add optional capabilities  
- define specialized behavior  
- support complex domains (furniture, MEP, 3D, site)  
- keep OAS lean, stable, and future-proof  

Extensions empower OAS to support both simple layouts and highly complex architectural models.
