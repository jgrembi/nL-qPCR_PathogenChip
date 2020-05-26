# nL-qPCR_PathogenChip

Code and datasets associated with evaluation of nL-qPCR for enteric pathogen detection and comparison against a commonly used uL volume enteric TaqMan array card (TAC).

The files include:

## Manuscript Files
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


## Primer Design Files

We have included python scripts used to generate PCR primers and a Docker image with dependencies pre-installed (see [Dockerfile](https://github.com/jgrembi/nL-qPCR_PathogenChip/blob/master/Dockerfile))


[![Docker Repository on Quay](https://quay.io/repository/kmayerb/nlpr/status "Docker Repository on Quay")](https://quay.io/repository/kmayerb/nlpr)


### nlpr - nLPrime 

1. If working on OSX or Windows, download, install and run [Docker Desktop](https://www.docker.com/products/docker-desktop). 
2. With Docker Desktop running, from the command line:

```bash
docker pull quay.io/kmayerb/nlpr:0.0.3
docker run -it quay.io/kmayerb/nlpr:0.0.3
git clone https://github.com/jgrembi/nL-qPCR_PathogenChip.git
cd /nL-qPCR_PathogenChip/nlpr/
python nl_control_file_example.py
``` 

3. After the scripts run, view example outputs generated in `/nL-qPCR_PathogenChip/nlpr/example` folder.

#### nlpr - Inputs

For new runs, three input files are required. They should be formatted like the files in the `nlpr/inputs` folder of this repo.

1. Nuleic Acids fasta `*fna`
2. Protein fasta  `*.faa`
3. Tabular results of an all_v_all blastp or blastn `.all-v-all_blastp_output`


#### nlpr - Run Configuration


Primer design parameters can be configured in `nl_control_file_.py`


Scripts were written to suggests thermodynamically compatible oligonucleotide PCR primer pairs capable of detecting and distinguishing between members of diverse bacterial protein families. For each pathogen associated target gene, PCR assays were designed from nucleic acid sequences of a reference set of pathgen-associated proteins within a larger protein family. Primer3 is a commonly used software for the design of oligonucleotide PCR primers. We used the Primer3 commandline interface with the following parameters to design and evaluate thousands of assays for each set of reference sequences. By using standard Wafergen™ validated assays known to perform well within a standard Wafergen™  thermocycler program, we tuned the input parameters of Primer3 to produce assays with similar predicted thermodynamic binding properties. The parameters used in the control file are provided below and in Mayer-Blackwell et al., [2014](https://pubs.acs.org/doi/pdf/10.1021/es500918w). These parameters produced many high efficiency assays when run at a 60C annealing temperature in the Roche LightCycler SYBR Green I Master Mix. Use of an alternative master mix or annealing temperatures may necessitate re-tuning of these parameters to account for the change in PCR conditions. We used the freely available EMBOSS program fuzznuc to performing fuzzy matching between each candidate assay and the relevant pathogen-specific target genes. This permitted evaluation of how many target and off-target genes within a query set were complementary to each primer pair, given a specified maximum number of mismatches. 


#### nlpr - Primer3 settings from Mayer-Blackwell et al. 2014.
```
PRIMER_NUM_RETURN=2500 PRIMER_MIN_TM=59
PRIMER_OPT_TM=60
PRIMER_MAX_TM=61
PRIMER_MIN_SIZE=15
PRIMER_MAX_SIZE=28 
PRIMER_NUM_NS_ACCEPTED=1 
PRIMER_PRODUCT_SIZE_RANGE=75-200 
PRIMER_GC_CLAMP=0
PRIMER_FILE_FLAG=1 
PRIMER_EXPLAIN_FLAG=1 
PRIMER_TM_FORMULA=1 
PRIMER_SALT_CORRECTIONS=1 
PRIMER_THERMODYNAMIC_ALIGNMENT=1 
PRIMER_SALT_DIVALENT=3 
PRIMER_DNTP_CONC=0.6 
PRIMER_LIB_AMBIGUITY_CODES_CONSENSUS=0 
```

#### nlpr - Citing 

If you use these scripts in your research, please cite:

* EMBOSS: The European Molecular Biology Open Software Suite (2000) Rice,P. Longden,I. and Bleasby,A. Trends in Genetics 16, (6) pp276—277

* Mayer-Blackwell, K., Azizian, M. F., Machak, C., Vitale, E., Carpani, G., de Ferra, F., ... & Spormann, A. M. (2014). Nanoliter qPCR platform for highly parallel, quantitative assessment of reductive dehalogenase genes and populations of dehalogenating microorganisms in complex environments. Environmental science & technology, 48(16), 9659-9667.

* Rozen, S., & Skaletsky, H. (2000). Primer3 on the WWW for general users and for biologist programmers. In Bioinformatics methods and protocols (pp. 365-386). Humana Press, Totowa, NJ.



#### Legacy versions of software used 

* cd-hit-v4.5.4-2011-03-07.tgz [download](https://www.dropbox.com/s/34ybl944fkcefds/cd-hit-v4.5.4-2011-03-07.tgz?dl=1)

* primer3-2.3.4.tar.gz [download](https://www.dropbox.com/s/z7x7tx1cmvwvl9h/primer3-2.3.4.tar.gz?dl=1)

* ncbi-blast-2.2.18-universal-macosx.tar.gz [download](https://www.dropbox.com/s/y2jeajmxgcho0bt/ncbi-blast-2.2.18%2B-universal-macosx.tar.gz?dl=1)

* silix-1.2.6.tar.gz [download](https://www.dropbox.com/s/rlctg1chfxqr13c/silix-1.2.6.tar.gz?dl=1)

