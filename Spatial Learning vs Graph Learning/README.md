
### Images vs Point Clouds:

Images have a regular spatial domain, so the order and location of pixels are very important. That is why the kernel filters in convolution layers have 
particular shape; it imposes certain structure. On the other hand, such regularity and certain structure are not observed on point clouds. In other words, 
point clouds are of irregular format. When we rotate a point cloud, we change the coordinates and locations of the points. However, the point cloud 
continues to depict same object, since the transformation would be applied to each point in the cloud. In other words, the order of the points is not 
important. This irregularity provides permutation and transformation invariance for point clouds. 

### Graphs:

The graphs have also irregular and invariant characteristics, so we cannot apply convolutions to the data represented in a graph. To be able to do deep 
learning at the top of these new domains, we need to have irregular learning approaches. At this point, graph neural networks enter the picture, and 
come up with some solutions to two main challenges.

* Challenge 1: Variable sized inputs
  * The number of nodes and edges can vary in graphs. 
  * Our networks in a social media tend to get bigger as more people are followed

* Challenge 2: Invariance to node permutations
  * The learning technique that will be applied to the point clouds and graphs should not depend on the order, permutation and location of the nodes.
  * It needs to treat each node as same as all other nodes.
