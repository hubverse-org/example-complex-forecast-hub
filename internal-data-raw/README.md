# Source data for examples

This folder is not part of the official hubverse structure, and should not be included in repositories used to house new modeling hubs. It contains the original data files and code used to create the target data and model output files for this example hub.

## Recreating the target data and model output files

To recreate the target data:

```bash
Rscript internal-data-raw/create_target_data.R
```

To recreate the model output files:

```bash
Rscript internal-data-raw/create_model_output_data.R
```
