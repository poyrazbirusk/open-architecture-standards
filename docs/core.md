# OAS-Core

OAS-Core defines the **fundamental building blocks** of the Open Architecture Standards.  
Every valid OAS document must follow the structures and conventions described in this module.

The purpose of OAS-Core is to provide a **minimal, stable, and consistent schema** for describing 2D architectural layouts using simple, millimeter-precise JSON. All other OAS modules—Program, Geometry, Layout, Render, and Extensions—build upon the definitions established here.

OAS-Core specifies the following primary components:

- **Metadata** (plan identifiers, titles, descriptions)
- **Units** (standardizing all geometry to millimeter integers)
- **Rooms** (functional spaces defined by polygons)
- **Walls** (straight boundary segments between points)
- **Openings** (doors and windows located along walls)
- **Annotations** (human or LLM-generated notes and comments)

These entities form the essential structure of an architectural plan, ensuring that both humans and automated tools (LLMs, layout solvers, renderers, and editors) interpret plans in a consistent and predictable manner.

OAS-Core does **not** include:

- High-level programmatic intent (see **OAS-Program**)  
- Resolved geometric layouts (see **OAS-Layout**)  
- Rendering/visualization rules (see **OAS-Render**)  
- Optional modules like furniture, MEP, or 3D (see **OAS-Extensions**)  

Instead, OAS-Core serves as the **foundation** of the standard, defining the core concepts and structures that all OAS-compliant tools are expected to support.
