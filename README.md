# RNA-Seq-analysis

This script is used to perform differential gene expression analysis using the DESeq2 package in R. It compares gene expression across three groups: Control, Condition1, and Condition2. The input file is called RawCountFile_rsemgenes.txt and contains raw RNA-seq gene counts. The first column has gene names and the other columns contain count values for samples.
First, the script removes genes with zero counts in all samples using an awk command. The filtered data is saved in a new file called filtered_counts.txt. Then, this file is loaded into R as a data table. The script defines which columns belong to each condition: Control (columns 2 to 4), Condition1 (columns 5 to 7), and Condition2 (columns 8 to 10). The count values are rounded to make sure they are integers.
Next, the script creates a DESeqDataSet object, which includes the count data and condition information for each sample. It then runs the DESeq function to perform the differential expression analysis. The script compares three pairs of conditions: Condition1 vs Control, Condition2 vs Control, and Condition1 vs Condition2.
For each comparison, it selects differentially expressed genes (DEGs) based on two criteria: adjusted p-value (padj) < 0.05 and absolute log2 fold change > 1. These genes are considered significant. It also removes any rows with missing values or extreme values (log2 fold change greater than 20).
Custom colors are defined to label DEGs as red and non-DEGs as black. The script saves the DEGs from the Condition1 vs Control comparison to a CSV file named DEGs_condition1_vs_control.csv.
Finally, the script creates a volcano plot using the ggplot2 package. This plot shows log2 fold change on the x-axis and negative log10 of the adjusted p-value on the y-axis. Red points show DEGs and black points show non-significant genes. The plot has a white background.
This analysis assumes that there are three replicate samples in each condition. Users should update the column numbers if their sample layout is different. The script provides a 
basic and useful pipeline for analyzing RNA-seq count data using DESeq2 in R.

 # PCA-Plot



This script performs Principal Component Analysis (PCA) on RNA sequencing gene expression data using the ggplot2 package in R. It compares samples from three groups: Control, Condition1, and Condition2.
The input file is named Filtered_counts.txt. It is a tab-separated text file. The first column contains gene names. Columns 2 to 4 contain expression values for Control samples, columns 5 to 7 for Condition1, and columns 8 to 10 for Condition2.
Steps performed by the script:
Load the ggplot2 package in R.
Read the data from the Filtered_counts.txt file.
Extract the gene name in the first column.
Extract expression values for Control, Condition1, and Condition2 samples.
Print the original column names for each group to check their structure.
Rename all column headers in each group to EV1, EV2, and EV3 for consistency.
Print the updated column names to confirm the change.
Combine all the expression data from the three groups into a single matrix by stacking them row-wise.
Perform PCA on the combined expression matrix using the prcomp function without scaling the values.
Keep only the first two principal components and store them in a new data frame.
Create group labels for each row in the combined data to indicate whether it came from Control, Condition1, or Condition2.
Add these labels as a new column in the PCA result data frame.
Use ggplot2 to create a PCA scatter plot using PC1 and PC2 as the axes and color the points by group.
Add axis labels and title of the plot.
Save the PCA plot as a PNG image named PCA_plot_filtered.png.
This PCA plot helps visualize the similarities and differences between samples from different conditions based on their gene expression patterns. Make sure the input file has numeric expression values and no missing data in the selected columns.
