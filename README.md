# GenOMICC_Pancreatitis

Repository containing instructions to reproduce GWAS analyses for the Pancreatitis phenotype.

## Reproducing the UKB-GenOMICC GWAS

To run the GWAS, we only need the [WDL-GWAS](https://github.com/olivierlabayle/WDL-GWAS) pipeline, make sure you have followed the installation instructions and run the following:

```bash
input_config=config/genomicc-inputs.pancreatitis.meta.regenie.json
compiled_input_config=config/genomicc-inputs.pancreatitis.meta.regenie.dx.json
output_dir=/or4_pancreatitis_regenie

# Clone WDL-GWAS pipeline
git clone https://github.com/olivierlabayle/WDL-GWAS

# Compile the workflow
java -jar $DX_COMPILER_PATH compile WDL-GWAS/workflows/gwas.wdl \
    -f -project $RAP_PROJECT_ID \
    -extras WDL-GWAS/config/extras.json \
    -reorg \
    -folder /workflows/gwas \
    -inputs ${input_config}

# Run the workflow
dx run -y \
    -f ${compiled_input_config} \
    --priority high \
    --preserve-job-outputs \
    --destination ${output_dir} \
    /workflows/gwas/gwas
```

## Reproducing the AoU GWAS

The WDL-GWAS workflow can also used on All of Us, to set it up, follow the instructions [here](https://support.workbench.verily.com/docs/guides/workflows/cromwell/). The configuration file used for the GWAS is `config/gwas.aou.config`.