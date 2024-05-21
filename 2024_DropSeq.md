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
