Commands for Weekly Assignment 8

First we have to make sure that we have the packages installed
install.packages("readr")
install.packages("tidyverse")
if (!requireNamespace("BiocManager", quietly = TRUE)) install.packages("BiocManager") 
BiocManager::install("DESeq2")


library(readr)
library(tidyverse)
library(DESeq2)


mycounts <- read_csv("data/WA_counts.csv")        The data is the folder where my WA_counts and WA8_metadata data are contained in
metadata <- read_csv("data/WA8_metadata.csv")


head(mycounts)
head(metadata)

class(mycounts)

mycounts <- as.data.frame(mycounts)
metadata <- as.data.frame(metadata)

class(mycounts)

names(mycounts)[-1]
metadata$id
names(mycounts)[-1]==metadata$id
all(names(mycounts)[-1]==metadata$id)

dds.data <- DESeqDataSetFromMatrix(countData=mycounts, 
                                   colData=metadata, 
                                   design=~dex, 
                                   tidy=TRUE)
dds.data

dds <- DESeq(dds.data)


res <- results(dds, contrast=c("dex","Control","Mutant"), tidy=TRUE)        The Control and the Mutant are what we are comparing
res <- tbl_df(res)
res

res2 <- arrange(res, padj)
res3 <- filter(res2, padj<=0.05 & log2FoldChange>=2)      This will tell us how many significantly different genes there are
res4 <- filter(res2, padj<=0.05 & log2FoldChange<=-2)



1.	How many genes are significantly differentially expressed?
•	2,404  genes are significantly differentially expressed
•	(padj<=0.05 & log2FoldChange>=2, and padj<=0.05 & log2FoldChange<=-2), so we add the 915 genes + 1,489 genes=2,404 genes
2.	How many genes are significantly differentially expressed in the Control versus the Mutant?
•	There are 915 genes that are significantly differentially expressed in the Control versus the Mutant
•	(padj<=0.05 & log2FoldChange>=2)
3.	How many genes are significantly differentially expressed in the Mutant versus the Control?
•	There are 1,489 genes that are significantly differentially expressed in the Mutant versus the Control
•	(padj<=0.05 & log2FoldChange<=-2)
4.	What gene is the most highly expressed gene in the Mutant versus the Control?
•	Solyc11g028040.1.1
5.	What gene is the most highly expressed gene in the Control versus the Mutant?
•	Solyc09g089500.2.1
