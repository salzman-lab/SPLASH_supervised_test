# NOMAD GLM-based supervised test
The repository contains the script for performing multinomial regression with lasso to identify and visualize anchors with metadata-dependent target fraction  

## Inputs:
- `directory`: NOMAD run directory
- `metadata_file`: path to metadata file
- `run_name`: prefix for the output folder
- `input_anchors`: list of specific anchors
- `sample_fraction_cutoff`: cutoff for the minimum fraction of samples each anchor should be present
- `num_anchors`: maximum number of anchors to be tested

## Two options for providing anchors:
- providing a list of anchors: each anchor in the list will be considered
- specifying `sample_fraction_cutoff` and `num_anchors`: In this case, among the anchors in `result.after_correction.scores.csv` that are in at least  `sample_fraction_cutoff` of samples, and have `avg_hamming_distance_max_target` >5, the top `num_anchors` with the highest effect size are selected to be tested by the GLM. 

## example commands:
- specific list of anchors:
```
Rscript NOMAD_spervised_anchor.R /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/runs/CCLE_all/ /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/utility_files/CCLE_metadata_modified.tsv one_unaligned_target_anchors /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/runs/CCLE_all/concatentaion_based_classified_compactors_one_SJ_one_unaligned.tsv
```

- anchors with the highest effect size:
 ```
Rscript NOMAD_spervised_anchor.R /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/runs/CCLE_all/ /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/utility_files/CCLE_metadata_modified.tsv one_unaligned_target_anchors 0.4 20000
```
## metadata file format:
The only requirement for metadata file is that the first column must contain sample names and the second column must contain the assigned class/group/category/celltype to each sample and that the first line shoule be column lines (column names can be anything). The two columns are renamed as "sample_name" and "group" in the script. Below is an example metadata file:
```
Run	type
SRR8788980	carcinoma
SRR8788981	melanoma
SRR8788982	lymphoma
SRR8788983	carcinoma
SRR8657060	carcinoma
```
## Output files: 
The output directory for the GLM test is: `directory`/`run_name`_supervised_metadata/.
- `GLM_supervised_anchors.tsv`: the output file containing anchors with non-zero GLM_coefficients whose largest GLM coefficient is greater than 1.
- `plots`: this subfolder contains the plots for visualizing the anchors with metadata-dependent target fraction varaition. For each anchor, two plots will be generated in a pdf named as anchor sequence, a box plot for showing the fraction of target1 per sample grouped by the category and a scatterplot for showing the counts for target1 and target2 per sample colorcoded by the metadata category.  
 
