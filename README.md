# UIntNPortray

A ruleset for producing simple and efficient vector drawings

- Draw using only straight strokes.
- The numerical values of the coordinates are integers only.

## Specifications for SVG format

- A stroke `<path>` has only coordinates attribute.
  - ```<path d="" />```
- A stroke `<path>` should be placed inside a `<g>` element has only stroke width attribute.
  - ```<g stroke-width="" />```
- A stroke width `<g>` should be placed inside a `<g>` element has only attributes related to color.
  - ```<g stroke="" opacity="" stroke-opacity=""/>```
- A `<rect>` element of the same size as the canvas is required for the background color.
  - ```<rect width="100%" height="100%" fill="" />```
- The range of canvas coordinates is from 0 to (2 ^ N - 1).
  - e.g. UInt8Portray: ```<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 255 255" />```
