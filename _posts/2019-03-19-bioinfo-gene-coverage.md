---
layout: post
title: 【生信】检查panel中特定基因的测序覆盖度
tags: 生信 annovar samtools
category: 生信
date: 2019-03-19 23:00:00
---

## 注释基因的捕获区域
```
awk '{print $0"\t0\t-"}' brcaPanel.bed > brcaPanel.avinput

bash anno_refgene.sh brcaPanel.avinput

grep BRCA2 brcaPanel.avinput.annovar.hg19_multianno.txt | cut -f 1-3,6,10 | cut -d ':' -f 1-3 > BRCA2_anno.bed

grep BRCA1 brcaPanel.avinput.annovar.hg19_multianno.txt | cut -f 1-3,6,10 | cut -d ':' -f 1-3 > BRCA1_anno.bed

```

## 检查覆盖度
```
samtools bedcov BRCA2_anno.bed test.final.bam | awk '{print $1,$2,$3,$4,$5,$6/($3-$2+1)}' | cut -f 1 -d '.' > BRCA2.exon.cov.txt

samtools bedcov BRCA1_anno.bed test.final.bam | awk '{print $1,$2,$3,$4,$5,$6/($3-$2+1)}' | cut -f 1 -d '.' > BRCA1.exon.cov.txt
```

### 代码:anno_refgene.sh
```
#!/bin/bash

name=$1
/rawdata/Zhangyu/software/ANNOVAR_latest/annovar/table_annovar.pl $name \
/rawdata/Zhangyu/software/ANNOVAR_latest/annovar/humandb \
-buildver hg19 \
-otherinfo \
-remove \
-nastring . \
-protocol refGene \
-operation g \
--outfile ${name}.annovar
```

<center>-END-</center>
