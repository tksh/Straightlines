# UIntNPortray

A subset of SVG to create simple and efficient vector drawings

## Core rules

- Portray using straight lines only.
- The coordinates of lines are unsigned integers only.
- The range of coordinates is between 0 and (2 ^ N - 1).
  - e.g. UInt8Portray: between 0 and 255 (2 ^ 8 - 1)

## Basic structures for SVG format

- Whole lines `<path>` elements should be placed inside a color group `<g>` element.
- Color group `<g>` elements have only attributes related to color like `stroke`, `opacity` and `stroke-opacity`
- A `<rect>` element of the same size as the canvas is required for the background color with `fill` attribute.
- There are two ways to express lines in SVG:
  - Simple: *Absolute and Separated*
  - Efficient: *Relative and Merged*

### Especially for *Absolute and Separated* style

- A line `<path>` element has only `d` attribute.
- A line `<path>` element should be placed inside a `<g>` element with only `stroke-width` attribute.
- A `<g>` element with `stroke-width` attribute should be placed inside a color group `<g>` element.

### Especially for *Relative and Merged* style

- Lines `<path>` elements have `stroke-width` and `d` attribute.
- Lines `<path>` elements should be placed inside a color group `<g>` element.

### Sample SVG code of UInt8Portray

#### In *Absolute and Separated* style

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 255 255">
    <rect width="100%" height="100%" fill="#FFFFFF" />
    <g stroke="#000000" opacity="1.0" stroke-opacity="0.9">
        <g stroke-width="3">
            <path d="M 1 2 L 3 4" />
            <path d="M 5 6 L 7 8" />
        </g>
    </g>
    <g stroke="#AAAAAA" opacity="0.8" stroke-opacity="0.7">
        <g stroke-width="2">
            <path d="M 11 12 L 13 14" />
            <path d="M 15 16 L 17 18" />
        </g>
        <g stroke-width="1">
            <path d="M 101 102 L 103 104" />
            <path d="M 105 106 L 107 108" />
        </g>
    </g>
</svg>
```

#### In *Relative and Merged* style

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 255 255">
    <rect width="100%" height="100%" fill="#FFFFFF" />
    <g stroke="#000000" opacity="1.0" stroke-opacity="0.9">
        <path stroke-width="3" d="m1 2 2 2m2 2 2 2" />
    </g>
    <g stroke="#AAAAAA" opacity="0.8" stroke-opacity="0.7">
        <path stroke-width="2" d="m11 12 2 2m2 2 2 2" />
        <path stroke-width="1" d="m101 102 2 2m2 2 2 2" />
    </g>
</svg>
```
