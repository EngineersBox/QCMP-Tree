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

#### V1

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

#### V2

TODO

## Ray Casting with a QCMP Tree

### V1

TODO

### V2

Variables:
| Identifier | Description               |
|------------|---------------------------|
| `c`        | Current node in question  |
| `r`        | Set of rays to be queried |
| `q`        | Current branch            |
| `p`        | Ray origin                |

1. Set `c` to the root node
2. Check for intersections with each ray in `r`
3. Set `q` to the relative directional quadrant from `c`
4. If `q` does not exist as a branch from `c`, set `q` to the quadrant closest in EUCD to `p`
5. Traverse the `q` from `c`
6. Set `c` to new node after traversal
7. Check for intersections with each ray in `r`, store it temporarily
8. If a new intersection is found check if there exists a branch in the direction from `c` to `p`
9. If there is a branch traverse the next node and check if it is between `c` and `p`
10. Repeat steps 8-9 until the closest node is found.
11. Repeat steps 3-6 until all rays have closest intersections
