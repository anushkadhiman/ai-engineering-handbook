# Linear algebra

Linear algebra is the branch of mathematics focusing on linear equations, vector spaces, and matrices used to perform linear transformations. It enables representing multi-variable systems and geometric transformations through numerical operations like matrix addition and multiplication. It is fundamental for computer graphics, engineering, machine learning, and physics.

Here are some most important concepts,

- **Vectors:** The foundational building blocks, interpreted as arrows in space (geometry) or ordered lists of numbers (data).
- **Matrices:** Rectangular arrays of numbers that represent linear operations (like rotation or scaling) or sets of simultaneous equations.
- **Linear Transformations:** Functions that take a vector as input and produce a new vector as output, keeping lines straight and the origin fixed.
- **Systems of Linear Equations:** Often represented as $Ax = b$, where $A$ is a matrix of coefficients, $x$ is the variable vector, and $b$ is the output vector.
- **Eigenvalues and Eigenvectors:** Special vectors of a transformation that do not change direction, only length, which provide deep insights into matrix properties.

**How these concepts are actually used in real world use cases?**

- Machine Learning/AI: Representing data as vectors and applying transformations for models.
- Computer Graphics: Using matrices to perform 2D and 3D rotations, scaling, and shearing.
- Engineering/Physics: Modeling physical phenomena, structural analysis, and solving differential equations.
- Data Analysis: Using techniques like Singular Value Decomposition (SVD) for image compression and data analysis.

Linear algebra acts as a bridge between geometric intuition (graphs, shapes) and numerical calculation (rows of numbers), making it essential for interpreting and manipulating high-dimensional data.

---

## Vectors

In linear algebra, vectors are ordered lists of numbers (components) representing points or directions in $n$-dimensional space ($\mathbb{R}^n$), often visualized as arrows from the origin. They are fundamental objects that can be added together and multiplied by scalars (numbers) to scale their length.

**Here are some key concepts in vector algebra**

- Vector Representation: Usually written as column vectors, e.g., $$
\vec{v} = \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix}
$$.
- Vector Addition: Performed component-wise. If $\vec{u} = \begin{bmatrix} a \\ b \end{bmatrix}$ and $\vec{v} = \begin{bmatrix} c \\ d \end{bmatrix}$, then $\vec{u}+\vec{v} = \begin{bmatrix} a+c \\ b+d \end{bmatrix}$.

- Scalar Multiplication: A scalar $c$ multiplies each component: $c\vec{u} = \begin{bmatrix} ca \\ cb \end{bmatrix}$, scaling the vector's length.
- Geometric Interpretation: An arrow starting at the origin $(0,0)$ and ending at $(v_1, v_2)$.
- Span: The set of all possible linear combinations (additions and scalar multiplications) of a set of vectors.
- Linear Independence: A set of vectors is linearly independent if none can be written as a linear combination of the others.

**What are some types of vectors?**

- Zero Vector: A vector with all components as zero, acting as the additive identity.
- Unit Vector: A vector with a magnitude (length) of 1, often used to indicate direction.
- Basis Vectors: A set of linearly independent vectors that span a vector space, such as the standard basis vectors $\vec{i} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ and $\vec{j} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$ in $\mathbb{R}^2$.

Vectors in linear algebra are foundational for representing data, solving systems of linear equations, and performing transformations in computer graphics and machine learning.

---

## Matrix

A matrix is a rectangular array of numbers, symbols, or expressions arranged in rows and columns, serving as a fundamental tool in linear algebra to represent linear transformations, solve systems of linear equations, and manipulate data. Matrices are defined by their dimensions ($m$ rows $\times$ $n$ columns) and can be added, subtracted, and multiplied when dimensions are compatible.

**Here are some key concepts and operations of matrix,**

- Structure: Matrices are ordered in $m \times n$ grids, where entries are identified by row and column (e.g., $a_{ij}$ is the entry in row $i$ and column $j$).
- Linear Transformations: Matrices represent geometric transformations, such as rotations or scaling, by mapping input vectors to output vectors.
- Matrix Multiplication: The product of two matrices represents the composition of their corresponding linear transformations.
- Special Matrices: Includes square matrices ($n \times n$), identity matrices, symmetric matrices, and zero matrices.
- Operations: Core operations include transposition (switching rows and columns), inversion ($A^{-1}$), determinant calculation ($\det(A)$), and finding eigenvalues/eigenvectors.

**So, what are the applications of matrix?**

- Solving Systems: Used in Gaussian elimination to solve linear equations.
- Computer Graphics: Used for 2D and 3D transformations.
- Data Science/ML: Representing datasets and algorithms like PageRank.
- Physics/Engineering: Analyzing networks and structural mechanics.

---

## Linear Transformation

A linear transformation is a function between two vector spaces that preserves vector addition and scalar multiplication, mapping input vectors to output vectors while keeping grid lines parallel and evenly spaced. Represented by matrix multiplication $T(\mathbf{v}) = A\mathbf{v}$, these transformations map the origin to itself and include operations like rotation, scaling, and shearing.

**Definition and Key Properties**
A mapping $T: V \rightarrow W$ is a linear transformation if it satisfies two fundamental properties for any vectors $\mathbf{u}, \mathbf{v}$ in $V$ and any scalar $c$:

- Additivity: $T(\mathbf{u} + \mathbf{v}) = T(\mathbf{u}) + T(\mathbf{v})$.
- Homogeneity (Scalar Multiplication): $T(c\mathbf{v}) = cT(\mathbf{v})$.

These can be combined into a single property: $T(c\mathbf{u} + d\mathbf{v}) = cT(\mathbf{u}) + dT(\mathbf{v})$.

**Linear Transformations as Matrices**
Every linear transformation $T: \mathbb{R}^n \rightarrow \mathbb{R}^m$ can be represented as an $m \times n$ matrix $A$, such that $T(\mathbf{x}) = A\mathbf{x}$.

- Finding the Matrix : The columns of the matrix $A$ are found by applying the transformation $T$ to the standard basis vectors $\mathbf{e}_1, \ldots, \mathbf{e}_n$ of $\mathbb{R}^n$, resulting in $A = [T(\mathbf{e}_1) \cdots T(\mathbf{e}_n)]$.

**What are some key concepts?**

- Kernel (Null Space): The set of all vectors $\mathbf{v}$ in $V$ such that $T(\mathbf{v}) = \mathbf{0}$.
- Image (Range): The set of all vectors in $W$ that are output by $T$, denoted as $\text{im}(T)$ or $T(V)$.
- Linear Operator: A linear transformation from a vector space to itself ($T: V \rightarrow V$).
- Properties Preserved: Linear transformations take lines to lines (or points) and keep the origin fixed.

**Here are some matrices commonly used in computer graphics and machine learning problems,**

- Rotation: Rotating a vector in $\mathbb{R}^2$ or $\mathbb{R}^3$ around the origin.
- Scaling: Stretching or compressing a vector by a scalar factor.
- Reflection: Reflecting a vector across a line or plane.
- Projection: Projecting a 3D vector onto the $xy$-plane.
- Translation: $T(\mathbf{v}) = \mathbf{v} + \mathbf{b}$ (not linear because $T(\mathbf{0}) \neq \mathbf{0}$).
- Quadratic functions: $T(x) = x^2$ (does not satisfy $T(cv) = cT(v)$).

---

## System of linear equations

A system of linear equations is a set of two or more equations with the same variables, where each variable has an exponent of one. Solutions are found when all equations are satisfied simultaneously, which can result in a unique solution, no solution, or infinitely many solutions. These are solved using methods like Gaussian elimination, substitution, or matrix inversion (represented as $Ax = b$).

**Here are some key concepts and methods:**

- Systems Types: Consistent systems have at least one solution (unique or infinite), while inconsistent systems have no solutions.
- Graphical Representation: In 2D, linear equations are lines; the solution is the intersection point. In 3D, they are planes, and the solution is their intersection line or point.
- Matrix Representation: A system is converted into an augmented matrix for systematic solving.
- Solving Techniques:
  - Gaussian Elimination: Transforms the matrix into row-echelon form to find solutions via back-substitution.
  - Substitution: Solving one equation for a variable and substituting it into another.
  - Row Reduction: Using elementary row operations (swapping, multiplying, adding rows) to solve the system.

- Solutions:
  - Unique Solution: The system intersects at one point.
  - Infinitely Many Solutions: The equations are dependent, representing the same line or plane.
  - No Solution: The lines or planes are parallel and never intersect.

---

## Eigenvalues ($\lambda$) and eigenvectors ($v$)

Eigenvalues ($\lambda$) and eigenvectors ($v$) are fundamental concepts in linear algebra representing the scalars and nonzero vectors that satisfy the equation $Av = \lambda v$ for a square matrix $A$. They define directions that remain unchanged in span when a linear transformation is applied, scaled only by the eigenvalue, forming key tools for diagonalizing matrices, understanding transformations, and solving differential equations.

**What are some core concepts?**

- Eigenvector : A nonzero vector that does not change direction under a linear transformation, only scaled by its eigenvalue.
- Eigenvalue : The scalar factor by which an eigenvector is multiplied (scaled or flipped) during a linear transformation.
- Fundamental Equation: $Av = \lambda v$.
- Geometric Meaning: Eigenvectors remain on their own span (the line passing through the origin and the vector) after the transformation.
- Spectrum: The set of all eigenvalues of a matrix.

**Finding Eigenvalues and Eigenvectors**
To find eigenvalues and eigenvectors of a square matrix $A$:

1. Solve the Characteristic Equation: Find the eigenvalues $\lambda$ by solving $\det(A - \lambda I) = 0$, where $I$ is the identity matrix.
2. Find Eigenvectors: For each eigenvalue $\lambda$, substitute it into $(A - \lambda I)v = 0$ to find the corresponding eigenvector $v$.

**Properties of Eigenvalues and Eigenvectors**

- Trace and Determinant: The sum of eigenvalues equals the trace (sum of diagonal elements) of the matrix, and the product of eigenvalues equals its determinant.
- Triangular Matrices: The eigenvalues of a triangular (upper or lower) matrix are its diagonal entries.
- Invertibility: A matrix is singular (non-invertible) if and only if it has an eigenvalue equal to zero.
- Matrix Powers: If $\lambda$ is an eigenvalue of $A$, then $\lambda^k$ is an eigenvalue of $A^k$.

**Here are some common examples and applications**

- Rotation Matrix (2D): A $90^\circ$ rotation in 2D has no real eigenvalues because no vector remains in the same direction, though it has complex eigenvalues.
- Projection Matrix: Projection matrices have only eigenvalues of 1 and 0.
- Reflection Matrix: Reflection matrices have eigenvalues of 1 and -1.

- Diagonalization: Simplifying a matrix $A = PDP^{-1}$, where $D$ is a diagonal matrix of eigenvalues and $P$ is a matrix of eigenvectors.
- Principal Component Analysis (PCA): Used in data reduction to find the principal components, which are eigenvectors of the covariance matrix.
- Stability Analysis: Used in differential equations to determine stability (eigenvalues with negative real parts indicate stability).
- Machine Learning: Eigenvectors/eigenvalues are used in spectral clustering and dimensionality reduction.
