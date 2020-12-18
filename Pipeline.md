**Pipeline for human mitogenome assembly from WGS library**
1. reference genome  
```wget -O NC_012920.1.fna "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=NC_012920.1&rettype=fasta&retmode=text"```

1. build bowtie2 index of reference genome  
1. extract pair-end reads for mitogenome assembly   
  
  
