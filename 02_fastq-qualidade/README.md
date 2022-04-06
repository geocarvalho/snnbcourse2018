# Usando FASTQC para análise de qualidade

## Instalando FASTQC
```
$ conda install -c bioconda fastqc
```

## Rodar FASTQC nos exemplos

* Entre na pasta `/02_fastq-quality/FASTQC` crie os diretórios e rode o comando abaixo

```
$ mkdir FASTQC cutadapt
$ fastqc ../../00_dados/510-7-BRCA_S8_L001_R1_001.fastq.gz --nogroup -o ./
$ fastqc ../../00_dados/510-7-BRCA_S8_L001_R2_001.fastq.gz --nogroup -o ./
```

> Dúvidas sobre os argumentos usados, use o comando abaixo:

```
$ fastqc --help
```

## Caso a qualidade não esteja boa, use alguma das opções indicadas nos slides. No nosso caso não é preciso, mas abaixo temos um exemplo de comando para para o `cutadapt` excluindo reads no final da sequência com phred score abaixo de 20.

```
$ conda install -c bioconda cutadapt
$ cd ../cutadapt/
$ cutadapt -q 20 -o 510-7-BRCA_S8_L001_R1_001.trimmed.fastq.gz ../../00_dados/510-7-BRCA_S8_L001_R1_001.fastq.gz
$ cutadapt -q 20 -o 510-7-BRCA_S8_L001_R2_001.trimmed.fastq.gz ../../00_dados/510-7-BRCA_S8_L001_R2_001.fastq.gz
```

## Analisando o número de sequências no FASTQ

```
$ gunzip -c ../../00_dados/510-7-BRCA_S8_L001_R2_001.fastq.gz | echo "$((`wc -l` / 4))"
$ gunzip -c ../../00_dados/510-7-BRCA_S8_L001_R1_001.fastq.gz | echo "$((`wc -l` / 4))"
