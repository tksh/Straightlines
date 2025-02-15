# Straightlines

A focused SVG subset that unlocks expressive vector art through deliberate simplicity.

## Core Principles

- Drawings are composed only of grouped straight lines.
- Line coordinates use unsigned integers for precision with compactness.
- Non-coordinate attributes are collectively applied through line groups.

## Element Structures

- **Lines** (`<path>` element) must be placed inside a line group (`<g>` element)
- **Line groups** must be at the same hierarchy level; nesting is not allowed

## Required Attributes

### Lines (`<path>`)

- Each line must have (or inherit) the following two attributes:
  - `d` — Line coordinates
    - Must be placed inside a `<path>`
    - Values are unsigned integers
    - Represent the start(x1, x2) and end(y1, y2) points as absolute or relative:
      - Absolute: `"M x1 y1 L x2 y2"`
      - Relative: `"m x1 y1 x2 y2"`
  - `stroke-width` — Line thickness
    - Can be placed either inside a `<g>` or `<path>`, depending on the path modes
    - Values are unsigned integers

### Line Groups (`<g>`)

- Each line group must have the following four attributes:
  - `id` — Sequential unique identifier
    - Values are unsigned integers starting from 0
    - Lower values are rendered first, higher values are rendered on top
  - `stroke` — Line color
    - Values are represented as rgb or hex
  - `opacity` — Group-level transparency
    - Applies to entire line group (`<g>` element)
    - Values are floats between 0 and 1.0
  - `stroke-opacity` — Per-line transparency
    - Applies to individual lines (`<path>` element) within the line group
    - Values are floats between 0 and 1.0

#### Group ID Rules

- The first line group (`id="0"`) serves a specific purpose:
  - It must define a background rectangle matching the `viewBox` size
  - Should be constructed using one or two lines
- Subsequent line groups (`id="1"`, `id="2"`, etc.) represent the actual drawn strokes

## Path Modes

- Lines can be structured in two different modes:
  1. Simple mode: _Absolute-and-separated_
  2. Efficient mode: _Relative-and-merged_
- These modes affect rendering through the application of `stroke-opacity`

### _Absolute-and-separated_

- Represent each line using absolute coordinate values in the `d` attribute
- `<path>` element must:
  - Contain only the `d` attribute
  - Be placed inside a `<g>` element that has only the `stroke-width` attribute
    - This `<g>` element must be nested inside a line group

### _Relative-and-merged_

- Represent lines sharing the same `stroke-width` using relative coordinates in the `d` attribute
- `<path>` element must:
  - Contain both `stroke-width` and `d` attributes
  - Be placed directly inside a line group

## SVG Examples

### _Absolute-and-separated_ Example

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 31 31">
    <g id="0" stroke="rgb(170 170 170)" opacity="1.0" stroke-opacity="1.0">
        <g stroke-width="31">
            <path d="M 15 0 L 15 31"/>
            <path d="M 16 0 L 16 31"/>
        </g>
    </g>
    <g id="1" stroke="rgb(0 0 0)" opacity="1.0" stroke-opacity="0.9">
        <g stroke-width="3">
            <path d="M 1 2 L 3 4" />
            <path d="M 5 6 L 7 8" />
        </g>
    </g>
    <g id="2" stroke="rgb(255 255 255)" opacity="0.8" stroke-opacity="0.7">
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

### _Relative-and-merged_ Example

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 31 31">
    <g id="0" stroke="#AAAAAA" opacity="1.0" stroke-opacity="1.0">
        <path stroke-width="31" d="m15 0 0 31m1-31 0 31"/>
    </g>
    <g id="1" stroke="#000000" opacity="1.0" stroke-opacity="0.9">
        <path stroke-width="3" d="m1 2 2 2m2 2 2 2" />
    </g>
    <g id="2" stroke="#FFFFFF" opacity="0.8" stroke-opacity="0.7">
        <path stroke-width="2" d="m11 12 2 2m2 2 2 2" />
        <path stroke-width="1" d="m101 102 2 2m2 2 2 2" />
    </g>
</svg>
```
