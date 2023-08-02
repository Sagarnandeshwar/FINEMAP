# FINEMAP
Implemented fine mapping algorithm to identify the causal SNPs(Single nucleotide polymorphisms) using GWAS (Genome-wide association studies).

## FINEMAP 
FINEMAP is a statistical method used for fine-mapping complex trait loci and identifying causal variants in genome-wide association studies (GWAS). In GWAS, researchers often identify regions of the genome that are associated with a specific trait or disease. However, these regions can be quite large and may contain multiple genetic variants (single nucleotide polymorphisms, or SNPs) that are in linkage disequilibrium with each other. This means that the true causal variant may not be immediately apparent. 

Fine-mapping aims to narrow down the list of candidate causal variants in a specific region of the genome, making it easier to identify the most likely causal variant responsible for the observed association with the trait or disease. 

## Method 
The FINEMAP software implements a Bayesian probabilistic approach for fine-mapping. It considers the correlation structure between SNPs and calculates the posterior probability of each SNP being the causal variant, given the observed association data. The method takes into account information such as the strength of association of each SNP with the trait, the level of correlation between SNPs, and the prior probability of each SNP being causal (usually based on functional annotations or previous knowledge). 

By integrating this information, FINEMAP assigns probabilities to each SNP being the causal variant, and it outputs a list of the most probable causal variants in the region of interest. This information can help researchers prioritize follow-up experiments or functional studies to validate the candidate causal variants. 

It's important to note that fine-mapping is computationally intensive and may require significant computational resources. 

## Assumption  
We are assuming there are maximum 3 causal SNPs in the locus.  

## Implementation
1. Implement the efficient Bayes factor for each causal configurations:
   where $s_λ^2$ is user-defined prior variance in the unit of $σ^2$, $Δ_γ$ is the diagonal matrix with diagonal equal to γ (causal configuration). You may assume that $s_λ^2$ = 0.005. Therefore, assuming there are k causal SNPs, then $Σ_{CC}$ = $Ns^2I_k$ = 2.49I_k
2. Implement the prior calculation for each configurations
3. Implement posterior inference over all possible configurations assuming at maximum 3 causal SNPs. Therefore, no stochastic sampling is required here (as in the original FINEMAP).

4. Implement posterior inclusion probabilities (PIP) to calculate SNP-level posterior probabilities.
   Visualize the normalized inferred PIP aligned with GWAS marginal -log10 p-values. It looks like we missed one of the 3 causal SNPs due to its nearly perfect LD with the other causal SNPs. But in general, we are able to pull down quite a few non-causal ones. That is, if we were going to experimentally validate the top SNPs, 2 out of 6 top SNPs based on PIP are true causal ones, whereas we would have got a lot more false positives if we were to follow the -log10 P-values instead.

   
