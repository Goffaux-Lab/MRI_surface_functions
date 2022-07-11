# MRI_surface_functions
Python functions for loading and manipulating a surface and functional map as a
[graph object](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics))
(made with help from [Umut Canoluk](https://github.com/dafrius)). The functions
in this repository allow you to do a few things that might not be so easy in
FSL. To use them, you have to think of the surface, the functional maps, the
labels/patches as a [graph
object](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics)) (some idea
is given below).

<img align="left" width="65%" src="/images/done.gif">

A brain surface is made from vertices (those are the individual dots you see in
the image) connected by edges (those are not drawn, but you can imagine that
each dot is connected to it's neighbours by a line (or 'edge') so as to form a
lot of triangles).

For a brain surface, you also have information about where each vertex is
located in 3D space. This extra information allows you to plot all the vertices
in a 3D scatterplot, but the important information is which vertices are
connected to each other by edges.

With fMRI data, we often have functional maps that we display on the surface.
Maps are a set of values - one per vertex. So we can color code the vertices
according to the map value to show how the map looks.

Labels are also a set of vertices, and so we can plot those vertices in a
different color. The black line in the image is the V1 border (that is, the
vertices that are labelled as the border of V1). The pink region is a label
that we are growing - that is, a set of vertices to which we are gradually
adding more vertices.
