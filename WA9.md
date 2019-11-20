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

if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install("dada2")
BiocManager::install("phyloseq")

ggplot

res=mutate(res,significance=ifelse(padj<0.05,"Significant","Non-significant")) 


To make basic volcano plot:
ggplot(res) +
  geom_point(aes(x=log2FoldChange, y=-log10(padj), colour=significance)) +
  ggtitle("Mov10 overexpression") +
  xlab("log2 fold change") + 
  ylab("-log10 adjusted p-value") +
  #scale_y_continuous(limits = c(0,50)) +
  theme(legend.position = "none",
        plot.title = element_text(size = rel(1.5), hjust = 0.5),
        axis.title = element_text(size = rel(1.25)))  +
  theme_bw()


ggplot(res) +
  geom_point(aes(x=log2FoldChange, y=-log10(padj), colour=significance)) +
  scale_color_manual(values = c("Significant" = "red", "Non-significant" = "blue"))+      
  ggtitle("Mov10 overexpression") +
  xlab("log2 fold change") + 
  ylab("-log10 adjusted p-value") +
  #scale_y_continuous(limits = c(0,50)) +
  theme(legend.position = "none",
        plot.title = element_text(size = rel(1.5), hjust = 0.5),
        axis.title = element_text(size = rel(1.25)))  +
  theme_bw()



Use the data generated from Weekly Assignment 8 to construct the following plots.

A volcano plot showing differentially expressed genes - color the Control points blue and the Mutant points Red.
A box plot of the expression of the gene with the highest positive fold change
A box plot of the expression of the gene with the highest negative fold change
An MA. MA plots are log10 of the mean expression (baseMean) of a gene on the x-axis and log2FoldChange on the y-axis.
