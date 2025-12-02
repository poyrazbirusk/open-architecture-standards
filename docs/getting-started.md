# Getting Started

This guide will help you understand and start using the Open Architecture Standards (OAS).

## Overview

OAS provides a standardized way to describe architectural layouts using JSON. The schema is designed to be both human-readable and machine-processable, making it ideal for AI-powered design tools.

## Basic Concepts

### Coordinate System

OAS uses a millimeter-based coordinate system:

- All measurements are in millimeters (mm)
- Origin point (0, 0) represents a reference point in the layout
- Coordinates can be positive or negative

### Core Elements

The standard defines several key elements:

1. **Layouts**: Overall architectural plans
2. **Rooms**: Defined spaces with specific programs
3. **Walls**: Physical boundaries and partitions
4. **Openings**: Doors, windows, and other passages

## Basic Example

Here's a simple example of an OAS structure:

```json
{
  "version": "1.0",
  "layout": {
    "id": "example-layout",
    "rooms": [
      {
        "id": "room-1",
        "name": "Living Room",
        "program": "residential",
        "boundaries": [
          {"x": 0, "y": 0},
          {"x": 5000, "y": 0},
          {"x": 5000, "y": 4000},
          {"x": 0, "y": 4000}
        ]
      }
    ],
    "walls": [
      {
        "id": "wall-1",
        "thickness": 200,
        "start": {"x": 0, "y": 0},
        "end": {"x": 5000, "y": 0}
      }
    ]
  }
}
```

## Next Steps

- Read the [Specification Overview](specification/overview.md) for detailed information
- Explore the [Schema](specification/schema.md) to understand all available properties
- Check out more [Examples](specification/examples.md) for common use cases

## Tools and Integration

OAS is designed to work seamlessly with:

- JSON parsers and validators
- Web-based rendering engines
- AI and LLM systems
- CAD and BIM tools

## Support

For questions, issues, or contributions, visit our [GitHub repository](https://github.com/poyrazbirusk/open-architecture-standards).
