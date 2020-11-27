## Filtering Illumina sequence

The following pipeline were used for filter Illumina sequence of two sets of data: (i) whole genomic DNA (gDNA); and (ii) probes of entire chromosomes (obtained by flow sorting and fragmented by a DOP-PCR reaction). Both samples from the species *Holochilus sciureus* (2n = 56+1B, NF = 56), a Neotropical rodent of Oryzomyini tribe.


### Softwares used

FastQC v0.10.1

http://www.bioinformatics.babraham.ac.uk/projects/fastqc/

BBMap_38.49.tar

https://jgi.doe.gov/data-andtools/bbtools/bb-tools-user-guide/bbduk-guide/

Trimmomatic-0.39.zip

http://www.usadellab.org/cms/?page=trimmomatic

Bolger AM, Lohse M, Usadel B (2014) Trimmomatic: A flexible trimmer for Illumina Sequence Data. Bioinformatics, 30(15):2114–2120.


### Whole genomic DNA

The process were performed using Trimmomatic with the set of Illumina adapters from BBMap. FastQC was used to verify the libraries quality and to determine the parameters to be used.

Parameters used:
- phred33: Specifies the base quality encoding
- ILLUMINACLIP: Will cut the adapters and other illumina-specific sequences from the read.
- LEADING: Will cut bases off the start of a read, if below a threshold quality.
- TRAILING: Will cut bases off the end of a read, if below a threshold quality.
- SLIDINGWINDOW: Will performs a sliding window trimming approach. It starts scanning at the 5‟ end and clips the read once the average quality within the window falls below a threshold.
- HEADCROP: Will cut the specified number of bases from the start of the read.
- MINLEN: Wil drop the read if it is below a specified length.

Comand line used:
java -jar Trimmomatic-0.39/trimmomatic-0.39.jar PE -phred33 read_r1.fastq read_r2.fastq out_r1_paired.fq.gz out_r1_unpaired.fq.gz out_r2_paired.fq.gz out_r2_unpaired.fq.gz ILLUMINACLIP:/bbmap/resources/adapters.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 HEADCROP:15 MINLEN:95
