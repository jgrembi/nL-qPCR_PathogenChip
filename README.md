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

### Inputs

For new runs, three input files are required. They should be formatted like the files in the `nlpr/inputs` folder.

1. Nuleic Acids fasta `*fna`
2. Protein fasta  `*.faa`
3. Tabular results of an all_v_all blastp or blastn `.all-v-all_blastp_output`


### Run Configuration

Primer design parameters can be configured in `nl_control_file_.py`


### Archive of legacy versions of software used 

- cd-hit-v4.5.4-2011-03-07.tgz [download](https://www.dropbox.com/s/34ybl944fkcefds/cd-hit-v4.5.4-2011-03-07.tgz?dl=1)

- primer3-2.3.4.tar.gz [download](https://www.dropbox.com/s/z7x7tx1cmvwvl9h/primer3-2.3.4.tar.gz?dl=1)

- ncbi-blast-2.2.18-universal-macosx.tar.gz [download](https://www.dropbox.com/s/y2jeajmxgcho0bt/ncbi-blast-2.2.18%2B-universal-macosx.tar.gz?dl=1)

- silix-1.2.6.tar.gz [download](https://www.dropbox.com/s/rlctg1chfxqr13c/silix-1.2.6.tar.gz?dl=1)

