# MRI_surface_functions
Python functions for loading and manipulating a surface and functional map as a
[graph object](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics))
(made with help from [Umut Canoluk](https://github.com/dafrius)).

The functions in this repository allow you to do a few things that might not be
so easy in FSL. To use them, you have to think of the surface, the functional
maps, the labels/patches as a [graph
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

## Example use: get MNI coordinates of surface activity 

<img align="left" width="65%" src="/images/cluster.gif">

Another use case is the turn the blobs of activation in a surface map into
clusters, and then report the MNI coordinates. Below is the script to do that.

```python
import matplotlib.pyplot as plt
import mesh_functions as mf
import numpy as np

# make a graph object with the surface and a functional map
G = mf.surf_and_map_to_graph(surf_name, map_name, ext='mgh')

# define clusters (taking all blobs separated by nan values)
clusters = mf.define_clusters(G, cluster_size_thresh=0, map_thresh=None, ignore_nans=True)

# find out each blob's MNI coordinates
mni_dict = mf.get_cluster_coords(surf_name, clusters, np_func_cen=np.median)

# write those coords to a txt file
mf.cluster_coords_to_txt(mni_dict, f'mni_cluster_coords_{map_name_only}_median.txt')


# plot the functional map and the clusters
to_plot = [list(v) for k,v in clusters.items()]

ax = mf.plot_nodes(G, surf_name, alpha = 1)
mf.setzoomed3Dview(ax, 230, 15, 5)
plt.show()

ax = mf.plot_nodes(G, surf_name, node_sets=to_plot,
                   colors = ['black',  'yellow',  'green',
                             'cyan',    'blue',   'green',
                             'pink',   'purple', 'cyan',
                             'orange', 'magenta', 'white',
                             'red',    'blue',   'yellow',
                             'pink',   'purple', 'cyan',
                             'orange', 'magenta', 'yellow',
                             'red',    'blue',   'green'], alpha = 0.01)
mf.setzoomed3Dview(ax, 230, 15, 5)
plt.show()
```
