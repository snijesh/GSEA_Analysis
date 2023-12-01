# GSEA_Analysis

Gene Set Enrichment Analysis (GSEA) is a computational method used in genomics and bioinformatics to analyze and interpret gene expression data. The algorithmic background of GSEA involves several key steps:

1. **Ranking Genes by Expression Change:**
   - GSEA starts with a list of genes ranked by their expression changes between two experimental conditions (e.g., treatment vs. control).
   - The genes are ranked based on a metric like fold change, t-statistic, or other relevant statistical measures.

2. **Defining Gene Sets:**
   - Gene sets are predefined groups of genes sharing common biological functions, pathways, or other annotations.
   - These gene sets can be obtained from databases like Gene Ontology (GO), Kyoto Encyclopedia of Genes and Genomes (KEGG), or other curated collections.

3. **Running a Running Sum Statistic:**
   - GSEA calculates an enrichment score by walking down the ranked list of genes.
   - At each step, a running sum statistic is calculated. The sum increases when a gene in the gene set is encountered and decreases when a gene not in the set is encountered.

4. **Normalizing the Enrichment Score:**
   - The enrichment score is normalized to account for the gene set size. This helps in comparing scores across different gene sets.

5. **Estimating Significance through Permutation Testing:**
   - Statistical significance of the enrichment score is determined through permutation testing.
   - The gene labels are randomly permuted, and the enrichment score is recalculated for each permutation to create a null distribution.

6. **Calculating the False Discovery Rate (FDR):**
   - Multiple testing correction is applied to control the false discovery rate.
   - The observed enrichment score is compared to the null distribution to calculate the FDR, providing a measure of the likelihood that the observed enrichment is due to chance.

7. **Interpreting Results:**
   - Gene sets with significant enrichment are identified based on the FDR threshold.
   - The results help in understanding which biological pathways or functions are differentially regulated under the experimental conditions.

GSEA is a powerful tool for discovering underlying biological processes in large-scale genomic data and is widely used in functional genomics research.


The core of Gene Set Enrichment Analysis (GSEA) involves calculating an enrichment score to quantify the overrepresentation of genes from a gene set at the top or bottom of a ranked list of genes. The basic steps for calculating the enrichment score are as follows:

1. **Ranking Genes:**
   - Start with a ranked list of genes based on a metric such as fold change, t-statistic, or another relevant measure derived from a comparison between experimental conditions (e.g., treatment vs. control).

2. **Walking Down the Ranked List:**
   - For each gene in the ranked list, calculate a running sum statistic that increases when a gene in the gene set is encountered and decreases when a gene not in the set is encountered.

3. **Enrichment Score Calculation:**
   - The enrichment score is calculated as the maximum deviation from zero of the running sum statistic. The score represents the degree to which the genes in the gene set are overrepresented at the extremes (top or bottom) of the ranked list.

4. **Normalization:**
   - Normalize the enrichment score to account for differences in gene set sizes. This involves dividing the enrichment score by the maximum possible score, which is the sum of the absolute values of the running sum statistic. This normalization helps in comparing scores across different gene sets.

Mathematically, the enrichment score (ES) for a given gene set is calculated using the formula:

\[ ES = \max \left( \sum \text{running sum statistic}, 0 \right) \]

The running sum statistic is updated as genes are encountered in the ranked list. The enrichment score is then normalized to obtain a normalized enrichment score (NES):

\[ NES = \frac{ES}{\text{Normalization factor}} \]

The normalized enrichment score is used for assessing the statistical significance of the enrichment.

The idea is that a high positive or negative enrichment score indicates that the genes in the gene set are clustered towards the top or bottom of the ranked list, suggesting a potential biological relevance of the gene set under the experimental conditions. The significance of the enrichment score is typically assessed through permutation testing, comparing the observed score to scores obtained from randomly permuting gene labels.


Let's consider a simple example with a ranked list of 8 genes and a gene set containing 5 genes that are part of a pathway. The gene set is denoted by "A" and the pathway genes are indicated with asterisks:

Ranked list of genes: \[G_1, G_2, G_3, G_4, G_5, G_6, G_7, G_8\]

Gene set A: \[\ast G_1, \ast G_3, \ast G_5, \ast G_7, G_8\]

Now, let's walk down the ranked list and calculate the running sum statistic and enrichment score:

1. **Initial State:**
   - Running sum statistic = 0
   - Enrichment score (ES) = 0

2. **Encounter \(G_1\):**
   - \(G_1\) is in gene set A, so the running sum increases: \[ \text{Running sum} = 1 \]
   - Update the enrichment score: \[ ES = \max(1, 0) = 1 \]

3. **Encounter \(G_2\):**
   - \(G_2\) is not in gene set A, so the running sum decreases: \[ \text{Running sum} = 0 \]
   - \(ES\) remains 1

4. **Encounter \(G_3\):**
   - \(G_3\) is in gene set A, so the running sum increases: \[ \text{Running sum} = 1 + 1 = 2 \]
   - Update the enrichment score: \[ ES = \max(2, 0) = 2 \]

5. **Encounter \(G_4\):**
   - \(G_4\) is not in gene set A, so the running sum decreases: \[ \text{Running sum} = 2 - 1 = 1 \]
   - \(ES\) remains 2

6. **Encounter \(G_5\):**
   - \(G_5\) is in gene set A, so the running sum increases: \[ \text{Running sum} = 1 + 1 = 2 \]
   - Update the enrichment score: \[ ES = \max(2, 0) = 2 \]

7. **Encounter \(G_6\):**
   - \(G_6\) is not in gene set A, so the running sum decreases: \[ \text{Running sum} = 2 - 1 = 1 \]
   - \(ES\) remains 2

8. **Encounter \(G_7\):**
   - \(G_7\) is in gene set A, so the running sum increases: \[ \text{Running sum} = 1 + 1 = 2 \]
   - Update the enrichment score: \[ ES = \max(2, 0) = 2 \]

9. **Encounter \(G_8\):**
   - \(G_8\) is in gene set A, so the running sum increases: \[ \text{Running sum} = 2 + 1 = 3 \]
   - Update the enrichment score: \[ ES = \max(3, 0) = 3 \]

So, in this example, the final enrichment score (ES) is 3, indicating that the gene set A is enriched towards the top of the ranked list. The normalized enrichment score (NES) would be calculated by dividing \(ES\) by the normalization factor, but for this simplified example, we won't perform that step.
