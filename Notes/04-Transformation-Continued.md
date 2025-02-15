# **Lecture 4 - Tranformation Continued**

- **Date**: 2025/2/14 (情人节看GAMES101这辈子有了)

## **Contents**

- 3D transformations
- Viewing (观测) transformation
  - View (视图) / Camera transformation
  - Projection (投影) transformation
    - Orthographic (正交) projection
    - Perspective (透视) projection

## **3D Transformations**

### **Recall**

Use homogeneous coordinates again:

- 3D point = $(x, y, z, 1)^T$
- 3D vector = $(x, y, z, 0)^T$

Core idea: To make translation general.

In general, (x, y, z, w) (w != 0) is the 3D point:

``` math
(\frac{x}{w}, \frac{y}{w}, \frac{z}{w})
```

We use 4x4 matrices for affine transformations:

``` math
\begin{pmatrix} x' \\ y' \\ z' \\ 1 \end{pmatrix} =
\begin{pmatrix} a & b & c & t_{x} \\ d & e & f & t_{y} \\
g & h & i & t_{z} \\ 0 & 0 & 0 & 1 \end{pmatrix} \cdot
\begin{pmatrix} x \\ y \\ z \\ 1 \end{pmatrix}
```

Is the order Linear Transform first or Translation first?

- It will be linear map + translation (the same as 2D).

### **General Formulas**

Scale:

``` math
\mathbf{S}(s_{x}, s_{y}, s_{z}) =
\begin{pmatrix} s_{x} & 0 & 0 & 0 \\ 0 & s_{y} & 0 & 0 \\ 0 & 0 & s_{z} & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
```

Translation:

``` math
\mathbf{T}(t_{x}, t_{y}, t_{z}) =
\begin{pmatrix} 1 & 0 & 0 & t_{x} \\ 0 & 1 & 0 & t_{y} \\ 0 & 0 & 1 & t_{z} \\ 0 & 0 & 0 & 1 \end{pmatrix}
```

Rotation around x-, y-, or z-axis:

``` math
\mathbf{R}_{x}(\alpha) =
\begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & cos\alpha & -sin\alpha & 0 \\ 0 & sin\alpha & cos\alpha & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
```

``` math
\mathbf{R}_{y}(\alpha) =
\begin{pmatrix} cos\alpha & 0 & sin\alpha & 0 \\ 0 & 1 & 0 & 0 \\ -sin\alpha & 0 & cos\alpha & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
```

``` math
\mathbf{R}_{z}(\alpha) =
\begin{pmatrix} cos\alpha & -sin\alpha & 0 & 0 \\ sin\alpha & cos\alpha & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
```

Note:

- The coordinate of the axis rotated around does not change.
- The rotation is always counter-clockwise around the axis.

Compose any 3D rotation from $R_x$, $R_y$, $R_z$:

``` math
\mathbf{R}_{xyz}(\alpha, \beta, \gamma) = \mathbf{R}_x(\alpha)\mathbf{R}_y(\beta)\mathbf{R}_z(\gamma)
```

- So-called Euler angles.
- Often used in flight simulators: roll, pitch, yaw.
  - Roll: Roll left and right (x-axis).
  - Pitch: Pitch up and down (y-axis).
  - Yaw: Yaw left and right in horizontal direction (z-axis).

### **Rodrigues' Rotation Formula**

Rotation by angle $\alpha$ around axis n:

``` math
\mathbf{R}(\mathbf{n}, \alpha) = \cos(\alpha) \mathbf{I} + (1 - \cos(\alpha)) \mathbf{n} \mathbf{n}^T + \sin(\alpha)
\underbrace{\begin{pmatrix}
0 & -n_z & n_y \\
n_z & 0 & -n_x \\
-n_y & n_x & 0
\end{pmatrix}}_{\mathbf{N}}
```

**The Derivation of Rodrigues' Rotation Formula:**

>