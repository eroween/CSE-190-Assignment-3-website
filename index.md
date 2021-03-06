---
layout: default
---

### Basic subdivision routine: 

#### Introduction

For this milestone on Assignment 3 we implemented Catmull-Clark Subdivision by repeatedly subdividing the faces of the mesh into smaller faces. As a proof of concept we split the edges using the midpoint formula. However we intend to implement Catmull-Clark by finding the new vertices’ location using a weighted combination of older vertex position. This is a basic example of subdivision by approximation which follows a set of refining rules to reallocate the original vertices.

{% include youtube.html id='chy8pF0clJU' %}

The rules to be implemented are the following :

1. At each iteration all faces are divided into four child faces.
2. New vertices are added along the edges (split edges).
3. The positions of the new vertices are computed using weighted averages of neighboring vertices
4. The position of each original vertex are updated with the weighted average of it position and the the position of neighboring vertices.

{% include youtube.html id='AaIO27J-dO4' %}

#### Mesh Data Structure

We have implemented a face oriented mesh data structure, composed by these two structure :


The face structure :

    struct Face
    {
        std::vector<Vertex *>     m_vertices;
        std::vector<Face *>     m_adjacent_faces;
        std::vector<Face *>     m_child_faces;
    }

and the vertex structure :

    struct Vertex
    {
        Face *        m_face;
    }


The data structure is optimized to do the subdivision part. In order to subdivide the face into 4 sub faces, we just need to allocate 4 new face and update the corresponding pointers.

#### Subdivision

The subdivision part is done recursively, given the fact that the subdivision is done by one level at the time. We just need to call the subdivision routine on the parent face and the recursive call will subdivide the face itself and each of its children.

The same process is used in order to compute the data for the mesh rendering.

### Future Work:

Even though a few iterations throughout the subdivision loop will give us a good approximation of the the limit surface. We intend to evaluate subdivision at arbitrary points on the surface by implementing Stam’s 98 algorithm on “Exact Evaluation of Catmull-Clark Subdivision Surface at Arbitrary Parameter Values”.

We also intend to develop a routine to computer tangents, normal and curvatures (Gauss and Mean) at the vertices.

