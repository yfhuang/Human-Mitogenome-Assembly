**Pipeline for human mitogenome assembly from WGS library**
1. Download reference genome from NCBI GenBank  
```wget -O NC_012920.1.fna "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=NC_012920.1&rettype=fasta&retmode=text"```  
1. build bowtie2 index of reference genome  
```bowtie2-build NC_012920.1.BW2Idx NC_012920.1.fna```
1. extract pair-end reads for mitogenome assembly   
```bowtie2 -x NC_012920.1.BW2Idx -1 QCRead.R1.fastq -2 QCRead.R2.fastq --local -p 12 [--no-mixed --no-discordant] | grep -v "^@" | aw -F"\t" '{if($3!="*") print $1} | uniq | awk '{if($1 > 1) print $@}' > Mitoread.list```  
```seqtk subseq QCRead.R1.fastq Mitoread.list > QCRead.Mito.R1.fastq```  
```seqtk subseq QCRead.R2.fastq Mitoread.list > QCRead.Mito.R2.fastq```  
1. de novo genome assembly  
```magahit -1 QCRead.Mito.R1.fastq -2 QCRead.Mito.R2.fastq -o megahit_out```  
1. identify mitogenome from contigs  

  
  
