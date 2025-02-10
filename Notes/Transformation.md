# **Transformation**

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

> We have an example of $s = 0.5$ (Scaling the image to 0.5x of its original.)
>
> $$
> x' = sx \\ y' = sy
> $$
>
> We can turn this to a matrix computation.
>
> $$
> \begin{bmatrix} x' \\ y' \end{bmatrix}
> = \begin{bmatrix} s_{x} & 0 \\ 0 & s_{y} \end{bmatrix}
> \begin{bmatrix} x \\ y \end{bmatrix}
> $$
>
> $ \begin{bmatrix} s*{x} & 0 \\ 0 & s*{y} \end{bmatrix} $
> is the scaling matrix (缩放矩阵).
> $x$ and $y$ can scale unevenly (i.e. $s_{x} = 0.5, s_{y} = 1.0$)

### **Reflection**

> Horizontal reflection:
> $$ x' = -x \\ y' = y $$
> We can get a general form of matrix operation here:
>
> $$
> \begin{bmatrix} x' \\ y' \end{bmatrix}
> = \begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix}
> \begin{bmatrix} x \\ y \end{bmatrix}
> $$

### **Shear**

> An example of a rectangle: \
> Horizontal shift is $0$ at $y = 0$ but is $a$ at $y = 1$. \
> Vertical shift is always $0$. \
> Rectangle coordinates: \
> $(0, 0), (0, 1), (1, 1), (1, 0)$ becomes $(0, 0), (0, 1), (a + 1, 1), (a, 1)$ after the operation. \
> We can now get a general form of matrices:
>
> $$
> \begin{bmatrix} x' \\ y' \end{bmatrix}
> = \begin{bmatrix} 1 & a \\ 0 & 1 \end{bmatrix}
> \begin{bmatrix} x \\ y \end{bmatrix}
> $$

### **Rotate**

> The rotation is in a 2D plane. The shape rotates around the point $(0, 0)$. The rotation goes counter-clockwise. \
> We can get a general form here, in which all angles are in degree:
>
> $$
> R_{\theta} =
> \begin{bmatrix} cos\theta & -sin\theta \\ sin\theta & cos\theta \end{bmatrix}
> $$
>
> For example, $(0, 0), (0, 1), (1, 1), (1, 0)$.
>
> $$
> \begin{bmatrix} x' \\ y' \end{bmatrix} =
> \begin{bmatrix} A & B \\ C & D \end{bmatrix}
> \begin{bmatrix} x \\ y \end{bmatrix}
> $$
>
> $$
> \begin{bmatrix} cos\theta \\ sin\theta \end{bmatrix} =
> \begin{bmatrix} A & B \\ C & D \end{bmatrix}
> \begin{bmatrix} 1 \\ 0 \end{bmatrix}
> $$
>
> Similarly, we can compute the complete formula.

### **Linear Transforms = Matrices**

> We can get a general form:
>
> $$
> x' = ax + by \\
> y' = cx + dy \\
> $$
>
> $$
> \begin{bmatrix} x' \\ y' \end{bmatrix} =
> \begin{bmatrix} a & b \\ c & d \end{bmatrix}
> \begin{bmatrix} x \\ y \end{bmatrix} \\
> $$
>
> $$
> x' = Mx
> $$
>
> These are all linear transforms of the same dimension, involving with simple linear multiplications. \

## **Homogeneous Coordinates**

### **Translation**

Translating a shape or points from one place to another. We can get the general form of translation formula:
$$ x' = x + t_{x} \\ y' = y + t_{y} $$
Translation cannot be directly represented in matrix form. It is not a linear transform! We need to add an extra matrix after the multiplication operation.

Is there a unified way to represent all transformations?

- It is
