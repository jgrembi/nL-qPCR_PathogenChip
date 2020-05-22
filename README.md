# nL-qPCR_PathogenChip
Code and datasets associated with evaluation of nL-qPCR for enteric pathogen detection and comparison against a commonly used uL volume enteric TaqMan array card (TAC).

The files include:

- **nL-qPCR_AnalysisScripts_Dec2019.Rmd** Code for all analyses contained in manuscript *High-throughput multi-parallel enteropathogen quantification via nano-liter qPCR* published on [bioRxiv](https://doi.org/10.1101/746446)

- **chipData_target.RDS** Dataset containing all nL-qPCR data for the 38 nL-qPCR chips run for this project.  This includes initial testing of multiple assays on an instrument in Fremont, CA as well as later testing on an instrument located in the Genomics Core Facility at Michigan State University. The dataset includes all raw data directley exported from the SmartChip instrument, as well as additional variables manually added for:
    - chipNum : the chip number (1-38)
    - Chip : a designation of the facility (WAF or MSU) plus chipNum 
    - TargetName : name of the gene for which the assay targets
    - labelName : label with organism and TargetName, e.g. EAEC (*aggR*)  
    - Type : descriptor for the type of assay including Pathogenic *E. coli*, Bacteria, Helminthes/Parasites (HP), General (for total Bacteria, Archaea, and Fungi assays), or Quality Control
    - operator : Instrument operator for run, if known

- **df.TAC.RDS** Dataset of enteric pathogen results via an enteric TaqMan array card qPCR (TAC) from fecal samples collected from children in rural Bangladesh as part of the WASH Benefits cluster-randomized controlled trial.

- **std.curve.all.RDS** Dataset containing the standard curves from the TAC instruments used for evaluation of the TAC dataset.

- **TACvWafergen.csv** Dataset identifying assay names targeting equivalent targets (either gene or organims) between the nL-qPCR and TAC datasets
