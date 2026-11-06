# Exercise 3: Run nf-core/viralrecon pipeline

*(Note that you can view an outline of this document by clicking the icon that
looks like a bullet point list, to the far right just above the header above)*

We ran `sierra-local` in the previous exercise to predict HIV drug resistance mutations locally.

The good news is that this tool has already been integrated into the `nf-core/viralrecon` nextflow pipeline `dev` branch through a collaboration between Karolinska Institutet, Karolinska University Laboratory, and the Bioinformatics Unit of Instituto de Salud Carlos III. The original work was done by [Sarai Varona](https://github.com/svarona) and [Lili Andersson-Li](https://github.com/LilyAnderssonLee). We are preparing for a new release of the viralrecon pipeline this December.

[nf-core/viralrecon](https://github.com/nf-core/viralrecon/tree/dev) is a bioinformatics analysis pipeline used to perform assembly and intra-host/low-frequency variant calling for viral samples. The pipeline supports both Illumina and Nanopore sequencing data.

In this exercise, we will run the nf-core/viralrecon pipeline on three publicly availabe samples: **DRR030302, SRR4071760 and SRR6937100**. These three samples are also used as examples in [Stanford HIVdb](https://hivdb.stanford.edu/hivdb/by-reads/) web interface

