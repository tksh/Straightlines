# UIntNPortray

A ruleset for producing simple and efficient vector drawings

## Specifications

- Draw using only straight strokes with <path> element.
- A stroke <path> has only coordinates attribute.
  - <path d="" />
- A stroke <path> should be placed inside a group element has only stroke width attribute.
  - <g stroke-width="" />
- A stroke width <g> should be placed inside a group element has only attributes related to color.
  - <g stroke="" opacity="" stroke-opacity=""/>
- A <rect> element of the same size as the canvas is required for the background color.
  - <rect width="100%" height="100%" fill="" />
- The range of canvas coordinates is from 0 to (2 ^ N - 1).
  - e.g. UInt8Portray: <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 255 255" />
