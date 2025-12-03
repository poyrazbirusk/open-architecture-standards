# OAS-Render

OAS-Render defines the **visualization guidelines** for converting OAS-Layout geometry into graphical output formats.  
While OAS-Layout provides exact spatial data in millimeters, OAS-Render describes *how that data should be displayed* in:

- **SVG**
- **Canvas 2D**
- **WebGL**
- **PDF**
- **Raster exports**

This module ensures that different tools render OAS plans with consistent visual meaning while allowing stylistic customization.

---

## 1. Purpose of OAS-Render

The goals of OAS-Render are:

- Provide a standard mapping from abstract geometry to graphical primitives  
- Ensure consistent interpretation across rendering engines  
- Make architectural plans visually clear and readable  
- Support real-time and static rendering pipelines  
- Support styling via CSS or shader overrides  

OAS-Render does **not** define aesthetics, but defines **defaults** and **mapping rules** that renderers must follow.

---

## 2. Rendering Components Overview

Rendering is based on OAS-Layout elements:

| OAS Entity | Rendered As | Notes |
|------------|-------------|-------|
| Room | Polygon | Fill + border |
| Wall | Line or thick line | Thickness in mm |
| Opening (door/window) | Rect/line segment | Placement tied to wall |
| Circulation | Paths/arrows | Optional layer |
| Tags/IDs | Labels | Optional |

The visual layers should align 1:1 with layout geometry.

---

## 3. Coordinate Mapping

OAS uses integer millimeters. Renderers must convert mm to pixels using a **scale factor**.

Example:

```
1 px = 2 mm  (for full-plan view)
1 px = 1 mm  (for detail views)
```

Scaling must preserve aspect ratio and orientation:

- X → right  
- Y → up (default architectural plan orientation)  

If using screen coordinates (y → down), renderer must invert Y internally.

---

## 4. SVG Rendering Guidelines

SVG is the recommended reference format due to:

- infinite scalability  
- human-readable structure  
- layering through `<g>` groups  
- CSS styling  

### 4.1 SVG Group Structure

Recommended grouping:

```svg
<g id="oas-rooms">...</g>
<g id="oas-walls">...</g>
<g id="oas-openings">...</g>
<g id="oas-circulation">...</g>
<g id="oas-labels">...</g>
```

### 4.2 Rooms

Render rooms as `<polygon>` elements.

Attributes:

- `fill` (default: none or light tint)
- `stroke` (default: #000)
- `stroke-width`

Example:

```svg
<polygon points="0,0 5000,0 5000,3000 0,3000"
         fill="#f8f8f8"
         stroke="#000"
         stroke-width="50"/>
```

### 4.3 Walls

Walls can be rendered in two ways:

1. **As lines with stroke-width = wall thickness**
2. **As polygons** (for full accuracy)

Example (simple):

```svg
<line x1="0" y1="0" x2="5000" y2="0" stroke="#000" stroke-width="200"/>
```

### 4.4 Openings

Doors and windows should be placed relative to wall coordinates.

Door example:

```svg
<rect x="1200" y="0" width="900" height="50" fill="#000"/>
```

Windows may use height offsets + sill height.

---

## 5. Canvas 2D Rendering Guidelines

Canvas is suitable for interactive editors.

### Key Rules:

- Use mm → px scaling
- Maintain OAS coordinate orientation
- Render in layers (rooms → walls → openings → labels)

Canvas example (in pseudocode):

```
ctx.beginPath()
ctx.moveTo(x1, y1)
ctx.lineTo(x2, y2)
ctx.lineWidth = wall.thickness_mm * scale
ctx.stroke()
```

### Labels

Rooms should have labels (centered):

```
ctx.fillText(room.name, cx, cy)
```

---

## 6. WebGL Rendering Guidelines

WebGL is used for interactive and high-performance rendering.  
OAS-Render provides guidelines for mapping geometric primitives to buffers:

- Rooms → triangle meshes
- Walls → extruded polygons
- Openings → boolean cutouts or overlays

### WebGL recommendations:

- Keep coordinates in world units = millimeters  
- Use shaders for styling  
- Use transform matrices for zoom/pan  
- Consider GPU instancing for large plans  

---

## 7. Default Visual Styling (Optional)

Defaults are recommended but not enforced:

### Rooms
- Fill: `#f8f8f8`
- Border: `#333`
- Border width: `50 mm`

### Walls
- Color: `#000`
- Thickness: from `thickness_mm`

### Openings
- Doors: black or dark gray rectangles
- Windows: blue or light gray

### Labels
- Font: sans-serif  
- Size: proportional to room  

Renderers may override styling through:
- CSS
- Theme files
- Shader uniforms

---

## 8. Layers and Z-Ordering

Recommended draw order:

1. Room fills  
2. Room boundaries  
3. Walls  
4. Openings  
5. Circulation  
6. Labels  
7. Annotations  

This ensures clarity and prevents overlaps from hiding important elements.

---

## 9. Interaction Support (Optional)

OAS-Render may provide optional interaction bindings:

- Select room by clicking its polygon
- Highlight walls on hover
- Show opening metadata on click
- Drag-to-move in editors
- Tooltips for area values

These interactions rely on referencing the `id` fields from OAS-Layout.

---

## 10. Export Guidelines

Renderers should support export to:

- SVG (preferred)
- PNG/JPEG (raster)
- PDF (vector)
- WebGL snapshots (canvas → image)

All exports must preserve:

- scale  
- line thickness  
- text positions  

---

## 11. Summary

OAS-Render defines:

- how to visualize millimeter-precise geometry  
- consistent mappings from layout → graphics  
- recommended groupings, layers, and styles  
- SVG, Canvas, and WebGL conventions  
- optional interactivity guidelines  

It ensures that any renderer can present an OAS layout consistently and clearly.
