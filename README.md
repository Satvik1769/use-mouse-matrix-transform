# useMouseMatrixTransform

Easily create draggable, zoomable layouts (maps, svg explorers, canvas dragging, etc.)

Allows you to easily create map-like interactions with a canvas element, this
library gives you flexibility in what context you use the transformations because
it just outputs/changes a transform matrix, not the actual elements contained
inside of the element. This makes it flexible for a variety of use cases with
custom renderers.

## Installation

```bash
npm install use-mouse-matrix-transform
```

## Props

|      Name      |    Type     | Required | Default | Description                                     |
| :------------: | :---------: | :------: | :-----: | ----------------------------------------------- |
|   canvasElm    | HTMLElement |   true   |         | The element that mouse events will be bound on. |
|   transform    |   Matrix    |  false   |         |                                                 |
| onSetTransform |   Matrix    |  false   |         |                                                 |

`useMouseMatrixTransform` returns an object with the following properties:

- **ref**: Put this ref on the container element that you want to drag/zoom on
- **transform** A transformation matrix that transforms screen x,y coordinates into the target transform space
- **applyTransformToPoint** Take any `[x,y]` or `{ x, y }` object and apply the transformation, returns a transformed point

## Example

```ts
import useMouseMatrixTransform from "use-mouse-matrix-transform"
import { useEffect, useRef, useState } from "react"
import SomeLayoutObject from "./SomeLayoutObject"

export default ({ layout }: { layout: Layout }) => {
  const { ref, applyTransformToPoint } = useMouseMatrixTransform()

  return (
    <div>
      <div
        ref={ref}
        style={{
          position: "relative",
          backgroundColor: "#eee",
          height: 600,
          overflow: "hidden",
        }}
      >
        {layout.objects
          .map((obj) => applyTransformToPoint(obj))
          .map((obj, i) => (
            <SomeLayoutObject obj={obj} />
          ))}
      </div>
    </div>
  )
}
```
