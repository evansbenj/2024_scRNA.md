# DropSeq

I am using the Drop-seq cook book to extract count data from fastq files from scRNA data from XL embryos

```
https://mccarrolllab.org/dropseq/
```

The data are from:
```
Lio et al. (2022) Nature Communications 13:4306 
```

I followed the protocol pretty much exactly except I did not run the `DetectBeadSubstitutionErrors` or `DetectBeadSynthesisErrors` options because they did not seem to work for me. I used the `BAMTagHistogram` program to figure out how many cells to assay for `DigitalExpression`, which is the counting program.

# Plotting BanTagHistogram

```R
setwd("/Users/Shared/Previously\ Relocated\ Items/Security/benstuff/\ \ \ \ \ 2024_grants/NSF_2024/single_cell/XL_embryo_scRNAseq/Drop-Seq")
options(scipen=999)

a=read.table("SRR19560472_out_cell_readcounts.txt.gz", header=F, stringsAsFactors=F) 
x=cumsum(a$V1)
x=x/max(x)

p <- ggplot(a, aes(x=1:length(x), y=x)) +
  geom_line() +
  xlim(1,100000) +
  xlab("Cell barcodes sorted by\n # of reads [descending]") +
  ylab("Cum fraction of reads") +
  theme_classic(base_size = 6) +
  # make it clean
  theme_bw()+ theme(panel.grid.minor=element_blank(),panel.grid.major=element_blank()) + 
  # add a title
  ggtitle("SRR19560472")  +
  theme(legend.background = element_blank(),
        legend.box.background = element_blank(),
        legend.key = element_blank()) +
  theme(text = element_text(size = 8))

ggsave(p, file = "SRR19560472_hist.jpg",  width = 5, height = 5, units="cm")

```

I had problems with annotating using TagReadWithGeneFunction, I think because the format of the gtf file did not have any "gene" annotation in the 3rd column. I modified this by making a new gtf file
```
module load StdEnv/2020 gffread/0.12.3
gffread -E XENLA_10.1_Xenbase_longest.gff3 -T -o XENLA_10.1_Xenbase_longest.gtf
sed -i 's/transcript    /gene   /g' XENLA_10.1_Xenbase_longest.gtf
```
