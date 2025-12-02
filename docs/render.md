# Render

This page describes rendering and visualization concepts for OAS layouts.

## Overview

While OAS is primarily a data format, understanding rendering concepts helps create layouts that visualize well. This page covers visualization strategies, styling, and rendering considerations.

## Rendering Concepts

### 2D Rendering

Most OAS layouts are rendered as 2D floor plans:

- **Top-down view**: Birds-eye perspective
- **Scale**: Typically 1:50 or 1:100 for floor plans
- **Line weights**: Different thicknesses for walls, openings, etc.
- **Colors**: Different colors for rooms by program type

### Coordinate Mapping

Convert OAS coordinates to screen/canvas coordinates:

```javascript
// Map millimeters to pixels
function toPixels(mm, scale = 0.1) {
  return mm * scale; // 0.1 = 1mm = 0.1px
}

// Map OAS point to canvas
function mapPoint(point, scale, offset) {
  return {
    x: point.x * scale + offset.x,
    y: point.y * scale + offset.y
  };
}
```

### Viewport

Define a viewport to control what's visible:

```javascript
const viewport = {
  centerX: 5000,  // Center on X coordinate
  centerY: 4000,  // Center on Y coordinate
  zoom: 0.05,     // Zoom level (smaller = zoomed out)
  width: 1200,    // Canvas width in pixels
  height: 800     // Canvas height in pixels
};
```

## Rendering Elements

### Rooms

Render room boundaries as filled polygons:

```javascript
function renderRoom(room, style) {
  ctx.fillStyle = style.fill;
  ctx.strokeStyle = style.stroke;
  ctx.lineWidth = style.lineWidth;
  
  ctx.beginPath();
  const first = room.boundaries[0];
  ctx.moveTo(first.x, first.y);
  
  for (let i = 1; i < room.boundaries.length; i++) {
    const point = room.boundaries[i];
    ctx.lineTo(point.x, point.y);
  }
  ctx.closePath();
  
  ctx.fill();
  ctx.stroke();
}
```

### Walls

Render walls as thick lines:

```javascript
function renderWall(wall) {
  ctx.strokeStyle = '#000000';
  ctx.lineWidth = wall.thickness * scale;
  ctx.lineCap = 'square';
  
  ctx.beginPath();
  ctx.moveTo(wall.start.x, wall.start.y);
  ctx.lineTo(wall.end.x, wall.end.y);
  ctx.stroke();
}
```

### Openings

Render openings with special symbols:

```javascript
function renderOpening(opening) {
  const wall = findWall(opening.wall_id);
  
  if (opening.type === 'door') {
    renderDoorSymbol(opening, wall);
  } else if (opening.type === 'window') {
    renderWindowSymbol(opening, wall);
  } else if (opening.type === 'passage') {
    renderPassageSymbol(opening, wall);
  }
}
```

## Styling

### Color Schemes

Define color schemes for different program types:

```javascript
const programColors = {
  'living': '#E3F2FD',      // Light blue
  'bedroom': '#F3E5F5',     // Light purple
  'kitchen': '#FFF3E0',     // Light orange
  'bathroom': '#E0F2F1',    // Light teal
  'office': '#F1F8E9',      // Light green
  'meeting': '#FFF9C4',     // Light yellow
  'storage': '#ECEFF1',     // Light gray
  'circulation': '#FFFFFF'  // White
};
```

### Line Styles

Different line styles for different elements:

```javascript
const lineStyles = {
  exteriorWall: {
    color: '#000000',
    width: 3,
    style: 'solid'
  },
  interiorWall: {
    color: '#666666',
    width: 2,
    style: 'solid'
  },
  partition: {
    color: '#999999',
    width: 1,
    style: 'dashed'
  }
};
```

### Annotations

Add labels and dimensions:

```javascript
function renderLabel(room, position) {
  ctx.font = '14px Arial';
  ctx.fillStyle = '#333333';
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  
  ctx.fillText(room.name, position.x, position.y);
  
  // Add area below name
  const area = calculateArea(room.boundaries);
  const areaSqm = (area / 1000000).toFixed(1);
  ctx.font = '12px Arial';
  ctx.fillStyle = '#666666';
  ctx.fillText(`${areaSqm} m²`, position.x, position.y + 20);
}
```

## SVG Rendering

Generate SVG output from OAS:

```javascript
function generateSVG(layout) {
  let svg = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 ${width} ${height}">`;
  
  // Render rooms
  layout.rooms.forEach(room => {
    const points = room.boundaries
      .map(p => `${p.x},${p.y}`)
      .join(' ');
    
    const fill = programColors[room.program] || '#FFFFFF';
    svg += `<polygon points="${points}" fill="${fill}" stroke="#000" stroke-width="2"/>`;
    
    // Add label
    const center = calculateCenter(room.boundaries);
    svg += `<text x="${center.x}" y="${center.y}" text-anchor="middle">${room.name}</text>`;
  });
  
  // Render walls
  layout.walls.forEach(wall => {
    svg += `<line x1="${wall.start.x}" y1="${wall.start.y}" `;
    svg += `x2="${wall.end.x}" y2="${wall.end.y}" `;
    svg += `stroke="#000" stroke-width="${wall.thickness}"/>`;
  });
  
  svg += '</svg>';
  return svg;
}
```

## 3D Visualization

For 3D rendering, extrude 2D layouts:

```javascript
function extrude3D(room, height = 2800) {
  const geometry = new THREE.ExtrudeGeometry(
    createShape(room.boundaries),
    {
      depth: height,
      bevelEnabled: false
    }
  );
  
  const material = new THREE.MeshLambertMaterial({
    color: programColors[room.program]
  });
  
  return new THREE.Mesh(geometry, material);
}
```

## Interactive Features

### Zoom and Pan

Implement zoom and pan controls:

```javascript
canvas.addEventListener('wheel', (e) => {
  e.preventDefault();
  const zoomFactor = e.deltaY > 0 ? 0.9 : 1.1;
  viewport.zoom *= zoomFactor;
  render();
});

let isDragging = false;
let lastPos = {x: 0, y: 0};

canvas.addEventListener('mousedown', (e) => {
  isDragging = true;
  lastPos = {x: e.clientX, y: e.clientY};
});

canvas.addEventListener('mousemove', (e) => {
  if (isDragging) {
    const dx = e.clientX - lastPos.x;
    const dy = e.clientY - lastPos.y;
    viewport.centerX -= dx / viewport.zoom;
    viewport.centerY -= dy / viewport.zoom;
    lastPos = {x: e.clientX, y: e.clientY};
    render();
  }
});
```

### Selection

Implement element selection:

```javascript
canvas.addEventListener('click', (e) => {
  const rect = canvas.getBoundingClientRect();
  const x = (e.clientX - rect.left - viewport.width/2) / viewport.zoom + viewport.centerX;
  const y = (e.clientY - rect.top - viewport.height/2) / viewport.zoom + viewport.centerY;
  
  const selectedRoom = findRoomAtPoint(layout, {x, y});
  if (selectedRoom) {
    highlightRoom(selectedRoom);
  }
});
```

## Export Formats

### PNG/JPEG

Export as raster image:

```javascript
function exportPNG() {
  const dataURL = canvas.toDataURL('image/png');
  const link = document.createElement('a');
  link.download = 'layout.png';
  link.href = dataURL;
  link.click();
}
```

### SVG

Export as vector graphic:

```javascript
function exportSVG() {
  const svg = generateSVG(layout);
  const blob = new Blob([svg], {type: 'image/svg+xml'});
  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.download = 'layout.svg';
  link.href = url;
  link.click();
}
```

### PDF

Export as PDF document:

```javascript
function exportPDF() {
  const doc = new jsPDF();
  const svg = generateSVG(layout);
  doc.svg(svg, {
    x: 10,
    y: 10,
    width: 180,
    height: 260
  });
  doc.save('layout.pdf');
}
```

## Performance Optimization

### Level of Detail

Adjust detail based on zoom level:

```javascript
function shouldRenderDetail(element, zoom) {
  if (zoom < 0.01) {
    // Very zoomed out - only render major elements
    return element.type === 'room';
  } else if (zoom < 0.05) {
    // Medium zoom - render rooms and walls
    return element.type !== 'annotation';
  } else {
    // Zoomed in - render everything
    return true;
  }
}
```

### Culling

Skip rendering elements outside viewport:

```javascript
function isInViewport(element, viewport) {
  const bounds = calculateBounds(element);
  return !(
    bounds.maxX < viewport.minX ||
    bounds.minX > viewport.maxX ||
    bounds.maxY < viewport.minY ||
    bounds.minY > viewport.maxY
  );
}
```

### Caching

Cache rendered elements:

```javascript
const renderCache = new Map();

function renderWithCache(element) {
  const key = `${element.id}-${viewport.zoom}`;
  if (!renderCache.has(key)) {
    const canvas = document.createElement('canvas');
    // Render element to canvas
    renderCache.set(key, canvas);
  }
  return renderCache.get(key);
}
```

## Rendering Libraries

Popular libraries for rendering OAS layouts:

- **HTML Canvas**: Native browser API
- **SVG**: Vector graphics in HTML
- **Three.js**: 3D rendering with WebGL
- **D3.js**: Data visualization and SVG
- **Paper.js**: Vector graphics scripting
- **Fabric.js**: Canvas library with interactivity

## Best Practices

!!! tip "Performance"
    Use appropriate level of detail based on zoom level

!!! tip "Accessibility"
    Provide text alternatives for visual elements

!!! tip "Responsiveness"
    Make renderings responsive to different screen sizes

!!! tip "Export"
    Support multiple export formats for different use cases

## Next Steps

- Learn about [Extensions](extensions.md) for custom rendering properties
- See [Examples](examples/simple_plan.md) for rendered layouts
- Explore [Glossary](glossary.md) for rendering terms
