---
{"dg-publish":true,"permalink":"/computational-analysis-of-tibetan-legal-texts/"}
---

# Computational Analysis of Tibetan Legal Texts
## 1. Introduction
This document outlines the use of Python and NLP techniques used to analyze a small  Tibetan text corpus of the *zhal lce bcu drug*. One early edition of the *zhal lce bcu gsum* corpus was also included to explore textual variation. 
Various computational methods, including [[Computational Analysis of Tibetan Legal Texts#4.1. Word Mover’s Distance (WMD)\|Word Mover’s Distance]], [[Computational Analysis of Tibetan Legal Texts#4.3. Syntactic Distance (POS-Level)\|Syntactic Distance (POS-Level)]], [[Computational Analysis of Tibetan Legal Texts#4.2. Longest Common Subsequence (LCS)\|Longest Common Subsequence (LCS)]], and [[Computational Analysis of Tibetan Legal Texts#4.4. Weighted Jaccard Similarity\|Weighted Jaccard Similarity]], were applied to measure textual similarity and structural differences.


## 2. Text Preparation and Preprocessing

1. **Transcription and Proofreading:** The texts were transcribed using [Transkribus](https://readcoop.eu/transkribus/) and manually proofread to ensure accuracy.
2. **Normalization:** Punctuation was standardized, and abbreviations were expanded for consistency.
3. **POS Tagging with ACTib:** Using [ACTib](https://github.com/lothelanor/actib), Tibetan-specific POS tagging was applied to analyze structural variation. POS (Part-of-Speech) tagging assigns labels to words based on their grammatical function (e.g., noun, verb), helping in structural comparisons across texts. 
   ACTib provides detailed linguistic annotations, including morphological and syntactic features, forming the basis for syntactic distance, LCS, and weighted Jaccard similarity calculations.
4. **Word Embeddings with MiLMo:** The Word2Vec model from [MiLMo](https://huggingface.co/CMLI-NLP/MiLMo) was used for WMD analysis. 
   Word embeddings means the mapping of words or syllables into a numerical space where distances reflect semantic similarity. This technique allows comparison based on meaning rather than just structural alignment, offering insights beyond syntax and vocabulary overlap.
5. **Data Processing:** The POS-tagged output formed the basis for constructing heat maps to compare different texts at lexical, syntactic, and semantic levels.


## 3. Text Corpus
- [[Witnesses/Bailey 16\|Bailey 16]]: As a working hypothesis, we consider this manuscript to be the earliest legal code of the Ganden Phodrang administration, composed in its first year (1642).
- [[Witnesses/Bhutan 16\|Bhutan 16]], [[Witnesses/Dolanji 16\|Dolanji 16]], and [[Witnesses/Leiden 16\|Leiden 16]]  all reflect regional variations in the textual transmission of a presumably earlier version, likely composed under the auspices of the Tsang king [[Historical figures/Karma Tenkyong Wangpo\|Karma Tenkyong Wangpo]].
- <u>Japan13</u>: This manuscript of the *zhal lce bcu gsum* (detailed in the [Toyo Bunko repository](https://toyo-bunko.repo.nii.ac.jp/records/7448)<u></u>), likely written in 1643, has been included to shed light on the textual evolution of the *zhal lce* genre. 

> [!info]
> To maintain alignment, the three missing chapters in <u>Japan13</u> (1, 2, and 16) were added as empty placeholders, causing systematic outliers in the heat maps. 
- **Future Additions:** The [[Witnesses/Bell 16\|Bell 16]] and [[Witnesses/LTWA 02 16\|LTWA 02 16]] editions are slated for future inclusion in the corpus upon completion of their transcription. 



## 4. Comparison of Similarity Metrics


### 4.1. Word Mover’s Distance (WMD)
- **What it measures:** WMD calculates the effort needed to transform one text into another using word embeddings, capturing semantic similarity. 
  The [MiLMo repository](https://huggingface.co/CMLI-NLP/MiLMo)  offers two vector files, one trained on the word-level (藏文-词级别) and another on the syllable-level (藏文-音节). 
  After experimenting with both, I realized that the **Word-level WMD** suffered from segmentation inconsistencies whereas the **Syllable-level WMD** provided more stable results, aligning better with the other similarity metrics. This is likely due to the fact that it **captures sub-word patterns** relevant for morphological variation, and **works better across manuscript traditions** by smoothing out editorial inconsistencies.
  
- Overall, it **provides a complementary perspective** to the POS-based similarity metrics, capturing semantic relationships beyond structural overlap.

![Word Mover's Distance Heatmap](/img/user/assets/heatmap_wmd.png)

##### Interpretation:
  - **The Bhutan, Dolanji, and Leiden versions exhibit consistently low WMD values when compared to each other**, indicating a **high degree of semantic similarity** across these versions. This suggests that, despite minor lexical variations, their overall meaning and word usage remain closely aligned.
  - Bailey 16 consistently shows slightly higher WMD values when compared to the Bhutan and Dolanji versions, indicating some lexical or semantic drift in the manuscript tradition.
  - The **highest WMD values appear in chapters 6, 9, and 12 across multiple comparisons**, suggesting that it varies significantly in wording across the versions.


### 4.2. Longest Common Subsequence (LCS)
- **What it measures:** LCS identifies the longest shared sequence of POS-tagged words, indicating textual continuity.
- High LCS values correlated with lower WMD distances.

![Longest Common Subsequence Heatmap](/img/user/assets/heatmap_lcs.png)

##### Interpretation:
  - **Bhutan vs. Dolanji and Dolanji vs. Leiden show particularly high LCS values, confirming strong textual alignment** and suggesting that these versions preserve long, uninterrupted stretches of text with minimal alterations.
- **Bailey 16 shows notably lower LCS values in certain later chapters when compared with other versions**, implying structural or editorial divergence. However, this is not uniformly true for all later chapters, suggesting selective modifications rather than a continuous trend of increasing divergence over time.
- **Chapters 8, 10, and 12 exhibit particularly high LCS values**, indicating that these sections remained stable across all versions. This suggests they may have been copied with fewer changes, potentially reflecting core material that was transmitted with greater fidelity.


### 4.3. Syntactic Distance (POS-Level)
- **What it measures:** This metric calculates how different the grammatical structure of two texts is by comparing their POS sequences.
- Variations in function words and grammatical structures influenced distance calculations.

![Syntactic Distance Heatmap](/img/user/assets/heatmap_syntactic_distance.png)

##### Interpretation:
  - **Chapters 3, 4, and 6 display relatively low syntactic distances**, indicating that sentence structures in these sections have remained more consistent across versions. This suggests fewer structural alterations, whether due to shared editorial lineage or limited rewording.
  - Conversely, **Chapters 8, 9, and 12 show the highest syntactic distances**, suggesting that these sections underwent the most substantial rewording or restructuring.
  - **Bailey 16 appears to diverge more from Bhutan and Dolanji in several chapters**, reinforcing the idea that it represents a syntactically distinct variant. Whether this reflects an older form or editorial independence requires further investigation.


### 4.4. Weighted Jaccard Similarity
- **What it measures:** Weighted Jaccard similarity examines how much vocabulary is shared between two texts, with POS categories influencing the weight.  I therefore created a weight system to account for the importance of specific word categories over others.

![Weighted Jaccard Similarity Heatmap](/img/user/assets/heatmap_weighted_jaccard.png)

##### Interpretation:
  - Weighted Jaccard similarity aligns well with the LCS findings, showing **high lexical overlap in chapters 8-10**.
  - However, **chapter 6 has a noticeably lower Jaccard similarity than its corresponding LCS value**, suggesting that while the structure is preserved, there are enough small substitutions or variations in vocabulary to decrease overall lexical similarity.
  - The Bhutan and Dolanji versions tend to have the **highest Jaccard similarity scores**, further supporting their close textual relationship.


## 5. Final Data Processing Pipeline

```mermaid
flowchart TD

A["Transkribus Transcription"] --> B["Proofreading & Normalization"]

B --> C["POS Tagging with ACTib"]

C --> D["Text Processing & Structuring"]

D -->|Lexical Analysis| E["Weighted Jaccard Similarity"]

D -->|Syntactic Analysis| F["Syntactic Distance (POS-Level)"]

D -->|Sequence Comparison| G["Longest Common Subsequence (LCS)"]

D -->|Semantic Distance| H["Word Mover's Distance (WMD)"]

H -->|Syllable-Level| J["Word2Vec Model (MiLMo)"]
```
---
##### Secondary reading:

Deng, J., Shi, H., Yu, X., Bao, W., Sun, Y., & Zhao, X. (2023). "MiLMo: Minority Multilingual Pre-Trained Language Model," *2023 IEEE International Conference on Systems, Man, and Cybernetics (SMC)*, Honolulu, Oahu, HI, USA, 329–334. [https://doi.org/10.1109/SMC53992.2023.10393961](https://doi.org/10.1109/SMC53992.2023.10393961)

Griffiths, R. (2024). “Handwritten Text Recognition (HTR) for Tibetan Manuscripts in Cursive Script”. *Revue d’Etudes Tibétaines*, *72*, 43–51. [https://doi.org/10.1553/TibSchol_ERC_HTR](https://doi.org/10.1553/TibSchol_ERC_HTR)

Li, Y., Li, X., Wang, Y., Lv, H., Li, F., & Duo, L. (2022). Character-based Joint Word Segmentation and Part-of-Speech Tagging for Tibetan Based on Deep Learning. *ACM Transactions on Asian and Low-Resource Language Information Processing*, *21*(5). [https://doi.org/10.1145/3511600](https://doi.org/10.1145/3511600)

Meelen, M., Roux, É., & Hill, N. (2021). Optimisation of the Largest Annotated Tibetan Corpus Combining Rule-based, Memory-based, and Deep-learning Methods. _ACM Transactions on Asian and Low-Resource Language Information Processing_, _20_(1), 1–11. [https://doi.org/10.1145/3409488](https://doi.org/10.1145/3409488)

Wang, J., & Dong, Y. (2020). Measurement of Text Similarity: A Survey. _Information (Basel)_, _11_(9), 421. [https://doi.org/10.3390/info11090421](https://doi.org/10.3390/info11090421)