# Brain Region Network Motif Analysis

## Project Description

This project constructs a brain network based on Brodmann cortical partitions using a NIfTI file (`Brodmann_YCG.nii`). It performs motif analysis to detect statistically significant subgraph patterns in the network. The analysis helps understand structural and functional connectivity in the brain.

## Dependencies

Make sure Python 3 is installed, along with the following packages:

```bash
pip install numpy nibabel networkx matplotlib scipy pandas tqdm
```

---

## Usage Steps

1. Place `Brodmann_YCG.nii` in your working directory.  
2. Run the provided script or Jupyter notebook.  
3. **Adjacency matrix**: Constructs by dilating each region and detecting overlaps; saved as `adjacency_matrix.csv`.  
4. **Network visualization**: Builds a NetworkX graph, computes centroids for each region, and outputs `brain_network.png`.  
5. **Motif enumeration**: Calls `enumerate_subgraphs` for sizes 3, 4, and 5.  
6. **Statistical test**: Uses `motif_pvalues` to compare counts against randomized networks; prints top motifs and saves results to `motif_results.csv`.  

## Output

- `adjacency_matrix.csv`: 0/1 matrix indicating spatial adjacency between Brodmann areas.  
- `brain_network.png`: 3D visualization of the brain network.  
- `motif_results.csv`: Table of motif counts, random-network statistics, and p-values.  
- **Console output**: Top 5 motifs (by p-value) for sizes 3, 4, and 5.  

## Methodology

- **Region adjacency**: Perform a 3D dilation (radius=1) of each region’s voxel mask and check overlaps to build the adjacency matrix.  
- **Subgraph enumeration**: Enumerate all combinations of 3, 4, and 5 nodes, extract induced subgraphs, and encode each motif by the upper triangle of its adjacency matrix.  
- **Random network generation**: Apply NetworkX’s `double_edge_swap` to preserve degree distribution while randomizing edges.  
- **Significance testing**: Compare real vs. randomized motif counts to compute p-values, identifying statistically significant motifs.  

## Notes and Precautions

- Ensure `Brodmann_YCG.nii` is valid and readable by NiBabel.  
- Randomization parameters (`n_rand`, number of swaps) affect runtime and stability—adjust as needed.  
- Motif enumeration scales combinatorially; use `tqdm` to monitor progress.  
- Interpret p-values near 0 or 1 as highly significant or not significant, respectively.  
