# NOMAD_GLM_supervised_test
The repository contains the script for performing GLM with lasso-based multinomial regression 

## Inputs:
- `directory`: NOMAD run directory
- `metadata_file`: path to metadata file
- `run_name`: prefix for the output folder
- `input_anchors`: list of specific anchors
- `sample_fraction_cutoff`: cutoff for the minimum fraction of samples each anchor should be present
- `num_anchors`: maximum number of anchors to be tested

## Two options for providing anchors:
- a specific list of anchors can be provided by the user which then every anchor in the list will be tested
- If `sample_fraction_cutoff` and `num_anchors` are provided, among the anchors in `result.after_correction.scores.csv` that are in at least  `sample_fraction_cutoff`% of samples, and have `avg_hamming_distance_max_target` >5, the top `num_anchors` with the highest effect size are selected for being tested by the GLM approach. 

## example commands:
- specific list of anchors:
`Rscript NOMAD_spervised_anchor.R /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/runs/CCLE_all/ /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/utility_files/CCLE_metadata_modified.tsv one_unaligned_target_anchors /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/runs/CCLE_all/concatentaion_based_classified_compactors_one_SJ_one_unaligned.tsv`

- anchors with the highest effect size:
 `Rscript NOMAD_spervised_anchor.R /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/runs/CCLE_all/ /oak/stanford/groups/horence/Roozbeh/NOMAD_10x/utility_files/CCLE_metadata_modified.tsv one_unaligned_target_anchors 0.4 20000`
