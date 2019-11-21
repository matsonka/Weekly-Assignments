Commands for Weekly Assignment 9
We are using our data from Weekly Assingment 8 to construct our plots. So this was my commands from weekly assignment 8:

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


For plotting for weekly assignment 9:


check to make sure that our previously installed packages are working
library(readr)
library(tidyverse)
library(DESeq2)


Install new packages
if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install("dada2")
BiocManager::install("phyloseq")

make sure they were installed properly
library(dada2)
library(phyloseq)


ggplot
Add a column indicating significance
res=mutate(res,significance=ifelse(padj<0.05,"Significant","Non-significant")) 
res=mutate(res,significance=ifelse(padj<0.05 & log2FoldChange>=2,"Control", ifelse(padj<0.05 & log2FoldChange<=-2,"Mutant", "Non-significant")))

Make the volcano plot that shows the differentially expressed genes (control points=blue, mutant points=red). I made the non-significant genes yellow since those also needed a color. Also, the volcano plot needs a title so I will title mine Differentially Expressed Genes since that is what we are looking at
volcano <- ggplot(res) +
  geom_point(aes(x=log2FoldChange, y=-log10(padj), colour=significance)) +
  ggtitle("Differentially Expressed Genes") +
  xlab("log2 fold change") +
  ylab("-log10 adjusted p-value") +
  #scale_y_continuous(limits = c(0,50)) +
  theme(legend.position = "none",
        plot.title = element_text(size = rel(1.5), hjust = 0.5),
        axis.title = element_text(size = rel(1.25)))  +
  theme_bw()
volcano + scale_colour_manual(values = c("blue", "red", "yellow"))


From Weekly Assignment 8 I know that the gene with the highest positive fold change is Solyc09g089500.2.1, so I can make the box plot for this gene. The box plot needs a title so I will title it Highest Positive Fold Change: Solyc09g089500.2.1 since that is the gene expression that we are looking at.
Commands for the box plot of the expression of the gene with the highest positive fold chage:

plotCounts(dds, gene="Solyc09g089500.2.1", intgroup="dex")
plotCounts(dds, gene="Solyc09g089500.2.1", intgroup="dex", returnData=TRUE)
plotCounts(dds, gene="Solyc09g089500.2.1", intgroup="dex", returnData=TRUE) %>%
  ggplot(aes(dex,count))+
  geom_boxplot()
plotCounts(dds, gene="Solyc09g089500.2.1", intgroup="dex", returnData=TRUE) %>%
  ggplot(aes(dex,count))+
  geom_boxplot(aes(fill=dex))+
  scale_y_log10() + 
  ggtitle("Highest Positive Fold Change: Solyc09g089500.2.1")



From Weekly Assignment 8 I know that the gene with the highest negative fold change is Solyc11g028040.1.1, so I can make the box plot for this gene. This box plot needs a title so I will title it Highest Negative Fold Change: Solyc11g028040.1.1 since that is the gene expression that we are looking at for this plot.
Commands for the box plot of the expressio of the gene with the highest negative fold change

plotCounts(dds, gene="Solyc11g028040.1.1", intgroup="dex")
plotCounts(dds, gene="Solyc11g028040.1.1", intgroup="dex", returnData=TRUE)
plotCounts(dds, gene="Solyc11g028040.1.1", intgroup="dex", returnData=TRUE) %>%
  ggplot(aes(dex,count))+
  geom_boxplot()
plotCounts(dds, gene="Solyc11g028040.1.1", intgroup="dex", returnData=TRUE) %>%
  ggplot(aes(dex,count))+
  geom_boxplot(aes(fill=dex))+
  scale_y_log10() + 
  ggtitle("Highest Negative Fold Change: Solyc11g028040.1.1")
  
  
Make a MA plot, which are plots that are log10 of the mean expression (baseMean) of a gene on the x-axis and log2FoldChange on the y-axis
What is an MA plot? From wikipedia website https://en.wikipedia.org/wiki/MA_plot: "The plot visualizes the differences between measurements taken in two samples, by transforming the data onto M (log ratio) and A (mean average) scales, then plotting these values."


To make this plot I took notes to make the command from the website https://chapmandu2.github.io/post/2017/02/21/bioinformatics-in-the-tidyverse/


I am going to title the plot MA Plot since that's the kind of plot it is. Here are the commands I used from this, which I figured out using the reference website:
ma_plot <- ggplot(res, aes(log10(baseMean), log2FoldChange, colour=padj<0.5)) + 
  geom_point(size=rel(1.5), aes(text=row)) + theme_bw() + ggtitle("MA Plot")
ma_plot

To copy the plots to a word document:
In RStudio in the plots that are shown in the lower right quadrant, select export. Then I selected copy to clipboard, then I selected copy plot, and then I just pasted the plot into the word document. I did this for all of the plots.


Use the data generated from Weekly Assignment 8 to construct the following plots.

A volcano plot showing differentially expressed genes - color the Control points blue and the Mutant points Red.
A box plot of the expression of the gene with the highest positive fold change
A box plot of the expression of the gene with the highest negative fold change
An MA. MA plots are log10 of the mean expression (baseMean) of a gene on the x-axis and log2FoldChange on the y-axis.
