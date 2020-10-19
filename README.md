## Bioinformatics pipeline to measure ribosomal DNA gene copy number using whole genome sequence data

A major advance in the measurement of rDNA copy number has been the emergence bioinformatic approaches that use whole genome (WG) next generation sequencing (NGS) reads to estimate copy number, based on the rationale that sequence coverage of the rDNA is proportional to its copy number. This correlation, in turn, comes about because of rDNA concerted evolution, where the high sequence identity between repeat copies dictates that reads from all copies will map to a single reference rDNA unit, thus providing a high coverage signal that is proportional to rDNA copy number. Existing bioinformatic approaches calculate the mean rDNA read coverage and normalize to the WG mean to estimate copy number, thus assuming that mean coverage represents the “true coverage” for both the rDNA and the WG. However, there are reasons to suspect this mean coverage approach assumption might not always hold. Repetitive elements (e.g. microsatellites and transposons), PCR/sequencing bias (which is particularly evident for the rDNA), and large-scale mutations such as aneuploidies and segmental duplications may all cause the measured mean coverage to differ from the real coverage. While efforts have been made to address some of these potential confounders, estimated copy number varies depending on which part of the rDNA is used, and it has been suggested that the mean coverage approach lacks precision unless coverage is over 65-fold.

Here we present a bioinformatics pipeline that measures rDNA copy number using modal (most frequent) NGS read coverage as a means to overcome limitations of the mean coverage bioinformatics approach. We assessed the parameters important for its performance and validated the pipeline using S. cerevisiae strains with known rDNA copy numbers. We then employed our pipeline to investigate whether distinct S. cerevisiae populations maintain different homeostatic rDNA copy numbers


## Workflow :

This bioinformatics pipeline works as follows :

i. a) It takes a sorted bam file as an input (position sorted bam file), alongwith the indexed reference genome to calculate the per-base coverage value across the reference.
   b) It can also take per-base coverage (.txt) file as an input :
   
   Example file format:
   The per-base read coverage file (from bedtools extracted using -genomecov option) in .txt format with 3 columns as:

### Example :
GenomeID  Baseposition  Depth/Coverage

 Chr1            1               15

ii. It then calculates the frequency for each coverage bin (using given sliding window and bin size) 

iii. Then using the frequency table generated above, it extracts the 3 highest peaks (corresponding to the most frequenct coverage across the base positions) for whole genome and rDNA, and use that to calculate the rDNA copy number.
