# QCMP Tree
Quadripartite Concentric Manhattan Partitioning (QCMP) tree is a 2D grid partitioning tree designed for efficient direction agnostic ray casting and tracing

## Term Glossary

| Term              | Explanation                                                      |
|-------------------|------------------------------------------------------------------|
| Section           | A chosen section of 2D grid that is closed                       |
| Cell              | Individual cell of the 2D grid in question                       |
| Quadrant          | One of the four divisions relative to the central point          |
| Filled Cell       | Any cell of the 2D grid that is considered a solid               |
| Manhattan Diamond | The outer cells of Manhattan distance `n` from the central point |
| EUCD              | Euclidean distance                                               |

## Tree Contruction

### Pre-Configuration

In order to construct a QCMP tree, a certain set of pre-configurations need to be done. These are generalisable to any 2D grid structure, as such can be assured for any desired layout. They are as follows:

1. Find the closest "filled" cell to the centre of the section
2. Ensure that the grid is closed by adding adjacent cells away from the central point if need be
3. From the centre outwards, (excluding the centre) index each of the cells in the concentric Manhattan neighbours in order of up, right, down, left

### Construction

After you have done the pre-configuration, we start with the central point and work through each of the filled cells in the concentric Manhattan diamonds. To start off, assign the central point to the root node of the tree. With each iteration perform the following:

1. Iterate over the filled cells of the current Manhattan diamond
2. Get the relative position of the filled cell to the central point (One of U, D, L, R)
3. Traverse the branch of the tree according to the relative position found
5. Calculate the EUCD to the root node for the current node
6. Calculate the EUCD to the root node for the filled cell being inserted
7. If the EUCD for the current node is greater choose the left branch, otherwise choose the right
8. If the current node is not a leaf node traverse the chosen branch and repeat steps 5-9
9. If the current node is a leaf node, insert the node according to the chosen branch
10. Terminate the tree construction
