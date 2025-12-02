# Geometry

This page describes the geometric elements and coordinate system used in OAS.

## Coordinate System

OAS uses a 2D Cartesian coordinate system with millimeter precision.

### Origin Point

The origin (0, 0) represents a reference point in the layout, typically:

- Bottom-left corner of the building
- Center point of the site
- A defined reference point in the architectural plans

### Axes

- **X-axis**: Horizontal direction (typically West to East)
- **Y-axis**: Vertical direction (typically South to North)
- **Units**: Millimeters (mm)

### Example

```json
{
  "x": 0,
  "y": 0
}
```

This represents a point at the origin.

## Points

A point is the fundamental geometric element, represented by X and Y coordinates.

### Point Object

```json
{
  "x": 5000,
  "y": 3000
}
```

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `x` | number | Yes | X-coordinate in millimeters |
| `y` | number | Yes | Y-coordinate in millimeters |

### Example Points

```json
// Origin point
{"x": 0, "y": 0}

// Point 5 meters east, 3 meters north
{"x": 5000, "y": 3000}

// Negative coordinates (west or south of origin)
{"x": -2000, "y": -1000}
```

## Lines

A line is defined by two points: start and end.

### Line Definition

```json
{
  "start": {"x": 0, "y": 0},
  "end": {"x": 5000, "y": 0}
}
```

This represents a horizontal line 5 meters long.

## Polygons

Polygons are defined by an array of points that form a closed shape.

### Polygon Definition

```json
{
  "boundaries": [
    {"x": 0, "y": 0},
    {"x": 5000, "y": 0},
    {"x": 5000, "y": 4000},
    {"x": 0, "y": 4000}
  ]
}
```

This represents a rectangle with:
- Width: 5000mm (5 meters)
- Height: 4000mm (4 meters)

### Winding Order

Polygons should follow a consistent winding order:

- **Counter-clockwise**: Exterior boundaries
- **Clockwise**: Interior boundaries (holes)

### Valid Polygons

A valid polygon must:

1. Have at least 3 points
2. Not self-intersect
3. Have the last point implicitly connecting to the first

## Shapes

Common architectural shapes can be represented using polygons.

### Rectangle

```json
{
  "boundaries": [
    {"x": 0, "y": 0},
    {"x": 6000, "y": 0},
    {"x": 6000, "y": 4000},
    {"x": 0, "y": 4000}
  ]
}
```

### L-Shape

```json
{
  "boundaries": [
    {"x": 0, "y": 0},
    {"x": 6000, "y": 0},
    {"x": 6000, "y": 3000},
    {"x": 3000, "y": 3000},
    {"x": 3000, "y": 5000},
    {"x": 0, "y": 5000}
  ]
}
```

### Irregular Shape

```json
{
  "boundaries": [
    {"x": 0, "y": 0},
    {"x": 4000, "y": 500},
    {"x": 5000, "y": 3000},
    {"x": 3000, "y": 4000},
    {"x": 0, "y": 3500}
  ]
}
```

## Dimensions

Elements can specify explicit dimensions:

### Thickness

Used for walls and other linear elements:

```json
{
  "thickness": 200  // 200mm thick wall
}
```

### Width and Height

Used for openings (doors, windows):

```json
{
  "width": 900,   // 900mm wide door
  "height": 2100  // 2100mm high door
}
```

### Area

Can be specified or calculated for rooms:

```json
{
  "area": 20000000  // 20 square meters in square millimeters
}
```

## Transformations

While not explicitly part of the base specification, geometric transformations can be applied:

### Translation

Moving an element by an offset:

```
new_x = x + offset_x
new_y = y + offset_y
```

### Rotation

Rotating around a point (typically the origin):

```
new_x = x * cos(θ) - y * sin(θ)
new_y = x * sin(θ) + y * cos(θ)
```

### Scaling

Scaling from a reference point:

```
new_x = reference_x + (x - reference_x) * scale
new_y = reference_y + (y - reference_y) * scale
```

## Precision

All coordinates should maintain millimeter precision:

- Integer values for whole millimeters
- Floating-point values for sub-millimeter precision when needed

```json
// Integer precision
{"x": 5000, "y": 3000}

// Sub-millimeter precision
{"x": 5000.5, "y": 3000.25}
```

## Geometric Calculations

### Distance Between Points

```
distance = sqrt((x2 - x1)² + (y2 - y1)²)
```

### Polygon Area

For a polygon with vertices (x₁, y₁), (x₂, y₂), ..., (xₙ, yₙ):

```
area = 0.5 * |Σ(xᵢ * yᵢ₊₁ - xᵢ₊₁ * yᵢ)|
```

### Line Length

```
length = sqrt((end.x - start.x)² + (end.y - start.y)²)
```

## Next Steps

- Understand [Program](program.md) for room classifications
- Learn about [Layout](layout.md) for complete designs
- See [Examples](examples/simple_plan.md) for practical geometry usage
