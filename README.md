# FDK_recon

## Creating projection geometry and volume geometry using Astra
For volume geometry: vol_geom = astra.create_vol_geom(n_rows, n_cols, n_slices), here the numbers refer to the voxels of the cubic that we wanna reconstruct. For projection geometry: take parallel_3d as an instance. proj_geom = astra.create_proj_geom('parallel3d', 1, 1, detector_rows, detector_cols, angles), it's related to the detector_rows and detector_cols, and angles is related to the number of projections.

Note that for the phantom case, n_rows, n_cols and n-slices of voxels equal to the pixels of Shepp-logan phantom. The shepp-logan has the dimension (n,n,n), thus vol_geom = astra.creators.create_vol_geom(n, n, n). For convenience, we could just set detector_rows and detector_cols to be the same as pixels(also it could be eg.500 as long as we want). As for the number of projections, it could be varied from e.g. 16 to 256, whatever is wanted.

Also for slices in volume geometry, it could be only 5, and slices_data, could be only 8. Reference shown in a diagram in the notes about proximal splitting algorithms.

## Creating projection geometry and volume geometry using Tomosipo
In practice, construct projection geometry and volume geometry with tomosipo, which is significantly faster than Astra. Note that for few-view CT, to create vectors for projection geometry, not only should we change angles, but rotation step as well.

## Read CT scan data
Do 2d shift, this one will stronly affect the denoising performance of our algorithms. (As for tilt and 3d shift, they do not affect the performance that much, thus omitted here).
