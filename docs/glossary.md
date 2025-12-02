# Glossary

Definitions of terms used in the Open Architecture Standards (OAS).

## A

**Adjacency**
: The relationship between spaces that share a common boundary or are positioned next to each other.

**Area**
: The two-dimensional space enclosed by a room's boundaries, measured in square millimeters in OAS.

**Axis**
: A reference line in the coordinate system, either horizontal (X-axis) or vertical (Y-axis).

## B

**Boundaries**
: The array of coordinate points that define the perimeter of a room or space.

**Building Code**
: Regulations that specify minimum standards for construction, safety, and occupancy.

## C

**Cartesian Coordinate System**
: A coordinate system that specifies each point using numerical coordinates based on its distance from perpendicular axes.

**Circulation**
: Spaces designated for movement and passage, such as hallways, corridors, and stairs.

**Coordinate**
: A set of values that show an exact position in a coordinate system. In OAS, coordinates use X and Y values in millimeters.

**Core Concepts**
: The fundamental elements and principles that form the foundation of OAS.

## D

**Door**
: An opening type that provides access between spaces, typically with a hinged or sliding panel.

**Draw.io**
: A diagramming tool that can be integrated with MkDocs for creating architectural diagrams.

## E

**Element**
: A fundamental component of an OAS document, such as a room, wall, or opening.

**Extrusion**
: The process of extending a 2D shape along a third axis to create a 3D form.

**Extension**
: Custom properties added to OAS elements using the `x-` prefix for domain-specific needs.

## F

**Floor Plan**
: A 2D representation showing the layout of a building level from above.

**Furniture**
: Movable objects within a space, which can be specified using extensions.

## G

**Geometry**
: The mathematical description of shapes, sizes, positions, and spatial properties.

**GLightbox**
: A plugin that provides image zoom and gallery functionality in MkDocs.

## H

**Height**
: Vertical measurement, typically referring to wall height, ceiling height, or opening height in millimeters.

## I

**Identifier (ID)**
: A unique string that identifies an element within an OAS document.

**ISO 8601**
: International standard for date and time format (e.g., "2024-01-01T00:00:00Z").

## J

**JSON (JavaScript Object Notation)**
: A lightweight data format used by OAS for representing architectural layouts.

## L

**Layout**
: The top-level container object that holds all architectural elements in an OAS document.

**Line**
: A straight geometric element defined by two points (start and end).

**LLM (Large Language Model)**
: AI systems designed to understand and generate human language, which OAS is optimized to work with.

## M

**Material**
: The substance from which building elements are constructed, such as concrete, wood, or steel.

**Material Theme**
: The design system used for the MkDocs documentation, providing modern UI components.

**MEP (Mechanical, Electrical, Plumbing)**
: Building systems for heating, cooling, electrical power, lighting, and plumbing.

**Metadata**
: Data that provides information about other data, such as document title, author, and dates.

**Millimeter (mm)**
: The base unit of measurement in OAS, equal to 0.001 meters.

**MkDocs**
: A static site generator used to create the OAS documentation from Markdown files.

## N

**Navigation**
: The structure and organization of documentation pages and their relationships.

## O

**OAS (Open Architecture Standards)**
: The specification defined in this documentation for representing architectural layouts in JSON.

**Opening**
: A gap in a wall for doors, windows, or passages.

**Origin**
: The point (0, 0) in a coordinate system from which all other points are measured.

## P

**Passage**
: An opening type representing an unobstructed connection between spaces without a door.

**Point**
: A location in space defined by X and Y coordinates.

**Polygon**
: A closed shape formed by connecting multiple points with straight lines.

**Program**
: The intended use or function of a space (e.g., "bedroom", "kitchen", "office").

**Pymdown Extensions**
: A collection of extensions for Python Markdown used in MkDocs for enhanced features.

## R

**Rendering**
: The process of generating a visual representation from OAS data.

**Room**
: An enclosed space within a layout, defined by its boundaries and program.

## S

**Schema**
: The structure and rules that define how OAS documents should be formatted.

**Semantic Versioning**
: A versioning system using MAJOR.MINOR.PATCH format (e.g., "1.0.0").

**SVG (Scalable Vector Graphics)**
: An XML-based vector image format that can be rendered at any size without loss of quality.

**Syntax Highlighting**
: Colored formatting of code to make it easier to read and understand.

## T

**Thickness**
: The measurement of a wall's width, perpendicular to its length, in millimeters.

**Type**
: A classification or category, such as opening type ("door", "window", "passage").

## U

**Units**
: The measurement system used in a document. OAS defaults to millimeters (mm).

## V

**Validation**
: The process of checking that an OAS document conforms to the specification rules.

**Vendor Extension**
: Custom properties specific to a particular tool or organization, using the `x-vendor-` prefix.

**Version**
: The specification version number an OAS document conforms to.

**Viewport**
: The visible area of a rendered layout, defined by position, zoom, and dimensions.

## W

**Wall**
: A linear architectural element that defines boundaries and partitions, characterized by thickness, start point, and end point.

**Window**
: An opening type that provides light and/or ventilation, typically with glass.

**Winding Order**
: The direction (clockwise or counter-clockwise) in which polygon vertices are ordered.

## X

**X-axis**
: The horizontal axis in a Cartesian coordinate system.

**X-prefix**
: The required prefix for custom extension properties (e.g., `x-custom-property`).

## Y

**Y-axis**
: The vertical axis in a Cartesian coordinate system.

## Z

**Zoom**
: The scale factor for viewing a layout, where larger values show more detail.

---

## Acronyms

| Acronym | Full Term |
|---------|-----------|
| 2D | Two-Dimensional |
| 3D | Three-Dimensional |
| ADA | Americans with Disabilities Act |
| API | Application Programming Interface |
| BIM | Building Information Modeling |
| CAD | Computer-Aided Design |
| HVAC | Heating, Ventilation, and Air Conditioning |
| ID | Identifier |
| JSON | JavaScript Object Notation |
| LLM | Large Language Model |
| MEP | Mechanical, Electrical, Plumbing |
| mm | Millimeters |
| OAS | Open Architecture Standards |
| PDF | Portable Document Format |
| PNG | Portable Network Graphics |
| SVG | Scalable Vector Graphics |
| UI | User Interface |
| URL | Uniform Resource Locator |
| XML | Extensible Markup Language |

---

## Related Terms

### From Architecture

- **Floor Area Ratio (FAR)**: The ratio of total building floor area to the area of the lot
- **Setback**: The minimum distance a building must be from property lines
- **Zoning**: Land use regulations that control building types and uses

### From Software

- **API**: Application Programming Interface for software integration
- **Parsing**: Analyzing and converting data from one format to another
- **Serialization**: Converting data structures into a storable format

### From Mathematics

- **Vector**: A quantity having direction and magnitude
- **Matrix**: A rectangular array of numbers used for transformations
- **Algorithm**: A step-by-step procedure for calculations

---

## See Also

- [Core Concepts](core.md) - Fundamental OAS concepts
- [Geometry](geometry.md) - Coordinate systems and shapes
- [Program](program.md) - Room types and classifications
- [Layout](layout.md) - Complete layout structures
- [Extensions](extensions.md) - Custom properties

---

*This glossary is maintained as part of the OAS specification. If you find terms that need clarification or addition, please contribute to the documentation.*
