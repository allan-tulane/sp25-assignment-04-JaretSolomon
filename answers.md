Jaret Solomon

1a.
A d-ary heap is a generalization of a binary heap where each node can have up to d children instead of just 2. This structure still forms a complete tree. The height of a heap with n elements is approximately log base d of n (log₍d₎n), meaning that increasing the number of children per node results in a shorter overall tree.
1b.
In a d-ary heap, removing the smallest element (the root) involves moving a leaf to the root and repeatedly swapping it down the tree to restore the heap property. Each level of this 'sift down' process requires comparing the node to its d children, leading to a runtime of O(d log₍d₎ n) for delete-min. Inserting an element means adding it at the end and sifting it up by comparing it with its parent—this only requires one comparison per level, for a total cost of O(log₍d₎ n).
1c.
When using a d-ary heap in Dijkstra’s algorithm, we need to account for the cost of heap operations. There’s one delete-min per vertex and up to one insert (or decrease-key) per edge. This gives us O(|V| d log₍d₎ |V|) work for the deletions and O(|E| log₍d₎ |V|) for the insertions, totaling O(|V| d log₍d₎ |V| + |E| log₍d₎ |V|).
1d.
To reduce the overall time to O(|E|), the term |V| d log₍d₎ |V| must not exceed O(|E|). This can be achieved by selecting d = Θ(|V|^ε), where ε > 0. This increases the branching factor and flattens the tree, which makes log₍d₎ |V| constant. As a result, the delete-min term becomes O(|E|) as well.
2a.
Shortest path weights:

k = 0:
[0][ -2][  2]
[∞][  0][  1]
[∞][ ∞ ][  0]

k = 1:
[0][ -2][ -1]
[∞][  0][  1]
[∞][ ∞ ][  0]

k = 2:
[0][ -2][ -1]
[∞][  0][  1]
[∞][ ∞ ][  0]
2b.
As k increases, APSP(i, j, k) can only get better (smaller or equal) since we can now go through one more intermediate vertex. For example: APSP(i, j, 2) = min(APSP(i, j, 1), APSP(i, 2, 1) + APSP(2, j, 1)). This shows how each new level of computation builds upon the last by allowing paths through one more node.
2c.
The recurrence APSP(i, j, k) = min(APSP(i, j, k−1), APSP(i, k, k−1) + APSP(k, j, k−1)) represents the idea of optimal substructure: the shortest path either avoids vertex k entirely or uses it. This fundamental choice drives the dynamic programming approach.
2d.
Since each of the i, j, and k indices ranges over |V| vertices, the total number of subproblems is |V|³. Memoizing results ensures each one is only solved once, leading to O(V³) overall work—efficient for dense graphs compared to redundant recalculations.
2e.
Johnson’s algorithm runs in O(|V||E| log |V|), while the dynamic programming method takes O(|V|³). For dense graphs (where |E| ≈ |V|²), Johnson’s complexity can be worse than cubic time. So, the DP approach is preferable for graphs with many edges or when needing to handle negative weights without cycles.
3a.
A minimum spanning tree (MST) doesn't always minimize the largest edge in the tree (the MMET). An MST minimizes total edge weight, while an MMET focuses on keeping the heaviest edge as small as possible. An MST might include a very large edge if it helps reduce total cost, even though it wouldn’t be ideal for MMET. Thus, the MST and MMET solutions may differ.
3b.
To find the second-best spanning tree, start with the MST. Then, for each edge in it, remove that edge and compute a new MST without it. This gives alternative spanning trees. Track the total weights of each and return the smallest one that's higher than the original MST's cost.
3c.
This process includes one initial MST computation and one for each of its n−1 edges. Each MST takes O(E log V) time, so the full process takes O(n E log V), where n is the number of vertices.
