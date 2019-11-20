mycounts <- read.csv("BL5300-DEG/WA_counts.csv")                          --- input my countable with counts and gene id, use mycounts package to manipulate my data
metadata <- read.csv("BL5300-DEG/WA8_Metadata.csv")                       --- input my samples and its treatment (which samples, which treatment: control, mutant,treated..), use metadata package to manipulate my data
mycounts <- as.data.frame(mycounts)                                       --- change mycounts's  property to data.frame, a data format for us to use DESeq (To use DESeqDataSetFromMatrix, the user should provide the counts matrix, the information about the samples (the columns of the count matrix) as a DataFrame or data.frame)
metadata <- as.data.frame(metadata)                                       --- change metadata's property to data.frame, a data format for us to use DESeq
names(mycounts)[-1]
metadata$ï..id
all(names(mycounts)[-1]==metadata$ï..id)                                  --- to test if samples match in mycounts and metadata
dds.data <- DESeqDataSetFromMatrix(countData=mycounts,                    ---colData is a table that contains the information on each sample needed to decide which sample has which condition
                                   colData=metadata, 
                                   design=~dex, 
                                   tidy=TRUE)                             --- make sure the format is correct
dds.data
dds <- DESeq(dds.data)                                                    --- output dds.data to dds
res <- results(dds, contrast=c("dex","Control","Mutant"), tidy=TRUE)
res <- tbl_df(res)
res
res2 <- arrange(res,padj)
res3 <- filter(res2,padj<=0.05 & log2FoldChange>=2)
res4 <- filter(res2,padj<=0.05 & log2FoldChange<=-2)

ggplot
res=mutate(res,significance=ifelse(padj<0.05,"Significant","Non-significant"))  --- add a column indicating significance
ggplot(res) +
  geom_point(aes(x=log2FoldChange, y=-log10(padj), colour=significance)) +
  scale_color_manual(values = c("Significant" = "red", "Non-Significant" = "blue"))+      ---- change color manually
  ggtitle("Mov10 overexpression") +
  xlab("log2 fold change") + 
  ylab("-log10 adjusted p-value") +
  #scale_y_continuous(limits = c(0,50)) +
  theme(legend.position = "none",
        plot.title = element_text(size = rel(1.5), hjust = 0.5),
        axis.title = element_text(size = rel(1.25)))  +
  theme_bw()

-------------------------------------------------------------------------------------------------------------------------
Use the data generated from Weekly Assignment 8 to construct the following plots.

A volcano plot showing differentially expressed genes - color the Control points blue and the Mutant points Red.
A box plot of the expression of the gene with the highest positive fold change
A box plot of the expression of the gene with the highest negative fold change
An MA. MA plots are log10 of the mean expression (baseMean) of a gene on the x-axis and log2FoldChange on the y-axis.
Copy your plots to a word document and upload the word document along with a link to the github page with your code.
