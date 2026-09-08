# Lecture 8: Collaborative Engineering Architecture, Systems of Linear Equations, Matrix Foundations, and Computational Linear Algebra via Maven

**Date:** 4 July 2026
**Course:** CSC360: Computer Graphics and Interaction

---

### Collaborative Group Project Architecture and Repository Governance

The eighth lecture marked a significant structural pivot in the course, transitioning from individual exploratory assignments to a multi-developer group software project. We initiated this phase by examining project scoping, architectural division of labor, and the creation of a centralized GitHub repository to host the project codebase. Developing software in a distributed team requires strict organizational discipline to prevent merge conflicts, inconsistent coding standards, and diverged development branches.

We established foundational Git governance protocols for the group repository. Teams must define a protected main branch that represents stable, production-ready code, while utilizing dedicated feature branches for individual contributions. This workflow requires developers to submit pull requests accompanied by peer code reviews before any integration occurs. Furthermore, maintaining repository hygiene requires an agreed-upon .gitignore file tailored to Java and Maven projects, ensuring that local workspace configurations, compiled bytecode directories, and environment variables are never committed. By configuring branch protection rules, standardizing commit message conventions, and establishing automated continuous integration builds on repository pushes, the group structure mirrors industry-standard collaborative engineering practices.

---

### Mathematical Foundations: Systems of Linear Equations and Matrix Representations

Shifting into graphics mathematics, the lecture established a rigorous theoretical foundation in linear algebra, focusing on systems of linear equations and their direct translation into matrix equations. Computer graphics fundamentally relies on transforming geometric points in space. Whether rotating a 3D polygonal mesh, scaling a 2D bounding box, or projecting virtual coordinates onto a 2D screen surface, every operation is modeled as a linear transformation applied to vectors.

We explored how a classical system of simultaneous linear equations can be represented compactly as a single matrix vector product:

$$A \mathbf{x} = \mathbf{b}$$

Consider a concrete system of linear equations in three variables:

$$2x + 3y + 1z = 8$$
$$4x + 1y - 2z = -2$$
$$-2x + 5y + 3z = 10$$

In this formulation, the coefficients of the unknowns form the coefficient matrix $A$ of dimension $3 \times 3$:

$$A = \begin{pmatrix} 2 & 3 & 1 \\ 4 & 1 & -2 \\ -2 & 5 & 3 \end{pmatrix}$$

The unknowns constitute the vector $\mathbf{x}$, and the constant values on the right side form the vector $\mathbf{b}$:

$$\mathbf{x} = \begin{pmatrix} x \\ y \\ z \end{pmatrix}, \quad \mathbf{b} = \begin{pmatrix} 8 \\ -2 \\ 10 \end{pmatrix}$$

Expressing the system in matrix notation allows graphics engines to process spatial transformations uniformly. Instead of computing coordinate changes through ad-hoc algebraic substitutions, graphics pipelines leverage optimized matrix multiplication, Gaussian elimination, and matrix decomposition algorithms to solve for unknown position states across thousands of vertices simultaneously.

---

### Vector Geometry: Row Vectors versus Column Vectors

A critical topic of discussion centered on the geometric and computational distinctions between row vectors and column vectors, and how their dimensional orientations dictate matrix multiplication conventions across different graphics APIs.

Mathematically, an $n$-dimensional vector represents a directed quantity possessing both magnitude and spatial direction. However, its algebraic structure can be arranged in two distinct formats:
* **Row Vector:** A horizontal $1 \times n$ matrix, where elements are arranged in a single row across $n$ columns.
* **Column Vector:** A vertical $n \times 1$ matrix, where elements are arranged in a single column down $n$ rows.

To illustrate this difference with a concrete example, consider a point located at coordinate $(4, -2, 7)$ in three-dimensional space. 

As a row vector $\mathbf{v}_{\text{row}}$, it is written as:

$$\mathbf{v}_{\text{row}} = \begin{pmatrix} 4 & -2 & 7 \end{pmatrix}_{1 \times 3}$$

As a column vector $\mathbf{v}_{\text{col}}$, it represents the transpose of the row vector:

$$\mathbf{v}_{\text{col}} = \begin{pmatrix} 4 \\ -2 \\ 7 \end{pmatrix}_{3 \times 1} = \mathbf{v}_{\text{row}}^T$$

The algebraic significance of this distinction becomes apparent during matrix transformation operations. Matrix multiplication is defined only when the number of columns in the first matrix equals the number of rows in the second matrix. Consequently, the chosen vector orientation determines whether transformations are applied via pre-multiplication or post-multiplication.

When using column vectors, standard in mathematical textbooks, OpenGL, and Java graphics pipelines, transformations are applied via post-multiplication:

$$\mathbf{v}' = M \mathbf{v}$$

Here, a $3 \times 3$ transformation matrix $M$ multiplies the $3 \times 1$ column vector $\mathbf{v}$, yielding a new $3 \times 1$ transformed column vector $\mathbf{v}'$. If multiple sequential transformations are applied, such as rotation $R$ followed by scaling $S$ and translation $T$, the operations chain from right to left:

$$\mathbf{v}' = T \cdot S \cdot R \cdot \mathbf{v}$$

Conversely, when using row vectors, common in frameworks like DirectX, transformations are applied via pre-multiplication:

$$\mathbf{v}' = \mathbf{v} M$$

Here, the $1 \times 3$ row vector $\mathbf{v}$ multiplies the $3 \times 3$ transformation matrix $M$, yielding a new $1 \times 3$ transformed row vector $\mathbf{v}'$. In this convention, sequential transformations chain naturally from left to right:

$$\mathbf{v}' = \mathbf{v} \cdot R \cdot S \cdot T$$

Understanding this dual convention prevents orientation errors, coordinate transposition bugs, and shader pipeline failures when translating mathematical specifications into executable graphics code.

---

### Determinants and Computational Linear Algebra via Maven

The lecture concluded by exploring the geometric meaning of determinants and examining how modern build tools like Maven enable efficient matrix computation in Java.

The determinant of a square matrix represents the scalar factor by which a linear transformation scales area in two dimensions or volume in three dimensions. For instance, given a $2 \times 2$ transformation matrix:

$$M = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$$

The determinant is calculated as:

$$\det(M) = ad - bc$$

If the determinant evaluates to zero ($\det(M) = 0$), the transformation collapses the spatial dimensions into a line or a single point, indicating that the matrix is singular and cannot be inverted. An invertible matrix ($\det(M) \neq 0$) guarantees that geometric transformations can be reversed, which is fundamental for converting world-space coordinates back to camera-space or screen-space coordinates during ray picking and rendering. Furthermore, a negative determinant signals that the transformation has flipped the coordinate orientation, such as a reflection across an axis.

While writing bespoke nested loops to compute determinants and matrix multiplications serves as a helpful academic exercise, doing so in production software is error-prone, numerically unstable, and computationally inefficient. Standard floating-point arithmetic can suffer from catastrophic cancellation errors and performance bottlenecks when handling large transformation pipelines.

This is where Apache Maven becomes indispensable for computational linear algebra. Rather than implementing matrix mathematics from scratch, developers can leverage Maven dependency management via pom.xml to integrate high-performance, battle-tested linear algebra libraries. Prominent Java libraries include:
* **Apache Commons Math:** Provides robust linear algebra modules (such as Array2DRowRealMatrix, LUDecomposition, and QRDecomposition) that solve systems of linear equations, invert complex matrices, and calculate determinants with numerical stability.
* **EJML (Efficient Java Matrix Library):** A specialized, high-performance linear algebra library engineered for real-time graphics and robotics, offering low memory overhead and optimized matrix decomposition algorithms.
* **JOML (Java OpenGL Math Library):** Tailored specifically for 2D and 3D graphics rendering, supplying optimized transformation matrices, quaternions, and projection vectors designed for tight render loops.

By declaring these dependencies inside pom.xml, Maven automatically downloads the required binaries, validates transitive dependencies, and links native computational routines. This enables graphics engineers to focus on scene composition, pipeline architecture, and visual interaction while relying on verified mathematical backends for low-level matrix computations.

---

### Curated Resources and Further Reading

#### Linear Algebra and Matrix Transformation Fundamentals
* 3Blue1Brown: Essence of Linear Algebra (Essential visual series covering linear transformations, matrix multiplication, determinants, and coordinate space changes).
* Immersive Math by J. Ström, K. Åström, and T. Akenine-Möller: Interactive Linear Algebra (Interactive textbook detailing row versus column vectors, affine transformations, and cross products).
* Scratchapixel: Matrix Operations and Graphics Transformations (Technical breakdown of homogenous coordinates, matrix multiplication, and transformation chaining).

#### Computational Java Libraries & Build Integration
* Apache Commons Math: Linear Algebra User Guide (Official documentation explaining RealMatrix, LU decomposition, and solving linear systems).
* EJML (Efficient Java Matrix Library) Official Repository: Performance Benchmarks and Matrix Decomposition (In-depth analysis of high-throughput linear algebra implementations in Java).
* JOML (Java OpenGL Math Library) Wiki: Matrix Conventions in Graphics Programming (Practical guide on row-major vs. column-major memory layouts and column vector multiplication).

#### Repository Management and Collaborative Git Workflows
* Atlassian Git Guides: Comparing Git Workflows and Feature Branching (Comprehensive guide on team branch protection, pull request reviews, and merge conflict resolution).
* GitHub Documentation: Managing Protected Branches and Repository Permissions (Step-by-step instructions for enforcing review policies and automated status checks on team repositories).
