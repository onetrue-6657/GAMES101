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
  - An array of pixels.
  - Size of the array: resolution.
  - A typical kind of raster display.
- Raster == screen in German
  - Rasterize == drawing onto the screen
- Pixel (FYI, short for "picture element")
  - For now: A pixel is a little square with uniform color.
  - Color is a mixture of RGB.
- Defining the screen space.
  - From bottom left and use x, y coordinates.
  - Pixels' indices are in the form of (x, y), where both x and y are integers.
  - Pixels' indices are from (0, 0) to (width - 1, height - 1).
  - Pixel (x, y) is centered at (x + 0.5, y + 0.5).
  - Irrelevant to z.
  - Transform in xy plane: $`[-1, 1]^2`$ to $`[0, width] * [0, height]`$.
  - Viewport transform matrix:

``` math
M_{viewport} = 
\begin{pmatrix} 
\frac{width}{2} & 0 & 0 & \frac{width}{2} \\
0 & \frac{height}{2} & 0 & \frac{height}{2} \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
```

### **Rasterization: Drawing to Raster Displays**

#### Why Triangles?

- Most basic polygon
  - Break up other polygons
- Unique properties
  - Guaranteed to be planar
  - Well-defined interior
  - Well-defined method for interpolating values at vertices over triangle (barycentric interpolation)

> Input: position of triangle vertices projected on screen =>
> Output: set of pixel values approximating triangles

#### Sampling a Function

Evaluating a function at a point is sampling. We can discretize a function by sampling.

```cpp
for (int x = 0; x < xmax; x++) {
  output[x] = f(x);
}
```

Sampling is a core idea in graphics. We sample time (1D), area (2D), direction (2D), volume (3D) ...

#### Functions

- Define Binary Function: ```inside(tri, x, y)```:

```r
inside(t, x, y) => 1 Point (x, y) in triangle t | 0 otherwise
```

- Rasterization = Sampling A 2D Indicator Function

```cpp
for (int x = 0; x < xmax; x++) {
  for (int y = 0; y < ymax; y++) {
    image[x][y] = inside(tri, x + 0.5, y + 0.5);
  }
}
```

- Evaluating ```inside(tri, x, y)```:

> We can cross product $`P_{0/1/2}P_{0/1/2} \times P_{0/1/2}Q`$. If these three have the same sign, then point Q is not inside the triangle.

- Use a bounding box.

- Incremental Triangle Traversal will make it suitable for thin and rotated triangles.
