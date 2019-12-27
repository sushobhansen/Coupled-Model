## Files for Coupled Model

Files for the coupled pavement-urban canyon model used in this paper:
Sen, S., & Roesler, J. (2019, January). Coupled pavement-urban canyon model for assessing cool pavements. In *International Airfield and Highway Pavements Conference 2019: Innovation and Sustainability in Highway and Airfield Pavement Technology* (pp. 207-215). American Society of Civil Engineers (ASCE).

Run on OpenFOAM v 6.0 and Python3

### To use 
Generate the mesh

```
gmsh -3 Urban3D.geo Urban3D.msh
```

Import the mesh into OpenFOAM:

```
gmshToFoam Urban3D.msh
```
Modify polyMesh with appropriate boundary conditions (not automated yet)

Run the following command from the terminal inside any of the folders:

```bash
bash runthis
```

The following processes will be run:

1. Any leftover processor or post-processing folders will be deleted
2. Any leftover log files will be deleted (use `mv` to rename if you need it!)
3. Any intermediate output folders will be deleted
4. The domain will be decomposed based on `decomposeParDict`
5. Parallel run of renumberMesh (edit to specify number of processors; use `nproc`to check how many are available)
6. The solver is run (buoyantBoussinesqSimpleFoam; OpenFOAM v 7.0 uses a different command)
7. Subdomain solutions are reconstructed 
8. Post-processing steps executed (varies, check file)

Use the following command to for some additional plots:

```bash
bash plotresiduals
```

### For coupled iteration
Run the following command to obtain canopy-average 2 m air temperature and wind speed (results stored in `canopydata.csv`:

```python
python3 canopyaverage.py
```

Use the data to update boundary conditions in `0/` and run the next iteration. I just take the average of all the data. 