# snRNA-seq-workflow

This is the R code used to process and analyze single-nuclei (sn)RNA-seq data (10X Genomics) from 24 human post-mortem brain tissue samples derived from temporal cortex. In this pipeline, an annotated reference dataset from [human motor cortex (M1)](https://www.biorxiv.org/content/10.1101/2020.03.31.016972v2.full) is used to identify cell types in our query dataset using a label transfer method. The following steps were performed:

1. Process the M1 reference dataset 
2. Generate 24 Seurat objects and perform QC filtering
3. Merge the 24 objects and remove mitochondrial genes
4. Perform SCT normalization and integrate the datasets
5. Use the processed M1 reference to annotate cell types
6. Filter out nuclei with poor annotation scores
7. Perform dimensional reduction (PCA & UMAP)
8. Manually annotate clusters by majority cell type
9. Conduct differential expression analyses

The method used to identify 'hybrid' nuclei in step 6 is taken from [Grubman et al, 2019](https://www.nature.com/articles/s41593-019-0539-4). Nuclei were filtered out if the difference between the first and second highest cell type scores were within 65% of the highest cell type score.

For differential expression analyses in step 9, we used MAST directly with a random effect for sample as in [Zimmerman et al., 2021](https://www.nature.com/articles/s41467-021-21038-1). This is done for 1 example cluster of microglia.

Mitochondrial (MT) gene expression in snRNA-seq data was treated as background signal. Thus, after using % MT as a tool to filter out nuclei with high background, these genes were removed.

Upon merging the objects, a strange error occured in which the sample ID for one of the samples replaced another in the metadata. This is fixed in step 6.

