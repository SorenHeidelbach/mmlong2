# mmlong2
Automated long-read metagenomics workflow, using either PacBio HiFi or Nanopore sequencing reads as input to generate characterized MAGs.
Mmlong2 is a continuation of [mmlong](https://github.com/SorenKarst/mmlong).

**Note:** At the moment, mmlong2 is an in-house pipeline at Aalborg University Bioservers. A distributable version of the pipeline is scheduled for a future release.
<br/>
<br/>

**Usage example for hybrid (Nanopore/Illumina) mode:** <br/>
`./mmlong2 -np [Nanopore_reads.fastq] -il [Illumina_reads.fastq] -t [Threads] -o [Output_dir]`
<br/>

**Full usage:**
```
READ INPUTS: 
-np		Nanopore_reads.fastq
-il		llumina_reads.fastq
-pb		PacBio_CCS_reads.fastq

OPTIONAL INPUTS:
-o		Output directory
-tmp		Temporary file directory
-t		Threads
-flye_min_cov	Set read coverage minimum for Flye assembly (default: 3)
-flye_min_ovlp	Set minimum read overlap for Flye assembly (default: 0/AUTO) 
-racon_rounds	Specify no. of Racon polishing rounds (default: 0)
-medaka_rounds	Specify no. of Medaka polishing rounds (default: 1)
-medaka_conf	Specify Medaka polishing model (default: r1041_e82_400bps_sup_g615)
-medaka_conf2	Specify Medaka variant model (default: r1041_e82_400bps_sup_variant_g615)
-cov		Space-sperated dataframe of additional read data to be used for binning (NP/PB/IL /path/to/reads.fastq)
-stop		Stop workflow after a specified stage completes: "assembly" "polishing" "metagenome-taxonomy" 
		"assembly" "polishing" "taxonomy" "binning" "qc" "annotation" "variants"

EXTRA:
-h OR -help	Display help file
-version	Display workflow version
-info		Display information file
```
<br/>

**Comments:**
* The workflow assumes that the input reads have been quality-filtered and adapter/barcode sequences have been trimmed off.
* The workflow is long-read-based and requires either Nanopore or PacBio HiFi reads. It doesn't feature an Illumina-only mode.
* If the workflow crashes, it can be resumed by re-running the same command.
* Medaka parallelisation is capped at 20 instances.
* MetaBinner and Vamb binners require a complex metagenome to run, and thus will exit with an error when reads for a low-complexity metagenome are provided.
* When the workflow is running with a large amount of threads (eg. 100), CheckM2 or GTDB-tk can get stuck. This can be fixed by running the workflow at 40 threads.
