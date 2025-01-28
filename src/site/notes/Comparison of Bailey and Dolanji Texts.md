---
{"dg-publish":true,"permalink":"/comparison-of-bailey-and-dolanji-texts/"}
---

## 1. Unique & Frequent Words Per Text  
### 1.1. Bailey Text 
| Word  | Meaning               | Frequency |
| ----- | --------------------- | --------- |
| དགག་  | negation, prohibition | 12        |
| དབང་  | authority, power      | 9         |
| གཟུང་ | to hold, grasp, seize | 8         |
| བཙོས་ | edited, corrected     | 7         |
| དོན་  | purpose, meaning      | 6         |
**Interpretation:**  
- ***Strong legal focus*** with terms like ***prohibition, authority, and correction**.  
- Suggests **a structured legal framework** with clear **rules and enforcement mechanisms**.  
- Possible **editorial oversight** (e.g., ****”edited, corrected”**** might indicate revisions).  
   
  
### 1.2. Dolanji Text

| Word    | Meaning                     | Frequency |
| ------- | --------------------------- | --------- |
| བཟུངས་  | to grasp, to accept         | 13        |
| བསྡུས་  | summary, collected          | 10        |
| བསྒྲུབ་ | to accomplish, to establish | 9         |
| མཇལ་    | meeting, audience           | 8         |
| བཟང་    | excellent, proper           | 7         |
**Interpretation:**
- **Less about enforcement**, more about **procedure and summary**.  
- Suggests *a tradition that focuses on documentation and records* rather than rigid legal restrictions.  
- More references to **meetings and interactions**, suggesting **a diplomatic or consensus-based legal approach**.  
   
  
## 2. Summary of Key Differences

| **Feature**                 | **Bailey Text**                | **Dolanji Text**                 |
| --------------------------- | ------------------------------ | -------------------------------- |
| Legal vs. Procedural        | Highly legalistic, rules-based | More procedural, records-based   |
| Enforcement vs. Consensus   | Strong legal enforcement       | More about meetings & agreements |
| Philosophy vs. Practicality | Practical, authoritative       | More bureaucratic, diplomatic    |
| Textual Approach            | Editing & correction noted     | Summaries and agreements         |

  
## 3. What This Suggests
- The *Bailey text* appears to be **a legal-philosophical discussion** with a focus on **rules, prohibitions, and textual integrity**.  
- The *Dolanji text* leans towards **economic, procedural, and diplomatic discussions*, with more **references to decisions, commerce, and formal processes**.  
- The differences suggest **regional or editorial variation**—perhaps *Bailey* represents a **stricter legal tradition**, while *Dolanji* reflects **real-world applications**.

## 4. Heatmap visualizations

### 4.1. Gaps (Unmatched Words) 
- Measures word-level differences between text pairs.  
- Certain chapters (e.g., chapter 9) have extremely high values, meaning some texts have significant missing content compared to others.  
→ *Useful for identifying missing or restructured content.*  
  
![heatmap_gaps.png](/img/user/assets/heatmap_gaps.png)

### 4.2. Jaccard Similarity
- Captures vocabulary overlap percentage.  
- Values are moderate, showing some differentiation, but still doesn't fully explain text differences.  
→ *Jaccard works best when used alongside Levenshtein distance.*  
 
![heatmap_jaccard.png](/img/user/assets/heatmap_jaccard.png)
 
### 4.3. Word-Level Levenshtein Distance
* Measures word-level differences (number of edits needed to transform one text into another).  
* High values in some chapters indicate significant textual modifications.  
→ *Useful for detecting partial rewrites rather than full content replacements.*  
→ *Possibly the best metric for detecting major textual revisions.*  
  ![heatmap_word_level_levenshtein.png](/img/user/assets/heatmap_word_level_levenshtein.png)
### 4.4. Shared Content
* Measures how much of one text is contained within the other.  
* Good differentiation across chapters, indicating some texts are much closer than others.  
→ *Helpful for identifying textual inheritance (e.g., Toyo Bunko’s 13 chapters originating from a 16-chapter version).*
![heatmap_shared_content.png](/img/user/assets/heatmap_shared_content.png)
