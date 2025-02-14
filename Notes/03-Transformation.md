# **Lecture 3 - Transformation**

- **Date**: 2025/2/9

## **Contents**

- Why study transformation
- 2D transformations
- Homogeneous coordinates
- Composing transforms
- 3D transformations

## **Why Study Transformation?**

### **Key Concepts**

- Modeling: Translation, rotation, scaling, ...
- Viewing: (3D world to 2D image) projection

## **2D Transformations**

### **Goals**

- Representing transformations using matrices
- Rotation, scale, shear

### **Scale**

We have an example of $s = 0.5$ (Scaling the image to 0.5x of its original.)

$$x' = sx \\ y' = sy$$

We can turn this to a matrix computation.

$$\begin{bmatrix} x' \\ y' \end{bmatrix}
= \begin{bmatrix} s_{x} & 0 \\ 0 & s_{y} \end{bmatrix}
\begin{bmatrix} x \\ y \end{bmatrix}$$

$ \begin{bmatrix} s*{x} & 0 \\ 0 & s*{y} \end{bmatrix} $ is the scaling matrix (缩放矩阵). $x$ and $y$ can scale unevenly (i.e. $s_{x} = 0.5, s_{y} = 1.0$)

### **Reflection**

Horizontal reflection:
$$ x' = -x \\ y' = y $$
We can get a general form of matrix operation here:

$$\begin{bmatrix} x' \\ y' \end{bmatrix}
= \begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix}
\begin{bmatrix} x \\ y \end{bmatrix}$$

### **Shear**

An example of a rectangle: \
Horizontal shift is $0$ at $y = 0$ but is $a$ at $y = 1$. \
Vertical shift is always $0$. \
Rectangle coordinates: \
$(0, 0), (0, 1), (1, 1), (1, 0)$ becomes $(0, 0), (0, 1), (a + 1, 1), (a, 1)$ after the operation. \
We can now get a general form of matrices:

$$\begin{bmatrix} x' \\ y' \end{bmatrix}
= \begin{bmatrix} 1 & a \\ 0 & 1 \end{bmatrix}
\begin{bmatrix} x \\ y \end{bmatrix}$$

### **Rotate**

The rotation is in a 2D plane. The shape rotates around the point $(0, 0)$. The rotation goes counter-clockwise. \
We can get a general form here, in which all angles are in degree:

$$
R_{\theta} =
\begin{bmatrix} cos\theta & -sin\theta \\ sin\theta & cos\theta \end{bmatrix}
$$

For example, $(0, 0), (0, 1), (1, 1), (1, 0)$.

$$\begin{bmatrix} x' \\ y' \end{bmatrix} =
\begin{bmatrix} A & B \\ C & D \end{bmatrix}
\begin{bmatrix} x \\ y \end{bmatrix}$$

$$\begin{bmatrix} cos\theta \\ sin\theta \end{bmatrix} =
\begin{bmatrix} A & B \\ C & D \end{bmatrix}
\begin{bmatrix} 1 \\ 0 \end{bmatrix}$$

Similarly, we can compute the complete formula.

### **Linear Transforms = Matrices**

We can get a general form:

$$
x' = ax + by \\
y' = cx + dy \\
$$

$$\begin{bmatrix} x' \\ y' \end{bmatrix} =
\begin{bmatrix} a & b \\ c & d \end{bmatrix}
\begin{bmatrix} x \\ y \end{bmatrix} \\$$

$$
x' = Mx
$$

These are all linear transforms of the same dimension, involving with simple linear multiplications.

## **Homogeneous Coordinates**

### **Translation**

Translating a shape or points from one place to another. We can get the general form of translation formula:
$$ x' = x + t_{x} \\ y' = y + t_{y} $$
Translation cannot be directly represented in matrix form. It is not a linear transform! We need to add an extra matrix after the multiplication operation.

Is there a unified way to represent all transformations?

- It is Homogeneous Coordinates (齐次坐标).

## **Homogenous Coordinates**

**Basic idea:** Add a third coordinate.

- 2D point = $(x, y, 1)^T$
- 2D vector = $(x, y, 0)^T$

Vector does not change when translating.

**Matrix representation of translations:**

$$\begin{pmatrix} x' \\ y' \\ w' \end{pmatrix} =
\begin{pmatrix} 1 & 0 & t_{x} \\ 0 & 1 & t_{y} \\ 0 & 0 & 1 \end{pmatrix}\cdot
\begin{pmatrix} x \\ y \\ 1 \end{pmatrix} =
\begin{pmatrix} x + t_{x} \\ y + t_{y} \\ 1 \end{pmatrix}$$

Valid operation if w-coordinate of result is 1 or 0:

- vector + vector = vector
- point - point = vector
- point + vector = point
- point + point = midpoint

In homogeneous coordinates, $\begin{pmatrix} x \\ y \\ w \end{pmatrix}$
is the 2D point $\begin{pmatrix} x / w \\ y / w \\ 1 \end{pmatrix}$,
$w \neq 0$.

**Affine Transformations:**

Affine map = linear map + translation

$$\begin{pmatrix} x' \\ y' \end{pmatrix} =
\begin{pmatrix} a & b \\ c & d \end{pmatrix}\cdot
\begin{pmatrix} x \\ y \end{pmatrix} +
\begin{pmatrix} t_{x} \\ t_{y} \end{pmatrix}$$

Using homogeneous coordinates:

$$\begin{pmatrix} x' \\ y' \\ w' \end{pmatrix} =
\begin{pmatrix} a & b & t_{x} \\ c & d & t_{y} \\ 0 & 0 & 1 \end{pmatrix}\cdot
\begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$$

## **2D Transformations Conclusion**

**Scale:**

$$S(s_{x}, s_{y}) =
\begin{pmatrix} s_{x} & 0 & 0 \\ 0 & s_{y} & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

**Rotation:**

$$R(\alpha) =
\begin{pmatrix} cos\alpha & -sin\alpha & 0 \\ sin\alpha & cos\alpha & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

**Translation:**

$$T(t_{x}, t_{y}) =
\begin{pmatrix} 1 & 0 & t_{x} \\ 0 & 1 & t_{y} \\ 0 & 0 & 1 \end{pmatrix}$$

A new dimension is introduced to the matrix system. However, the last row is $(0, 0, 1)$ at most situations.

## **Other Transforms**

### **Inverse Transform**

$$M^{-1}$$
is the inverse of transform $M$ in both a matrix and geometric sense.

### **Composite Transform**

The order of transformation matters! Translate then rotate makes a different outcome from rotate then translate! (Essentially the same theory as matrix multiplication.)

$$R_{45} \cdot T_{(1, 0)} \neq T_{(1, 0)} \cdot R_{45}$$

Note: Matrices are applied right to left.

Sequence of affine transforms $A_{1}$, $A_{2}$, $A_{3}$, ...

- Compose by matrix multiplication.

$$A_{n}(\dots A_{2}(A_{1}(x))) = A_{n} \dots A_{2} \cdot A_{1} \cdot \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$$

- We pre-multiply n matrices here to obtain a single matrix representing combined transform.

### **Decomposing Transforms**

Rotate around a given point c:

1. Translate center to origin
2. Rotate around origin
3. Translate back

We can represent this operation to:

$$\mathbf{T}(\mathbf{c}) \cdot \mathbf{R}(\alpha) \cdot \mathbf{T}(-\mathbf{c})$$

Note: The operation is right to left!

## **3D Transforms**

Use homogeneous coordinates again:

- 3D point = $(x, y, z, 1)^T$
- 3D vector = $(x, y, z, 0)^T$

Core idea (again): To make translation general.

In general, (x, y, z, w) (w != 0) is the 3D point:

$$(\frac{x}{w}, \frac{y}{w}, \frac{z}{w})$$

We use 4x4 matrices for affine transformations:

$$\begin{pmatrix} x' \\ y' \\ z' \\ 1 \end{pmatrix} =
\begin{pmatrix} a & b & c & t_{x} \\ d & e & f & t_{y} \\
g & h & i & t_{z} \\ 0 & 0 & 0 & 1 \end{pmatrix} \cdot
\begin{pmatrix} x \\ y \\ z \\ 1 \end{pmatrix}$$

Is the order Linear Transform first or Translation first?

- It will be linear map + translation (the same as 2D).
