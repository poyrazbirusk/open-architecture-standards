# Program

This page describes how to specify room programs and usage types in OAS.

## Overview

The **program** of a space defines its intended use, function, or room type. This information is essential for:

- Automated layout generation
- Space planning and optimization
- Building code compliance
- Functional analysis
- Rendering and visualization

## Program Property

Rooms in OAS can include a `program` property to specify their function:

```json
{
  "id": "room-1",
  "name": "Master Bedroom",
  "program": "bedroom",
  "boundaries": [...]
}
```

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `program` | string | No | Room function or type |

## Standard Programs

While OAS allows any string value for `program`, these standard programs are recommended for consistency:

### Residential Programs

| Program | Description | Typical Size Range |
|---------|-------------|-------------------|
| `living` | Living room, family room | 15-40 m² |
| `bedroom` | Bedroom, sleeping quarters | 9-20 m² |
| `kitchen` | Kitchen, cooking area | 8-20 m² |
| `dining` | Dining room | 10-20 m² |
| `bathroom` | Full bathroom | 4-8 m² |
| `powder-room` | Half bath, toilet room | 2-4 m² |
| `laundry` | Laundry room | 3-6 m² |
| `storage` | Storage, closet | 2-10 m² |
| `garage` | Garage, parking | 12-40 m² |
| `entry` | Entry, foyer | 4-10 m² |
| `hallway` | Corridor, circulation | 2-8 m² |
| `utility` | Utility room, mechanical | 3-8 m² |

### Commercial Programs

| Program | Description | Typical Size Range |
|---------|-------------|-------------------|
| `office` | Private office | 9-20 m² |
| `open-office` | Open workspace | 100-500 m² |
| `meeting` | Meeting room, conference | 10-40 m² |
| `reception` | Reception area, lobby | 15-50 m² |
| `breakroom` | Break room, kitchen | 10-25 m² |
| `restroom` | Public restroom | 8-20 m² |
| `server-room` | Server room, data center | 10-40 m² |
| `storage` | Storage, supplies | 5-30 m² |

### Public Programs

| Program | Description | Typical Size Range |
|---------|-------------|-------------------|
| `retail` | Retail space | 50-500 m² |
| `restaurant` | Restaurant, café | 100-400 m² |
| `classroom` | Classroom, training room | 40-80 m² |
| `auditorium` | Auditorium, theater | 200-1000 m² |
| `library` | Library, reading room | 100-500 m² |
| `gym` | Gymnasium, fitness | 200-800 m² |

### Service Programs

| Program | Description | Typical Size Range |
|---------|-------------|-------------------|
| `mechanical` | Mechanical room, HVAC | 10-50 m² |
| `electrical` | Electrical room | 5-20 m² |
| `janitor` | Janitor closet | 2-5 m² |
| `circulation` | Circulation, corridor | Varies |
| `stairs` | Stairwell | 8-15 m² |
| `elevator` | Elevator shaft | 4-8 m² |

## Program Examples

### Residential Unit

```json
{
  "rooms": [
    {
      "id": "living-room",
      "name": "Living Room",
      "program": "living",
      "boundaries": [...]
    },
    {
      "id": "master-bedroom",
      "name": "Master Bedroom",
      "program": "bedroom",
      "boundaries": [...]
    },
    {
      "id": "kitchen",
      "name": "Kitchen",
      "program": "kitchen",
      "boundaries": [...]
    }
  ]
}
```

### Office Suite

```json
{
  "rooms": [
    {
      "id": "reception",
      "name": "Reception Area",
      "program": "reception",
      "boundaries": [...]
    },
    {
      "id": "conference",
      "name": "Conference Room",
      "program": "meeting",
      "boundaries": [...]
    },
    {
      "id": "office-1",
      "name": "Private Office",
      "program": "office",
      "boundaries": [...]
    }
  ]
}
```

## Custom Programs

You can define custom programs for specialized uses:

```json
{
  "id": "recording-studio",
  "name": "Recording Studio",
  "program": "recording-studio",
  "boundaries": [...]
}
```

For custom programs, consider using descriptive kebab-case names:
- `maker-space`
- `meditation-room`
- `art-studio`
- `home-theater`

## Program Metadata

You can add additional program-related metadata using custom properties:

```json
{
  "id": "bedroom-1",
  "name": "Bedroom 1",
  "program": "bedroom",
  "x-occupancy": 2,
  "x-furnishing": "king-bed",
  "x-requirements": {
    "window": true,
    "closet": true,
    "ensuite": false
  },
  "boundaries": [...]
}
```

## Program Hierarchies

For complex buildings, programs can be organized hierarchically:

```json
{
  "id": "suite-100",
  "name": "Suite 100",
  "program": "residential-unit",
  "x-sub-programs": [
    "living",
    "bedroom",
    "bedroom",
    "bathroom",
    "kitchen"
  ],
  "boundaries": [...]
}
```

## Adjacency Requirements

Program information is useful for defining adjacency requirements:

```json
{
  "x-adjacency-matrix": {
    "kitchen": {
      "dining": "required",
      "living": "preferred",
      "bedroom": "avoid"
    },
    "bathroom": {
      "bedroom": "preferred",
      "kitchen": "avoid"
    }
  }
}
```

## Program Validation

When validating programs, check for:

1. **Required programs**: Ensure all necessary room types are present
2. **Minimum counts**: Verify minimum number of each program type
3. **Area requirements**: Validate room sizes meet program requirements
4. **Code compliance**: Check against building code requirements

## Use Cases

### Generative Design

Programs guide AI-powered layout generation:
- Room placement based on adjacency preferences
- Size allocation based on program requirements
- Circulation planning based on program relationships

### Space Planning

Programs enable automated space planning:
- Area calculation by program type
- Program distribution analysis
- Functional zoning

### Visualization

Programs control rendering:
- Color coding by program type
- Material selection
- Furniture placement

## Best Practices

!!! tip "Consistency"
    Use standard program names consistently throughout your documents

!!! tip "Documentation"
    Document any custom programs you define in your organization

!!! tip "Validation"
    Create validation rules based on program requirements

## Next Steps

- Learn about [Layout](layout.md) to combine programs with geometry
- See [Core](core.md) for base concepts
- Explore [Examples](examples/multi_room_plan.md) for program usage
