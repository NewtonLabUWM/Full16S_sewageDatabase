# Wastewater microbial marker gene reference database

<b>Lou LaMartina, Angie Schmoldt, Ryan Newton</b>

Full-length 16S rRNA gene sequences, from 27F to 1492R and regions V1-V9. DNA sequences from the PacBio Sequel II were curated with DADA2, mothur, and Silva v.138. Sample information, FASTA sequences, counts, and taxonomy are publicly available in multiple formats.


## Data access

- [Google Drive](https://drive.google.com/drive/folders/1lfjwUHkiLNQoR53-yt8B6eLNDEsZCWob?usp=sharing) (curated)

- [GitHub](https://github.com/loulanomics/Full16S_sewageDatabase/tree/main/Files) (curated)

- [NCBI Sequence Read Archive](https://www.ncbi.nlm.nih.gov/Traces/study/?acc=PRJNA809416&o=acc_s%3Aa) (raw, demultiplexed)


## Dataset

### ASV files

Amplicon sequence variants (ASVs), or unique DNA sequences, of 16S ribosomal RNA genes from wastewater bacteria. <b>Counts</b> files are the number of times (reads) that ASVs occur in each sample. <b>Taxonomy</b> files show the taxonomic classification of ASVs from Kingdom to Species. ASV names range from ASV0001 to ASV1041, ranked from most to least abundant.

### OTU files

Operational taxonomic units (OTUs) were generated by grouping ASVs that were at least 99.5% similar. OTU names range from OTU001 to OTU681, ranked from most to least abundant. If there was no consensus in taxonomy among ASVs within an OTU, the proportion of reads belonging to that ASV is in its name. For example, OTU011 was 16 ASVs all in the genus <i>Acidovorax</i>, but they were mixed with <i>defluvii</i> (11), <i>carolinensis</i> (4), or were unclassified (1) to species. Among all the reads in OTU011 (5568), 67% (3719) were assigned to <i>defluvii</i>, while <i>carolinensis</i> and unclassified were 16% and 17%, respectively. Therefore, the OTU names are OTU011_67, OTU011_17, and OTU011_16.
  
### Analysis files
  
<b>FASTA.</b>  DNA sequences of ASVs. Sequence headers include ASV ID, taxonomic assignments, read count, and read direction (R1/R2).

<b>Phyloseq. </b>  ASV or OTU counts combined with taxonomy and sample metadata in a single object, for easy exploration in R ([website](https://joey711.github.io/phyloseq/)).


### Code

R scripts to organize and explore data, calculate statistics, and create plots.

## Sample set

In total, 46 wastewater treatment plant influent (raw sewage) underwent 16S rRNA gene sequencing. Samples encompass a wide range of bacterial diversity over space and time, according to previous studies ([1](https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-021-01038-5), [2](https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-021-01038-5)). <b>Temporally</b>, 24 sewage samples were collected once a month for two years from a single treatment plant. <b>Spatially</b>, 22 treatment plants were sampled from across the US, with southern samples from summer and northern samples from winter.


## Analysis

<b>1.  Marker gene.</b>  Hypervariable and conserved regions (V1-V9) were PCR-amplified at 27F and 1492R. Unique barcodes were appended to primers to allow  sequencing of all samples simultaneously (multiplex).

- 12 forward [barcodes](https://github.com/PacificBiosciences/Bioinformatics-Training/blob/master/barcoding/pacbio_384_barcodes.fasta) (0007_Forward - 0018_Forward)
- 4 reverse barcodes (reverse complements; 0004_Forward - 0007_Forward)
- 27F:AGRGTTYGATYMTGGCTCAG and 1492R:RGYTACCTTGTTACGACTT universal primer set

<b>2.  DNA sequencing.</b>  PCR amplicons were sequenced in multiplex on a PacBio Sequel II.

<b>3.  Data processing.</b>  Data files were subsetted to individual samples according to their assigned barcodes. Cutadapt was used to trim primers and barcodes from reads, [DADA2](https://benjjneb.github.io/dada2/tutorial.html) generated ASV counts and assigned taxonomy, and [mothur](https://mothur.org/wiki/cluster/) clustered ASVs into OTUs.

