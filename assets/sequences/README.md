# `assets/sequences` `README.md`

This directory contains sequences in support of BM214 workshop 3.

The `isolate_1_16SrDNA.fasta` sequence is what was used to generate some of the figures/screengrabs. The sequence is unrelated to the exercises otherwise (it's a _Deinococcus_).

The `*_16s.fasta` multisequence files are RefSeq 16S full-length sequences for the named organisms, obtained with a search of the format:

```text
txid1396[ORGN] AND (biomol_rrna[PROP] AND refseq[filter]) AND 16s[All Fields]
```