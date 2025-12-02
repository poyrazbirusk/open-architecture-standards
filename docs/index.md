# Open Architecture Standards

Welcome to the **Open Architecture Standards (OAS)** documentation!

## What is OAS?

Open Architecture Standards (OAS) is a lightweight, LLM-friendly schema for describing architectural layouts, programs, rooms, walls, and openings using simple JSON in millimeter coordinates. It's designed for:

- 🤖 **Generative design** - Enable AI-powered architectural design
- ✏️ **Editing by prompts** - Modify designs using natural language
- 🌐 **Easy rendering** - Simple integration with web tools

## Key Features

- **Simple JSON Format**: Easy to read, write, and parse
- **Millimeter Precision**: Accurate coordinate-based descriptions
- **LLM-Friendly**: Designed for seamless AI integration
- **Web-Ready**: Built for modern web rendering tools

## Quick Start

Get started with OAS by exploring our documentation:

1. **[Core Concepts](core.md)** - Understand the fundamentals
2. **[Geometry](geometry.md)** - Learn about coordinates and shapes
3. **[Program](program.md)** - Define room types and usage
4. **[Layout](layout.md)** - Create complete architectural designs

## Specification

- **[Core](core.md)** - Base concepts and data structures
- **[Geometry](geometry.md)** - Coordinate systems and geometric elements
- **[Program](program.md)** - Room classifications and programs
- **[Layout](layout.md)** - Complete layout definitions
- **[Render](render.md)** - Visualization and rendering
- **[Extensions](extensions.md)** - Custom properties and extensions
- **[Glossary](glossary.md)** - Terminology and definitions

## Examples

Learn by example:

- **[Simple Plan](examples/simple_plan.md)** - Basic single-room layout
- **[Multi-Room Plan](examples/multi_room_plan.md)** - Complex apartment layout

## Use Cases

OAS is perfect for:

- **Architectural Design Tools**: Build AI-powered design applications
- **Space Planning**: Automate layout generation and optimization
- **Visualization**: Create interactive floor plans and 3D models
- **Documentation**: Standardize architectural data representation

## Example

Here's a minimal OAS document:

```json
{
  "version": "1.0.0",
  "layout": {
    "id": "simple-room",
    "name": "Office",
    "rooms": [
      {
        "id": "room-1",
        "name": "Office",
        "program": "office",
        "boundaries": [
          {"x": 0, "y": 0},
          {"x": 4000, "y": 0},
          {"x": 4000, "y": 3000},
          {"x": 0, "y": 3000}
        ]
      }
    ]
  }
}
```

## Contributing

This is an open standard. Contributions and feedback are welcome! Visit our [GitHub repository](https://github.com/poyrazbirusk/open-architecture-standards) to get involved.

## Version

Current specification version: **1.0.0**
