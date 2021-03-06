<!-- Generated by Docile.jl -->

# GeometryTypes - Types

## Hyper Geometry

<a name="GeometryTypes.HyperRectangle"></a>

A `HyperRectangle` is a generalization of a rectangle into N-dimensions. Formally it is the cartesian product of intervals, which is represented by the `origin` and `width` fields, whose indices correspond to each of the `N` axes.

<a name="GeometryTypes.HyperSphere"></a>

A `HyperSphere` is a generalization of a sphere into N-dimensions. A `center` and radius, `r`, must be specified.

## Primitives

<a name="GeometryTypes.Simplex"></a>

A `Simplex` is a generalization of an N-dimensional tetrahedra and can be thought of as a minimal convex set containing the specified points.

  * A 0-simplex is a point.
  * A 1-simplex is a line segment.
  * A 2-simplex is a triangle.
  * A 3-simplex is a tetrahedron.

Note that this datatype is offset by one compared to the traditional mathematical terminology. So a one-simplex is represented as `Simplex{2,T}`. This is for a simpler implementation.

It applies to infinite dimensions. The sturucture of this type is designed to allow embedding in higher-order spaces by parameterizing on `T`.

<a name="GeometryTypes.LineSegment"></a>

An alias for a one-simplex, corresponding to LineSegment{T} -> Simplex{2,T}.

<a name="GeometryTypes.Circle"></a>

An alias for a HyperSphere of dimension 2. i.e. Circle{T} -> HyperSphere{2, T}

<a name="GeometryTypes.Sphere"></a>

An alias for a HyperSphere of dimension 3. i.e. Sphere{T} -> HyperSphere{3, T}

## Meshes

<a name="GeometryTypes.HomogenousMesh"></a>

The `HomogenousMesh` type describes a polygonal mesh that is useful for computation on the CPU or on the GPU. All vectors must have the same length or must be empty, besides the face vector Type can be void or a value, this way we can create many combinations from this one mesh type. This is not perfect, but helps to reduce a type explosion (imagine defining every attribute combination as a new type).

### Faces

<a name="GeometryTypes.Face"></a>

A Face is typically used when constructing subtypes of `AbstractMesh` where the `Face` should not reproduce the vertices, but rather index into them. Face is parameterized by:

  * `N` - The number of vertices in the face.
  * `T` - The type of the indices in the face, a subtype of Integer.

## DistanceFields

<a name="GeometryTypes.SignedDistanceField"></a>

A `SignedDistanceField` is a uniform sampling of an implicit function. The `bounds` field corresponds to the sampling space intervals on each axis. The `data` field represents the value at each point whose exact location can be rationalized from `bounds`. The type is parameterized by:

  * `N` - The dimensionality of the sampling space.
  * `SpaceT` - the type of the space where we will uniformly sample.
  * `FieldT` - the type resulting from evaluation of the implicit function.

Note that decoupling the space and field types is useful since geometry can be formulated with integers and distances can be measured with floating points.

## Abstract Types

<a name="GeometryTypes.GeometryPrimitive"></a>

Abstract to categorize geometry primitives of dimensionality `N`.

<a name="GeometryTypes.AbstractSimplex"></a>

Abstract to classify Simplices. The convention for N starts at 1, which means a Simplex has 1 point. A 2-simplex has 2 points, and so forth. This convention is not the same as most mathematical texts.

<a name="GeometryTypes.AbstractMesh"></a>

No documentation found.

**Summary:**

```julia
abstract GeometryTypes.AbstractMesh{VertT,FaceT} <: GeometryTypes.GeometryPrimitive{N,T}
```

**Subtypes:**

```julia
GeometryTypes.HomogenousMesh{VertT,FaceT,NormalT,TexCoordT,ColorT,AttribT,AttribIDT}
```

<a name="GeometryTypes.AbstractDistanceField"></a>

No documentation found.

**Summary:**

```julia
abstract GeometryTypes.AbstractDistanceField <: Any
```

**Subtypes:**

```julia
GeometryTypes.AbstractSignedDistanceField
GeometryTypes.AbstractUnsignedDistanceField
```
