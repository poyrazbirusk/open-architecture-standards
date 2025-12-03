# OAS Glossary

This glossary defines key terminology used across the Open Architecture Standards (OAS).  
All definitions here apply consistently across OAS-Core, OAS-Geometry, OAS-Program, OAS-Layout, OAS-Render, and OAS-Extensions.

---

## A

### **Adjacency**
A design or layout relationship where two rooms or spaces share a boundary or must be positioned near each other. Defined in OAS-Program and realized in OAS-Layout.

### **Area (m²)**
A derived value representing surface area in square meters. Allowed to contain decimals since it is not a geometric primitive.

---

## B

### **Boundary Polygon**
A closed polygon that defines the perimeter of a room or space. Must use integer millimeter coordinates. Defined in OAS-Geometry.

---

## C

### **Circulation**
Movement paths between rooms, typically represented as a graph of connections. Defined in OAS-Layout and influenced by OAS-Program rules.

### **Closed Polygon**
A polygon whose last point connects back to the first. Must be explicitly marked as `"closed": true`.

### **Core (OAS-Core)**
The foundational module of OAS defining rooms, walls, openings, units, and metadata.

---

## D

### **Design Goal**
A natural-language statement describing the desired outcome of a design (e.g., “compact 2-bedroom apartment with south-facing living room”). Part of OAS-Program.

### **Door**
An opening element connecting rooms. Represented in OAS-Layout as an opening placed along a wall.

---

## E

### **Extension**
A modular add-on for OAS that introduces domain-specific entities such as furniture, MEP, 3D geometry, or materials. Defined in OAS-Extensions.

---

## F

### **Footprint**
A 2D polygon representing the physical outline of an object such as a piece of furniture. Often used in OAS-Furniture.

---

## G

### **Geometry (OAS-Geometry)**
The OAS module defining coordinate systems, polygons, lines, units, and mm-based integer rules.

---

## H

### **Hard Constraint**
A mandatory rule in OAS-Program that must be satisfied in any generated layout.

---

## I

### **ID**
A unique identifier for any entity (room, wall, opening, extension object). Must be stable across editing iterations.

---

## L

### **Layout (OAS-Layout)**
The module representing the resolved geometric state of the design, including all room polygons, walls, openings, and circulation.

### **LLM-Friendly**
A design philosophy emphasizing simple JSON structures, predictable keys, and minimal nesting to support interactions with large language models.

---

## M

### **Metadata**
Supplementary information attached to a document or entity, such as authoring tools, timestamps, or notes.

---

## O

### **Opening**
A door, window, or other penetrations in a wall. OAS-Layout entities specifying width, height, and position along a wall.

### **Origin**
The coordinate (0,0) defining the reference point of the plan's local coordinate system.

---

## P

### **Plan ID**
A unique identifier used to link OAS-Program, OAS-Layout, and OAS-Core documents together.

### **Polygon**
A list of points defining a closed 2D shape. Must follow OAS-Geometry rules (integer mm coordinates, closed: true).

### **Program (OAS-Program)**
The intent-level module specifying desired Areas, Adjacencies, Constraints, and high-level goals.

---

## R

### **Render (OAS-Render)**
Guidelines describing how to convert OAS-Layout data into SVG, Canvas, WebGL, and other visual formats.

### **Room**
A functional space defined by a boundary polygon. Core entity across OAS.

---

## S

### **Scale**
The conversion factor from millimeters to pixels used in rendering.

### **Soft Constraint**
A non-mandatory rule in OAS-Program that solvers or LLMs should attempt to satisfy but may override if needed.

### **Structural Wall**
A wall marked as load-bearing. Rendered differently in many implementations.

---

## T

### **Tag**
A keyword applied to rooms or entities to categorize or filter them (e.g., “daylit”, “wet_area”).

---

## U

### **Unit**
Measurement units used in OAS. Geometry always uses `mm`, angles use `deg`, areas may use `mm2` or `m2`.

---

## W

### **Wall**
A straight boundary element between two points, often with thickness, connecting rooms. Defined in OAS-Core and OAS-Layout.

### **Window**
An opening that provides daylight and ventilation, placed along a wall with attributes such as width, height, and sill height.

---

## Summary

This glossary standardizes terminology across all OAS modules, ensuring consistent understanding and interoperability between tools, LLMs, solvers, and renderers.
