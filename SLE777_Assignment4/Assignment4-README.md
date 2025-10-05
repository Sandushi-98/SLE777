SLE777 – Assessment 4 (Applied Bioinformatics)

This repository contains code and data to analyse:

Part 1: Gene expression and tree growth.
Part 2: Sequence diversity in Escherichia coli vs Campylobacter coli.

##Part 1

Purpose:
Analyzes the provided growth_data.csv and gene_expression.tsv datasets to explore site-based differences in tree circumference and gene expression.

Inputs:
growth_data.csv – tree circumference data for control and treatment sites.
gene_expression.tsv – gene expression dataset (Question 1–5).

Outputs:
Calculated means, standard deviations, and t-test results.
Boxplots and histograms illustrating growth differences.
Numerical summaries for control vs treatment sites.

##Part 2

Sequence Analysis: E. coli vs Campylobacter coli

Purpose:
The objective of this section is to analyse the biological sequence diversity between Escherichia coli and Campylobacter coli through their complete coding DNA sequences (CDS).  This analysis illustrates the differences in base composition, codon bias, and amino acid usage patterns between the two organisms.

The primary objective is to determine the impact of genomic nucleotide composition (GC versus AT bias) on amino acid and peptide (k-mer) composition within the proteomes of the two bacterial species.

#Step 1: Import CDS FASTA files

Two FASTA files were downloaded from NCBI:
ecoli_cds.fa – CDS for Escherichia coli K12 strain.
campy_cds.fa – CDS for Campylobacter coli (GCA_003780985.1).

The data were imported into R using seqinr::read.fasta(). Each sequence entry represents a single protein-coding gene.

Outputs:
Number of CDS entries per organism (length()).
Total nucleotide counts (sum(sapply(..., length))).

This determines the size of each organism's proteome and total coding DNA.


#Step 2: Translate CDS to Protein Sequences

Each DNA sequence is translated into amino acids using seqinr::translate(), which adheres to the standard genetic code.

Inputs: ecoli_cds.fa, campy_cds.fa
Outputs: amino acid and nucleotide frequency plots, codon usage, and k-mer comparison charts.

The obtained protein lists are converted into character vectors for further processing.  Stop codons (*) are eliminated before performing amino acid or k-mer calculations.

Purpose: To acquire the entire proteome of both organisms and prepare it for comparative frequency analysis.


#Step 3: Calculate Coding DNA and CDS Length Statistics

Lengths of all coding sequences are computed and summarized.
The mean, median, and range of CDS lengths are computed for each organism.
A boxplot of CDS length distribution compares the overall genome organisation to gene size variance.

Interpretation: E. coli has a wider dispersion and slightly longer CDS on average, but C. coli has shorter and more consistent gene lengths, reflecting its smaller and AT-rich genome.


#Step 4: Compute and Compare Nucleotide Frequencies

All nucleotide bases across coding regions are merged and counted using seqinr::count().

Frequencies are normalised to proportions.
The barplots indicate the differences in A/T vs G/C composition.

Interpretation: E. coli has a balanced nucleotide makeup, with around 50% GC.
C. coli has a high A/T content, indicating an AT-rich genome, which influences codon bias and amino acid distribution in proteins.


#Step 5: Amino Acid Composition

Protein sequences are converted into amino acid vectors, and seqinr::count() is used again to calculate frequencies for the 20 standard amino acids.

Visualization: Two barplots compare amino acid frequencies for E. coli and C. coli.

Interpretation: E. coli uses amino acids in a reasonably regular manner, with Leucine (L), Valine (V), and Glycine (G) being the most common.
C. coli has a skewed profile, with a larger proportion of Isoleucine (I), Lysine (K), and Asparagine (N) – amino acids encoded by AT-rich codons.

This reveals the direct effect of genome makeup on proteome structure.


#Step 6: Protein k-mer Analysis (3–5 amino acids)

Codon usage is quantified using seqinr::uco() to obtain Relative Synonymous Codon Usage (RSCU) values.

Purpose:
To identify the ten most over- and under-represented protein k-mers, ranging from 3 to 5 amino acids in length, in Campylobacter coli and to compare their prevalence in Escherichia coli.

Protein sequences were flattened and stop codons removed. Using seqinr::count(), k-mer frequencies (k = 3, 4, 5) were calculated. The top and bottom 10 motifs in C. coli were extracted and compared with their frequencies in E. coli. Barplots were created for visual comparison.

C. coli exhibits a significant bias in k-mer composition.
Motifs that are over-represented include those abundant in Lysine (K), Leucine (L), and Glutamic acid (E), such as KEL, LKE, and KEELK.
Motifs that are under-represented include GC-rich amino acids such as Alanine (A), Glycine (G), and Proline (P).

In E. coli, similar motifs are present, albeit with minor variations, indicating a more balanced k-mer distribution.

The elevated k-mer bias in C. coli is indicative of its AT-rich genome and pronounced codon usage bias, which preferentially supports AT-encoded residues (K, I, N).
The balanced GC/AT ratio in E. coli leads to uniform frequencies of amino acids and motifs.
The genomic and evolutionary differences elucidate the enrichment or depletion of specific peptide motifs in C. coli relative to E. coli.

##Overall summary

The AT-rich genome of Campylobacter coli induces a distinct codon usage bias favouring AT-heavy codons, leading to an over-representation of amino acids including Isoleucine, Lysine, and Asparagine.

Escherichia coli exhibits a balanced GC/AT ratio, resulting in a more uniform amino acid distribution and reduced k-mer bias.

Variations in sequence composition indicate genomic adaptation, tRNA availability, and the evolutionary pressures linked to the ecological niche of each organism.