# **Lecture 5 - Rasterization 1 (Triangles)**

- **Date**: 2025/2/18

## **Contents**

- Viewing
- Rasterization
- Occlusions and Visibility

## **Finishing Up Viewing**

### **Perspective Projection**

- What's near plane's l, r, b, t?
  - If explicitly specified good.
  - Sometimes people prefer: vertical **field-of-view** (fovY) and **aspect ratio** (assume symmetry i.e. l = -r, b = -t)
- How to convert from fovY and aspect to l, r, b, t?
  - Trivial:

``` math
\tan{\frac{fovY}{2}} = \frac{t}{|n|} \\
aspect = \frac{r}{t}
```

### **What's after MVP?**

- Model transformation (placing objects).
- View transformation (placing camera).
- Projection transformation:
  - Orthographic projection (cuboid to "canonical" cube $`[-1, 1]^3`$)
  - Perspective projection (frustum to "canonical" cube)

### **Canonical Cube to Screen**

- What is a screen?
  - An array of pixels
  - Size of the array: resolution
  - A typical kind of raster display
- Raster == screen in German
  - Rasterize == drawing onto the screen
- Pixel (FYI, short for "picture element")
  - For now: A pixel is a little square with uniform color
  - Color is a mixture of RGB
