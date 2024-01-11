# UIntNPortray

A subset of SVG for creating simple and efficient vector drawings

- Portray using straight lines only.
- The coordinates of lines are unsigned integers only.
- The range of coordinates is between 0 and (2 ^ N - 1).
  - e.g. UInt8Portray: between 0 and 255 (2 ^ 8 - 1)

## Structure

- A line `<path>` has only coordinates attribute.
  - ```<path d="M 1 2 L 3 4" />```
- A line `<path>` should be placed inside a `<g>` element has only width attribute.
  - ```<g stroke-width="1" />```
- A `<g>` element with width attribute should be placed inside a `<g>` element has only attributes related to color.
  - ```<g stroke="#000000" opacity="1.0" stroke-opacity="0.9"/>```
- A `<rect>` element of the same size as the canvas is required for the background color.
  - ```<rect width="100%" height="100%" fill="#FFFFFF" />```

### Sample SVG of UInt8Portray ruleset drawing

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
