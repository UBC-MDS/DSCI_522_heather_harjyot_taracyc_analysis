Project Report
================
Harjyot Kaur and Heather Van Tassel
November 23, 2018

Summary Report
==============

Taracyc Ocean Virus Analysis
============================

Introduction
============

The ocean is full of mysteries, and plays an important role in oxygen production, weather patterns, climate, carbon sequestration and global ecosystem health. Bacteria help sequester carbon in the ocean and it is estimated that 93% of the earth's carbon dioxide is stored in algae, vegetation, and coral under the sea and cycled through the oceans. There are viruses present can infect bacteria and alter their chance of survival. For example, viruses have been found to use their own viral DNA to turn the photosynthesis system back on in a dying bacterial cell, to promote cell survival.<sup>1</sup>

### Motivation for research

To further explore the populations of bacteria and viruses in the oceans, project was led by the TARA oceans <sup>1</sup> collected 300 water samples from all over the world's oceans at various depths. These samples were filtered for viral and bacterial DNA. By understanding these populations and how they might interact, we can gain insight into carbon sequestration patterns and how these viruses are impacting the bacteria. The Hallam lab at UBC created an algorithm to classify these bacterial and viral DNA sequences into categories and specific biological pathways that these sequences may be involved in. We would like to use this data to explore how viral DNA differs across biological pathways and depths to start exploring which areas and pathways are most represented by these creatures.

Research Question
=================

Does the mean abundance of viral DNA sequences differ across biological pathways? Does the mean abundance of viral DNA sequences differ across ocean depth levels? Does the mean abundance of viral DNA sequences of the biological pathways differ across ocean depth levels?

Data Set
========

We will be analyzing the metaviriome data collected from the [Tara Oceans Project](http://oganm.com/shiny/taracyc/). Downloading data from the R Shiny App is a nine-step manual process. Thus, a data repository [Data\_Taracyc\_Analysis](https://github.com/HarjyotKaur/Data_Taracyc_Analysis) has been created to store the raw master data. Since the data file is too large, we have used [Github Large File Storage](https://git-lfs.github.com/). For detailed information, of data download visit the [repository](https://github.com/HarjyotKaur/Data_Taracyc_Analysis).

Here are the variables we are using:

| Variable Name | Type        | Description                                               |
|---------------|-------------|-----------------------------------------------------------|
| RKPM          | Continuous  | Reads per kilobase of transcript per million mapped reads |
| LEVEL1        | Categorical | Biological Pathways                                       |
| Depth         | Categorical | Levels of ocean depth                                     |

The four depths that we explored are: - SRF: Surface Water Layer (5m) - DCM: Deep Chlorophyll Maximum (17-188m) - MIX: Marine Epipelagic Mixed Layer (2-140m) - MES: Mesopelagic (250-1000m)

The biological pathways we are analyzing are: - Biosynthesis: - Energy-Metabolism - Degradation - Detoxification - Metabolic-Clusters

More information on how interesting and complex these pathways are can be found on [KEGG](https://www.genome.jp/kegg/pathway/map/map01100.html)

### Table 1: Snapshot of data set

|    X|       RPKM| LEVEL1       | DEPTH |
|----:|----------:|:-------------|:------|
|    1|  0.4476350| Biosynthesis | DCM   |
|    2|  0.0974505| Degradation  | DCM   |
|    3|  0.0826759| Biosynthesis | DCM   |
|    4|  0.1531230| Degradation  | DCM   |
|    5|  0.0597218| Degradation  | DCM   |

Exploratory Data Analysis and Data Cleaning
===========================================

The data consists of 299 samples of ocean organism DNA sequences, to bifurcate samples containing viral and bacterial DNA. Definition for bifurcation available [here](https://github.com/hackseq/tara-cyc-hs18).

### Figure 1: Samples collected for Ocean DNA

<img src="../results/figures/fig1_eda_sample_split.png" alt="Figure 1: Samples collected for Ocean DNA" width="1800" />
<p class="caption">
Figure 1: Samples collected for Ocean DNA
</p>

<br> <br> Since the research question focuses on viral DNA, we filter out the samples containing only viral DNA sequences. This resulted in 90 samples out of 299, or 30% of the total data.

After, filtering the data we wanted to explore the viral DNA samples collected for various biological pathways across varied ocean depth. *To keep things simple, we are only looking at the higher level biological pathways stored as LEVEL1, but for those who are interested, the original dataset contains LEVEL2 and LEVEL3 variables that further classify the types of biological pathways these genes may be involved in.* <br> <br>

### Figure 2: Samples of Viral DNA Sequences Collected for five biological pathways across four levels of ocean depth

<img src="../results/figures/fig3_eda_biological_pathways_depth_dna_volume.png" alt="Figure 2: Samples of Viral DNA Sequences Collected for five biological pathways across four levels of ocean depth" width="2099" />
<p class="caption">
Figure 2: Samples of Viral DNA Sequences Collected for five biological pathways across four levels of ocean depth
</p>

<br> <br>

We observe that Viral DNa Sequences samples were collected from four different levels of ocean depth. Also, the samples are able to capture interaction of viral population in five pathways. Majority of samples collected are from Surface Water Layer, the sample capture maximum interaction of Viral DNA in Biosynthesis pathway.

One of the assumptions for a Two-Way ANOVA is homogenity of variances. We performed Levene's Test to validate the same, it evaluated the p-value &lt;0.05, thus failing the test. Since, we did not have proper tools to tackle the fallout of Levene Test, we decided to look for outliers in data. <br> <br>

### Figure 3: Spread of Abundance of Viral DNA Sequences (RKPM) and Outliers across Biological Pathways

<img src="../results/figures/fig4_eda_biological_pathways_spread_outliers.png" alt="Figure 1: Samples collected for Ocean DNA" width="2099" />
<p class="caption">
Figure 1: Samples collected for Ocean DNA
</p>

<br> <br>

### Figure 4: Spread of Abundance of Viral DNA Sequences (RKPM) and Outliers across levels of Ocean Depth

<img src="../results/figures/fig5_eda_depths_spread_outliers.png" alt="Figure 1: Samples collected for Ocean DNA" width="2099" />
<p class="caption">
Figure 1: Samples collected for Ocean DNA
</p>

<br> <br>

The black dots in Figure 3 and 4 represent outliers in data. RPKM (Reads Reads per kilobase million) values lying below the 1st percentile and lying above the 99th percentile were removed to ensure the assumption of homogenity of variances.

After cleaning the data set we observe the mean abundance of viral DNA sequences in groups created for the two factors under consideration, biological pathways and ocean depth. The data gets grouped into 20 categories. <br> <br>

### Figure 5: Mean Abundance of Viral DNA Sequences in 20 categories

<img src="../results/figures/fig6_eda_mean_dna_across_categories.png" alt="Figure 1: Samples collected for Ocean DNA" width="2099" />
<p class="caption">
Figure 1: Samples collected for Ocean DNA
</p>

<br> <br> The mean abundance of viral DNA sequences is highest for biological pathways that occur in surface water layer whereas the mean abundance of viral DNA sequences seems to be similar for Detoxification and Degradation across all depths. To further investigate the interaction between biological pathways and ocean depth levels in terms of mean abundance of viral DNA sequences we will perform a Two-Way ANOVA.

Analysis
========

Two-Way ANOVA has certain assumptions:

-   Dependent variable should be measured at the continuous level
-   Two independent variables should each consist of two or more categorical, independent groups.
-   Independence of observations
-   No significant outliers
-   All samples were drawn from normally distributed populations
-   Homogeneity of variances (among the groups should be approximately equal).

-   Factors: Biological Pathways & Ocean Depth

H<sub>0</sub>: There is no significant interaction between biological pathways and ocean depth levels in terms of mean abundance of viral DNA sequences
H<sub>A</sub>: There is a significant interaction between biological pathways and ocean depth levels in terms of mean abundance of viral DNA sequences

We will be checking the above three set of hypothesis at 5% Level of Significance.

Results
=======

### Table 1: Two-Way ANOVA, estimates and F-Statistic

|     X| term         |       sumsq|     df|   statistic|    p.value|
|-----:|:-------------|-----------:|------:|-----------:|----------:|
|     1| (Intercept)  |    52143749|      1|  319.864227|  0.0000000|
|     2| LEVEL1       |    14123966|      4|   21.660082|  0.0000000|
|     3| DEPTH        |     7272040|      3|   14.869570|  0.0000000|
|     4| LEVEL1:DEPTH |     2327845|     12|    1.189971|  0.2833311|
|     5| Residuals    |  2482280923|  15227|          NA|         NA|
|  <br>|              |            |       |            |           |
|  <br>|              |            |       |            |           |

Our ANOVA results are shown in the table below. *Note that LEVEL1 is the name of the factor for Biological Pathways.* All results have a p-value &lt; 0.05, and thus we reject our null hypothesis. There is significant difference in mean abundance of Viral DNA Sequence across biological pathways and levsl of ocean depths individually. Also, there is a significant interaction between biological pathways and ocean depth levels in terms of mean abundance of viral DNA sequences. Our findings can be visualized by the plot below. <br> <br>

### Figure 6: Confidence Intervals and Mean of Viral DNA Sequences at 5% Significance Level

<img src="../results/figures/fig7_results.png" alt="Figure 1: Samples collected for Ocean DNA" width="2100" />
<p class="caption">
Figure 1: Samples collected for Ocean DNA
</p>

<br> <br>

It seems that viral DNA that interact in Biological Pathways do not have overlapping condfidence intervals across all ocean depth layers. Viral DNA interacting in Degradation, Detoxification and Metabolic-Clusters have overlapping confidence intervals in Deep Chlorophyll Maximum ocean layer.

Discussion
----------

We can conclude that there is a difference in mean viral DNA accross all pathways and depths. However, when comparing interaction effects of each depth and pathway, there are a few groups that may not be significantly different, but it is hard to tell visually. With a Two-Way ANOVA, we are only able to determine whether one or more groups is significantly different than the others. Thus, even though we rejected our null hypothesis, we can not conclude which pathways are significantly different. However, to further investigate these differences, one could do a pairwise t.test or Tukey-Kramer analysis.

Conclusion
----------

This was a very interesting exploration of viral DNA that represents the world's ocean populations. In the future, we hope to analyze how the viral DNA might affect the abundance of bacterial DNA for each pathway. We hypothesize that the viral DNA will be correlated with the bacterial DNA, as it seems that they interact. <sup>2</sup> Additional factors could be explored, such as how the viral and DNA samples and pathways are distributed accross geographical locations. There is so much waiting to be discovered, and we are excited to see what future findings may uncover, and what implications these findings may have on how we manage and care for our oceans in the face of climate change.

References
----------

-   <sup>1</sup> Thompson et al., 2007. Phage auxiliary metabolic genes and the redirection of cyanobacterial host carbon metabolism [link](http://www.pnas.org/content/108/39/E757.short)

-   <sup>2</sup> [Tara Oceans Project website](https://oceans.taraexpeditions.org/en/m/about-tara/les-expeditions/tara-oceans/)