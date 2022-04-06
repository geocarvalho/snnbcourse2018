# Download e preparação do genoma de referência

> Espera-se que o BWA e samtools estejam instalados para criação dos indexes (senão, ver a instalação desses itens no README.md dessa mesma pasta.

## Para fazer download do genoma inteiro (incluindo seus contigs extras):

```
$ cd genome
$ wget --timestamping 'ftp://hgdownload.cse.ucsc.edu/goldenPath/hg19/chromosomes/*'
$ ls chr* | xargs cat > ucsc.hg19.fa 
```

## Para esse tutorial só precisamos de chr13 e chr17, para facilitar é possível criar um novo arquivo com eles:

```
$ cd genome
$ for fasta in $(ls *.gz); do gunzip ${fasta}; done
$ ls chr* | xargs cat > ucsc-chr13-chr17.hg19.fa
```

## Gerar arquivos de index do fasta e para o BWA

```
$ bwa index -a bwtsw ucsc-chr13-chr17.hg19.fa
$ samtools faidx ucsc-chr13-chr17.hg19.fa
```

## Quais os contigs no genoma de referência e quantas linhas de DNA eles possuem?

```
$ grep '>' ucsc-chr13-chr17.hg19.fa
$ grep -v '>' ucsc-chr13-chr17.hg19.fa | wc -l
```

## Links interessantes:

* [Question: Where Can I Download Human Reference Genome In Fasta Format? Hgref.Fa File](https://www.biostars.org/p/1796/)
* [Download Human Reference Genome (HG19 - GRCh37)](https://www.gungorbudak.com/blog/2014/04/13/download-human-reference-genome-hg19/)
* Para usar o kit de ferramentas GATK, você precisa preparar o genoma de referência:
> [How can I prepare a FASTA file to use as reference?](https://gatkforums.broadinstitute.org/gatk/discussion/1601/how-can-i-prepare-a-fasta-file-to-use-as-reference)

> [Prepare a reference for use with BWA and GATK](https://gatkforums.broadinstitute.org/gatk/discussion/2798/howto-prepare-a-reference-for-use-with-bwa-and-gatk)
