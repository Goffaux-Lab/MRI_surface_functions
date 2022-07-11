# MRI_surface_functions
Python functions for loading and manipulating a surface and functional map as a
[graph object](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics)). The
functions in this repository allow you to do a few things that might not be so
easy in FSL. To use them, you have to think of the surface, the functional
maps, the labels/patches as a [graph
object](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics)) (some idea
is given below.

<img align="left" width="65%" src="/images/done.gif">

A surface is made from vertices (those are the individual dots you see in the
image) connected by edges (those are drawn, but you can imaging that each dot
is connected to it's neighbours so as to form a lot of triangles).

For a brain surface mesh, you also have information about where each vertex is
in 3D space. This extra information allows you to plot it in a 3D scatterplot,
but either way the important information is contained in which vertices are
connected to which other vertices by edges.

With fMRI data, we often have functional maps that we display on the surface.
Maps are a set of values - one per vertex. So we can color code the vertices
according to the map value to show how the map looks.

Labels are also a set of vertices, and we can plot those vertices in a
different color. The black line in the image is the V1 border (that is, the
vertices that are labelled as the border of V1). The pink region is a label
that we are growing - that is, a set of vertices that we are gradually adding
more vertices to.
