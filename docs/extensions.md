# Extensions

This page describes how to extend OAS with custom properties and vendor-specific features.

## Overview

OAS is designed to be extensible, allowing you to add custom properties without breaking compatibility with standard tools. Extensions enable:

- Domain-specific metadata
- Vendor-specific features
- Experimental capabilities
- Integration with other systems

## Extension Naming

Custom properties must use the `x-` prefix to avoid conflicts with future standard properties.

### Valid Extensions

```json
{
  "id": "room-1",
  "name": "Living Room",
  "x-custom-property": "value",
  "x-vendor-specific": {...}
}
```

### Invalid Extensions

```json
{
  "id": "room-1",
  "name": "Living Room",
  "custom-property": "value",  // ❌ Missing x- prefix
  "vendorSpecific": {...}      // ❌ Missing x- prefix
}
```

## Common Extensions

### Material Properties

Specify material information for elements:

```json
{
  "id": "wall-1",
  "thickness": 200,
  "x-material": {
    "type": "concrete",
    "finish": "painted",
    "color": "#FFFFFF",
    "thermal-resistance": 2.5,
    "fire-rating": 120
  }
}
```

### Height Information

Add height data to elements:

```json
{
  "id": "room-1",
  "name": "Living Room",
  "boundaries": [...],
  "x-ceiling-height": 2800,
  "x-floor-elevation": 0,
  "x-ceiling-type": "suspended"
}
```

### Furniture and Fixtures

Include furniture and fixture data:

```json
{
  "id": "bedroom",
  "name": "Master Bedroom",
  "boundaries": [...],
  "x-furniture": [
    {
      "type": "bed",
      "model": "king",
      "position": {"x": 2000, "y": 2000},
      "rotation": 0,
      "dimensions": {"width": 1800, "length": 2000, "height": 600}
    },
    {
      "type": "nightstand",
      "position": {"x": 3000, "y": 2000},
      "dimensions": {"width": 500, "length": 400, "height": 500}
    }
  ]
}
```

### MEP Systems

Mechanical, Electrical, and Plumbing information:

```json
{
  "id": "kitchen",
  "name": "Kitchen",
  "boundaries": [...],
  "x-mep": {
    "electrical": {
      "outlets": [
        {"position": {"x": 1000, "y": 0}, "type": "standard", "voltage": 120},
        {"position": {"x": 3000, "y": 0}, "type": "gfci", "voltage": 120}
      ],
      "switches": [
        {"position": {"x": 5000, "y": 1500}, "controls": ["ceiling-light"]}
      ],
      "lighting": [
        {"id": "ceiling-light", "type": "recessed", "count": 4}
      ]
    },
    "plumbing": {
      "fixtures": [
        {"type": "sink", "position": {"x": 2000, "y": 0}},
        {"type": "dishwasher", "position": {"x": 3500, "y": 0}}
      ],
      "supply": [
        {"type": "hot-water", "position": {"x": 2000, "y": 0}},
        {"type": "cold-water", "position": {"x": 2000, "y": 0}}
      ]
    },
    "hvac": {
      "vents": [
        {"type": "supply", "position": {"x": 3000, "y": 1500}},
        {"type": "return", "position": {"x": 1000, "y": 1500}}
      ]
    }
  }
}
```

### Building Code

Building code and compliance information:

```json
{
  "id": "commercial-suite",
  "name": "Office Suite",
  "boundaries": [...],
  "x-code-compliance": {
    "occupancy-type": "B",
    "occupant-load": 20,
    "exit-requirements": {
      "exits-required": 2,
      "exit-distance": 60000,
      "exit-width": 900
    },
    "accessibility": {
      "ada-compliant": true,
      "accessible-route": true,
      "accessible-toilet": true
    },
    "fire-safety": {
      "sprinklered": true,
      "fire-alarm": true,
      "smoke-detectors": 3
    }
  }
}
```

### Energy Analysis

Energy performance data:

```json
{
  "layout": {
    "id": "building-a",
    "x-energy": {
      "climate-zone": "4A",
      "orientation": 0,
      "envelope": {
        "wall-r-value": 19,
        "roof-r-value": 38,
        "window-u-value": 0.3,
        "infiltration-rate": 3.0
      },
      "systems": {
        "heating": "natural-gas",
        "cooling": "electric",
        "ventilation": "mechanical",
        "dhw": "natural-gas"
      }
    }
  }
}
```

### Rendering Hints

Provide hints for rendering engines:

```json
{
  "id": "room-1",
  "name": "Living Room",
  "boundaries": [...],
  "x-render": {
    "camera-position": {"x": 3000, "y": 2000, "z": 1500},
    "camera-target": {"x": 3000, "y": 3000, "z": 0},
    "lighting": "natural",
    "shadow-quality": "high",
    "materials": {
      "floor": "hardwood-oak",
      "walls": "paint-white",
      "ceiling": "paint-white"
    }
  }
}
```

### Cost Estimation

Construction cost information:

```json
{
  "id": "wall-1",
  "thickness": 200,
  "x-cost": {
    "material-cost": 45.50,
    "labor-cost": 32.00,
    "unit": "per-linear-meter",
    "currency": "USD",
    "date": "2024-01-01"
  }
}
```

### Scheduling

Construction schedule data:

```json
{
  "id": "room-1",
  "name": "Living Room",
  "boundaries": [...],
  "x-schedule": {
    "start-date": "2024-06-01",
    "end-date": "2024-06-15",
    "duration": 14,
    "unit": "days",
    "dependencies": ["foundation", "framing"],
    "crew-size": 4
  }
}
```

## Vendor Extensions

Vendors can define their own extension namespaces:

### Example: Autodesk Extension

```json
{
  "id": "wall-1",
  "x-autodesk": {
    "revit-family": "Basic Wall",
    "revit-type": "Generic - 200mm",
    "element-id": "1234567"
  }
}
```

### Example: Custom Tool Extension

```json
{
  "id": "room-1",
  "x-mycompany-tool": {
    "version": "2.0",
    "generated-by": "MyCompanyTool",
    "custom-data": {
      "feature-a": true,
      "feature-b": "value"
    }
  }
}
```

## Extension Guidelines

### Naming Conventions

Use clear, descriptive names with kebab-case:

- ✅ `x-ceiling-height`
- ✅ `x-material-type`
- ✅ `x-cost-estimate`
- ❌ `x-ch` (too abbreviated)
- ❌ `x-ceilingHeight` (use kebab-case)

### Data Structure

Keep extensions well-structured:

```json
// Good: Organized structure
{
  "x-lighting": {
    "fixtures": [...],
    "controls": [...],
    "circuits": [...]
  }
}

// Bad: Flat structure
{
  "x-lighting-fixtures": [...],
  "x-lighting-controls": [...],
  "x-lighting-circuits": [...]
}
```

### Documentation

Document your extensions:

```json
{
  "$schema": "https://example.com/my-extension-schema.json",
  "x-my-extension": {
    "version": "1.0",
    "documentation": "https://example.com/docs/extension"
  }
}
```

### Compatibility

Ensure extensions don't break standard parsers:

- Use valid JSON
- Don't override standard properties
- Make extensions optional
- Provide defaults when possible

## Extension Schemas

Define JSON schemas for your extensions:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "OAS Material Extension",
  "type": "object",
  "properties": {
    "x-material": {
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["concrete", "wood", "steel", "glass", "brick"]
        },
        "finish": {
          "type": "string"
        },
        "color": {
          "type": "string",
          "pattern": "^#[0-9A-Fa-f]{6}$"
        }
      },
      "required": ["type"]
    }
  }
}
```

## Backward Compatibility

When evolving extensions:

1. **Don't remove properties**: Add new ones instead
2. **Use version numbers**: Include version in extension data
3. **Provide defaults**: Make new properties optional
4. **Document changes**: Maintain a changelog

```json
{
  "x-my-extension": {
    "version": "2.0",
    "legacy-support": true,
    "new-feature": "value"
  }
}
```

## Extension Registry

Consider maintaining a registry of common extensions:

| Extension | Purpose | Maintainer | Schema |
|-----------|---------|------------|--------|
| `x-material` | Material properties | Community | [Link](#) |
| `x-cost` | Cost estimation | Community | [Link](#) |
| `x-mep` | MEP systems | Community | [Link](#) |
| `x-bim` | BIM integration | Community | [Link](#) |

## Best Practices

!!! tip "Prefix Everything"
    Always use the `x-` prefix for custom properties

!!! tip "Namespace Vendors"
    Use vendor names in extensions: `x-autodesk-*`, `x-mycompany-*`

!!! tip "Document Extensions"
    Provide clear documentation and examples for custom extensions

!!! tip "Use Schemas"
    Define JSON schemas for validation

!!! warning "Don't Override"
    Never override standard OAS properties with extensions

## Validation

Validate documents with extensions:

```javascript
function validateWithExtensions(document, schemas) {
  // Validate base OAS
  validateOAS(document);
  
  // Validate extensions
  Object.keys(document).forEach(key => {
    if (key.startsWith('x-')) {
      const schema = schemas[key];
      if (schema) {
        validateAgainstSchema(document[key], schema);
      }
    }
  });
}
```

## Next Steps

- Review [Core](core.md) for base concepts
- See [Examples](examples/simple_plan.md) for extension usage
- Check [Glossary](glossary.md) for extension terms
