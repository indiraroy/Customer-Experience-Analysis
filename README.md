# CFPB Customer Experience Analysis Using NLP & Statistical Association

## Overview

Customer complaints contain detailed information about where customers experience friction, but the information is often unstructured and difficult to analyze at scale.

This project analyzes consumer complaints related to credit cards using Natural Language Processing (NLP) and statistical association analysis to:

- Identify recurring customer-experience themes
- Classify complaints into interpretable CX themes
- Examine how CX themes relate to specific CFPB complaint issues
- Identify statistically overrepresented complaint combinations
- Translate the findings into business priorities and recommendations

The analysis combines unsupervised NLP with statistical inference to move from unstructured customer narratives to actionable customer-experience insights.

---

## Business Problem

Complaint volume alone does not necessarily indicate where a business should intervene.

A complaint category may have a large number of cases but weak association with a particular customer-experience problem. Conversely, a relatively smaller category may reveal a disproportionately strong relationship with a specific issue.

Therefore, this analysis evaluates both:

1. **Complaint volume**
2. **Strength of association between CX themes and CFPB complaint issues**

This allows customer-experience problems to be prioritized based on both scale and statistical concentration.

---

## Dataset

The analysis uses CFPB consumer complaint data relating to credit-card complaints.

The dataset contains structured complaint information along with unstructured consumer narratives.

Key fields used in the analysis include:

- Issue
- Sub-issue
- Consumer complaint narrative
- Company
- State
- ZIP code
- Product information

The raw dataset is not included in this repository.

---

## Methodology

### 1. Text Cleaning

Consumer complaint narratives were cleaned using text preprocessing techniques including:

- Lowercasing
- Removal of CFPB anonymization placeholders
- Removal of non-alphabetic characters
- Whitespace normalization

### 2. TF-IDF Representation

Consumer narratives were transformed into numerical representations using TF-IDF.

The vectorization used:

- Unigrams and bigrams
- Minimum document frequency filtering
- Maximum document frequency filtering
- A capped feature space

This created a sparse representation of the complaint narratives suitable for topic modeling.

### 3. NMF Topic Modeling

Non-Negative Matrix Factorization (NMF) was applied to identify recurring patterns in complaint narratives.

Multiple topic configurations were evaluated using reconstruction error and topic diversity.

A six-topic solution was selected for the final analysis.

The six resulting customer-experience themes were:

1. Merchant Disputes & Refunds
2. Payment & Late-Fee Issues
3. Credit Reporting & Inaccurate Information
4. Identity Theft & Fraudulent Accounts
5. Fraud & Unauthorized Transactions
6. Balance Transfers & Promotional Offers

### 4. Complaint Classification

Each complaint was assigned to its dominant NMF topic based on its topic-weight distribution.

Only observations with valid NMF representations were retained for the final analysis.

This resulted in:

**84,999 valid complaints**

across:

- **6 CX themes**
- **15 CFPB complaint issues**

### 5. CX × CFPB Association Analysis

A contingency table was constructed between:

- Customer-experience theme
- CFPB complaint issue

A chi-square test of independence was then performed to determine whether the two categorical variables were statistically associated.

Effect size was measured using Cramér's V.

Standardized Pearson residuals were used to identify individual CX × CFPB combinations that occurred substantially more frequently than expected under independence.

---

## Key Findings

### Customer Experience Theme Distribution

The largest customer-experience theme was:

**Balance Transfers & Promotional Offers — 34.9%**

Other major themes included:

| CX Theme | Share |
|---|---:|
| Balance Transfers & Promotional Offers | 34.9% |
| Merchant Disputes & Refunds | 15.1% |
| Payment & Late-Fee Issues | 14.3% |
| Credit Reporting & Inaccurate Information | 13.5% |
| Fraud & Unauthorized Transactions | 11.3% |
| Identity Theft & Fraudulent Accounts | 10.8% |

---

## Statistical Results

The relationship between CX themes and CFPB complaint issues was statistically significant.

**Chi-square statistic:** 84,742.42

**Degrees of freedom:** 70

**p-value:** < 0.001

**Cramér's V:** 0.447

The results indicate a statistically significant and substantial association between customer-experience themes and CFPB complaint issues.

However, the chi-square test establishes the overall association; standardized Pearson residuals were used to identify which specific combinations contributed most strongly to that relationship.

---

## Strongest CX × CFPB Associations

The strongest positive associations were identified using standardized Pearson residuals.

| CX Theme | CFPB Issue | Observed Cases | Standardized Residual |
|---|---|---:|---:|
| Merchant Disputes & Refunds | Problem with a purchase shown on your statement | 11,468 | 121.46 |
| Identity Theft & Fraudulent Accounts | Getting a credit card | 4,879 | 118.51 |
| Fraud & Unauthorized Transactions | Problem with a purchase shown on your statement | 7,446 | 83.92 |
| Payment & Late-Fee Issues | Problem when making payments | 2,688 | 74.59 |
| Payment & Late-Fee Issues | Problem with a company's investigation into an existing problem | 1,584 | 54.12 |

These combinations occurred substantially more frequently than would be expected if CX theme and CFPB issue were independent.

---

## Business Priority Framework

To translate statistical results into business priorities, complaint volume was evaluated alongside association strength.

The resulting priority matrix separates complaint relationships into four areas:

- **High Priority:** High complaint volume + high association strength
- **High Association / Lower Volume:** Strong relationship but lower scale
- **High Volume / Lower Association:** Large complaint volume but weaker association
- **Lower Priority:** Lower volume + lower association strength

This helps distinguish between problems that are merely common and problems that are both common and disproportionately concentrated within a specific customer-experience theme.

---

## Business Implications

The analysis suggests several areas where customer-experience interventions could be prioritized.

### 1. Merchant disputes and refunds

The strongest observed association involved merchant disputes/refunds and problems with purchases appearing on customer statements.

**Recommendation:** Improve merchant-dispute and refund workflows, including clearer status visibility and resolution communication.

### 2. Identity theft and account opening

Identity theft/fraudulent-account complaints showed a very strong association with difficulties involving obtaining a credit card.

**Recommendation:** Strengthen identity verification, account-opening controls, and customer support pathways for suspected fraudulent accounts.

### 3. Fraud and unauthorized transactions

Fraud-related complaints were strongly associated with problems involving purchases appearing on statements.

**Recommendation:** Enhance transaction monitoring, unauthorized-transaction detection, and dispute-resolution workflows.

### 4. Payment and late-fee issues

Payment-related complaints showed strong associations with payment-processing problems and investigations into existing complaints.

**Recommendation:** Improve payment-status visibility, exception handling, and communication during payment investigations.

### 5. Balance transfers and promotional offers

Balance transfers and promotional offers represented the largest CX theme at 34.9% of classified complaints.

**Recommendation:** Review promotional-offer communication, eligibility explanations, fees, terms, and balance-transfer processes to reduce customer confusion.

---

## Key Takeaway

The analysis demonstrates how unstructured customer complaint narratives can be transformed into actionable customer-experience insights.

Rather than relying solely on complaint volume, the project combines:

**NLP → Topic Modeling → Complaint Classification → Statistical Testing → Association Analysis → Business Prioritization**

This provides a framework for identifying not only what customers complain about most, but also which specific customer-experience problems are disproportionately associated with particular complaint issues.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- TF-IDF
- Non-Negative Matrix Factorization (NMF)
- SciPy
- Matplotlib
- NLP / Text Mining
- Statistical Analysis
- GitHub

---

## Project Structure

```text
cfpb-customer-experience-nlp/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   └── CFPB_Customer_Experience_Analysis.ipynb
│
├── outputs/
│   ├── customer_experience_themes.png
│   ├── top_cx_cfpb_associations.png
│   ├── business_priority_matrix.png
│   └── executive_summary.png
│
└── data/
    └── README.md
## Reproducibility

The analysis can be reproduced using the notebook and the documented dataset setup.

### 1. Clone the repository

```bash
git clone https://github.com/indiraroy/Customer-Experience-Analysis.git
cd Customer-Experience-Analysis
