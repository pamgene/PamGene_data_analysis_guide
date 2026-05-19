
Differential `Phosphosite Analysis` using the Bioconductor package LIMMA (linear models for micro arrays): [https://bioconductor.org/packages/release/bioc/html/limma.html](https://bioconductor.org/packages/release/bioc/html/limma.html)

LIMMA is used to apply linear modeling to PamChip experiments over all included test conditions.

Subsequently, all pairwise comparisons (contrasts) are analyzed.

LIMMA, instead of analyzing each peptide in isolation compared to a T-test, uses information from all the peptides and conditions in the experiment to improve its analysis. This is like asking, "What can we learn from the whole group to help us understand each individual better?" This is done by applying the empirical Bayes method to calculate differences (the t-statistic), borrowing information from all peptides.

Applying LIMMA leads to results with increased statistical power (i.e. the ability to detect real differences) over individual testing per peptide (with for example t-tests). Therefore, LIMMA can detect smaller differences that might otherwise be missed. This makes the analysis more robust, especially when only limited data is available.

**References**

Ritchie ME, Phipson B, Wu D, Hu Y, Law CW, Shi W, Smyth GK (2015). “limma powers differential expression analyses for RNA-sequencing and microarray studies.” Nucleic Acids Research, 43(7), e47. doi:10.1093/nar/gkv007.