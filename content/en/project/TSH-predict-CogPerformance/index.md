---
type: "project" # DON'T TOUCH THIS ! :)
Date: "2026-06-26" # Date you first upload your project.
# Title of your project (we like creative title)
title: "Can brain structure and Thyroid Stimulating Hormone levels predict cognitive performance? Prediction models and SHAP-based variable contribution analyses?"

# List the names of the collaborators within the [ ]. If alone, simple put your name within []
names: [Katrina Mae Tapang, Monika Folkierska-Żukowska, Xinni Wang]

# Your project GitHub repository URL
github_repo: https://github.com/brainhack-school2026/TSH-predict-CogPerformance

# If you are working on a project that has website, indicate the full url including "https://" below or leave it empty.
website:

# List +- 4 keywords that best describe your project within []. Note that the project summary also involves a number of key words. Those are listed on top of the [github repository](https://github.com/brainhack-school2023/JDaoust_project.git), click `manage topics`.
# Please only lowercase letters
tags: [cognition, thyroid, sex, sMRI]

# Summarize your project in < ~75 words. This description will appear at the top of your page and on the list page with other projects..

summary: "Thyroid hormone levels potentially impacts cortical structures and cognitive performance. This project aims to determine if TSH levels and cortical structure can predict cognitive performance for executive function, attention, and working memory using Elastic Net Regression ."

# If you want to add a cover image (listpage and image in the right), add it to your directory and indicate the name
# below with the extension.
image: "project_image.png"
---

## Project definition
---
## Background

Cognitive impairment is a leading cause for loss of functional independence in old age and often precedes cognitive disorders such as Alzheimer’s Disease (AD). Dementia is predicted to increase to 152.8 million cases by 2050 (1). However, more research is needed to identify modifiable factors to decrease risk of cognitive decline and dementia (2). 

Thyroid hormones have an established role in the development and the maturation of the brain through neurogenesis, synaptogenesis, and myelination (3). However, the impact and the role of thyroid hormones on the adult brain is more unclear. There are conflicting findings of the impact of thyroid dysregulation on cognitive impairment (4). An association was found between the thyroid function and the cortical architecture in functional areas of the brain linked to neurodegeneration (5), suggesting a mechanistic link. In addition, thyroid function is known to modulate mood, and result in certain psychiatric conditions such as depression and bipolar disorder (6). Comorbid depression and sub-threshold hypothyroidism comorbidity was shown to result in reduced gray matter volume in the middle front gyrus and lower executive function performance (7). The middle front gyrus is also associated with working memory and attention, suggesting that these cognitive subdomains may also be impacted. Together, these suggest that thyroid function may modulate function in multiple cognitive domains through more than one pathway. However, due to missing depressive scores in majority of participants, depression scores was unable to be accounted for as a predictive variable.

Thus, this research project has the following objectives:

**Primary**:  To determine if thyroid stimulating hormone (TSH), and cortical structure are able to sufficiently predict cognitive scores in executive function, working memory, and attention, using elastic net regression machine learning. 

**Secondary**: To determine if adding sex as a predictor improves the predictive performance of the model.


### Tools
This project relied on numerous tools such as:
1) Git and GitHub to use and share methods;
2) Python Packages: sklearn, shap, pandas, numpy

### Data
The database used for the project was “The National Institute of Mental Health (NIMH) and Research Volunteer Data Set” from OpenNeuro. This dataset consists of clinical assessments, mood-related psychometrics, cognitive function neuropsychological tests, structural and functional MRI, diffusion tensor imaging (DTI), comprehensive magnetoencephalography battery (MEG), and blood samples. 

Link to the dataset: https://openneuro.org/datasets/ds005752/versions/2.1.0




### Project deliverables 
At the end of this project, these files will be made available:
1) Python scripts for the 3 different predictive models;
2) Figures of this results; 
3) A repository on GitHub;

## Methodology

### Variables
The main outcomes were chosen for the main models are from the NIH Toolbox Cognitive Battery to represent cognitive performance, with the following cognitive subdomain.:

 1) Flanker Inhibitory Control and Attention Task Score: Attention
 2) Dimensional Change Card Sort Task Score: Executive Function
 3) List Sorting Working Memory Task Score: Working Memory

These outcomes were chosen due to existing literature suggesting that thyroid activity may impact these specific cognitive subdomains. This is a continuous variable of the participant’s score in the cognitive subdomain. 

A secondary control model was also created in which the outcome was sex. This is a binary outcome of either male or female.

### Models
The machine learning method chosen was elastic net regression due to the high amounts of predictors used for this model. Elastic net regression has penalty coefficients that allows the model to choose for the best features and stabilize the model. SHAP values were also calculated to give insight into which predictors had the highest predictive power.

While, the main goal of the project was to create a model predicting cognitive score based on TSH levels, and structural brain features, additional models were created to ensure robustness and confirm the pipeline developed works for more established relationships.

The following models were created: 

**Model 1**

This is the original planned model to determine if TSH and brain features are able to predictive various cognitive subdomain scores
Output:

(1) Flanker Inhibitory Control and Attention Task Score

(2) Dimensional Change Card Sort Task Score

(3) List Sorting Working Memory Task Score

Predictors: log(TSH), 68 CT variables, 68 SA variables, ICV, age

**Model 2**

This model modifies the first model by residualizing the brain variables to account for head size and age.

Output: 

(1) Flanker Inhibitory Control and Attention Task Score

(2) Dimensional Change Card Sort Task Score

(3) List Sorting Working Memory Task Score

Predictors: log(TSH), sex, 68 CT residuals after adjusting for age and ISV, 68 SA residuals after adjusting for age and ISV

**Model 3**

This model serves to confirm the pipeline developed works for variables and outcomes that have more literature evidence.

Output: Sex

Model 3.1

Predictors: age, ICV, CT, SA

Model 3.2 (added log(TSH)

Predictors: log(TSH), ICV, CT, SA

Model 3.3 (residualized and without log(TSH)

Predictors: age, CT and SA residualized for age and CV

Model 3.4 (residualized with log(TSH)

Predictors: log(TSH), age, CT and SA residualized for age and CV


---
## Results

**Cognitive Performance Models**

Across the cognition outcomes, neither elastic-net model showed meaningful held-out prediction of cognitive performance. Most R² values were close to zero or below zero, indicating that the models did not improve over a simple mean-prediction baseline in held-out participants.

The original model showed a very small positive R² for working memory, but the effect was weak and convergence warnings occurred during fitting. Overall, these results suggest that the tested combinations of TSH, sex, age, ICV, cortical thickness, and surface area did not robustly predict cognition in held-out participants.

SHAP outputs were generated to inspect variable contributions, but they should be interpreted cautiously because overall prediction performance was weak.

In the cognitive performance models, because held-out prediction was weak, the SHAP outputs should be treated as descriptive rather than as evidence of reliable prediction.

Across the cognition models, log(TSH) showed no meaningful SHAP contribution. In the original working-memory model, age was the strongest SHAP contributor and ICV also contributed, but this result should be interpreted cautiously because the held-out prediction was very weak and convergence warnings occurred during fitting.

For the other cognition models, the highest SHAP values were mainly assigned to cortical thickness and surface-area features, including residualized CT/SA features in Model 2.

### Model 1 Performance Metrics

| Outcome | R-squared | RMSE | MAE |
| --- | --- | --- | --- |
| ATTN_EXE_COMP | -0.021 | 0.644 |  0.510 |
|WKMEM | -0.008 | 10.352 | 8.357 |
|EF_COMP | -0.003 | 0.813 | 0.679 |

### Model 2 Performance Metrics

| Outcome | R-squared | RMSE | MAE |
| --- | --- | --- | --- |
| ATTN_EXE_COMP | -0.643 | 0.644 |  0.513 |
|WKMEM | -0.042 | 10.541 | 8.578 |
|EF_COMP | -0.015 | 0.818 | 0.682 |

#### Figure 1 and 2: [The performance metrics for the main models predicting cognitive performance for both the original and residualized ](https://github.com/brainhack-school2026/TSH-predict-CogPerformance/blob/main/03_results/cognition/results.md)

### Model 3 Performance Metrics

| Model | Pooled ROC AUC | Accuracy | Balanced Accuracy |
| --- | --- | --- | --- |
| Original | 0.788 | 0.729 |  0.723 |
|Original + TSH | 0.788 | 0.729 | 0.723 |
|Residualized | 0.535 | 0.518 | 0.507 |
|Residualized + TSH | 0.536  |  0.523 | 0.510  |

#### Figure 3: [The performance metrics for the sex predictive model](https://github.com/brainhack-school2026/TSH-predict-CogPerformance/blob/main/03_results/sex_classification_exercise/results.md)

**Sex Predictive Models**

The non-residualized CT/SA sex-classification models showed moderate held-out classification performance. The SHAP summaries indicate that ICV was the strongest individual contributor in these models, consistent with the drop to near-chance performance after CT and SA were residualized for age and ICV.

Adding log(TSH) did not improve the printed performance metrics and did not produce a meaningful SHAP contribution.

Overall, the positive-control exercise shows that the pipeline can recover a sex-classification signal when age, ICV, cortical thickness, and surface area are included. After age/ICV residualization, this signal was no longer recovered above chance-level performance.

In the original, non-residualized sex-classification models, ICV was the strongest individual SHAP contributor. Additional contributions came from cortical surface-area and cortical-thickness features. Age had little SHAP contribution, and adding log(TSH) did not produce a meaningful SHAP contribution.

In the residualized models, the highest SHAP values were assigned to age/ICV-residualized cortical thickness and surface-area features. However, these models performed close to chance, so the SHAP rankings should be interpreted cautiously. 


## Discusssion
The two main predictive models were not able to reliably predict cognitive scores. Findings regarding the relationship between thyroid hormone levels and cognitive performance are generally mixed. This result is consistent with Quinque et al 7. The authors found that participants with Hashimoto’s Thyroiditis (hypothyroidism) were not significantly associated with cognitive impairment in working memory, and attention. The authors suggest that cognitive deficits may not be apparent in young, healthy individuals, due to cognitive reserve. The NIMH database is a healthy volunteer study, thus specifically excludes individuals with education levels lower than completion of middle school and those with mental health conditions, like depression. Thus, individuals whose cognitive performance may be impacted by thyroid levels may not be in the dataset. Additionally, due to depression scores being dropped as a predictor variable, one of the pathways in which thyroid hormones modulate cognitive performance may not be captured, further weakening the relationship.

Our results contradict the findings from Zhao et al., and Beydoun et al. 8,9, which their results suggest that TSH levels can impact cognitive performance. Zhao et al., found that higher levels of TSH is associated with better performance in psychomotor speed, and attention; while, Beydoun et al., found that comorbid depression and hypothyroidism results in worse cognitive performance in executive function. These results together suggest TSH is associated with cognitive performance, in which low levels of TSH result in poor performance and vice-versa. Beydoun et al. found that the interaction term between TSH and depression score to be non-significant; suggesting the relationship between TSH and depression in relation to cognitive performance, in the model,  is additive. This suggests that the predictive accuracy of TSH is accurate but simply weak. This is supported by SHAP, which shows TSH as a very weak predictor of cognitive performance. 

Based on the SHAP values, the largest contribution to predictive power in the model are various brain regions. The brain regions that are calculated to be the most predictive by SHAP are not consistent with literature. The most predictive brain regions are the right supramarginal gyrus, and the right transversternal gyrus, as opposed to the middle front gyrus and the left anterior cingulate cortex found in literature 7,8.

In contrast, the sex predictive model had fairly acceptable performance, with the non-residualized version performing the most accurately. This is fairly consistent with literature as machine learning models have been shown to be able to predict sex of a participant via imaging of their brains 10. In addition, the SHAP values are somewhat consistent with literature, since the most predictive region is the superior frontal gyrus 10. In addition, when accounting for the head and brain size in the residualized model, the predictive performance worsened. This is also consistent with literature since intracranial volume is a large contributor to model performance 11. This is also seen in the SHAP values for the sex difference model. 
Overall, through the positive control of the sex predictive model, it was shown that this pipeline works for creating an accurate predictive model when the model is given predictors strongly related to the outcome. The main models had poor predictive performance due to the weak relationship between the predictors and cognitive performance, rather than poor methodology. Considering that the dataset uses healthy volunteers, which may not capture populations susceptible to cognitive decline due to TSH, and the lack of depressive score data, the model may also have been inaccurate due to the unavailability of data for relevant populations and stronger predictive variables. Thus, future predictive models for cognitive performance should ensure to utilize datasets with relevant populations and variable data to avoid bias.  


## References
1) Nichols, E. et al. Estimation of the global prevalence of dementia in 2019 and forecasted prevalence in 2050: an analysis for the Global Burden of Disease Study 2019. Lancet Public Health 7, e105–e125 (2022).

2) Rasmussen, J. & Langerman, H. <p>Alzheimer’s Disease – Why We Need Early Diagnosis</p>. Degener. Neurol. Neuromuscul. Dis. Volume 9, 123–130 (2019).
Bernal J. Thyroid Hormones in Brain Development and Function. [Updated 2025 Sep 29]. In: Feingold KR, Adler RA, Ahmed SF, et al., editors. Endotext [Internet]. South Dartmouth (MA): MDText.com, Inc.; 2000-. Available from: https://www.ncbi.nlm.nih.gov/books/NBK285549/

3) Eslami-Amirabadi, M., & Sajjadi, S. A. (2021). The relation between thyroid dysregulation and impaired cognition/behaviour: An integrative review. Journal of neuroendocrinology, 33(3), e12948. https://doi.org/10.1111/jne.12948

4) Wu X, Liu H, Cui L, Mo M, Li C. Genetically determined thyroid function and cerebral cortex structure: A Mendelian randomization study. Adv Clin Exp Med. 2025 Nov;34(11):1863-1879. doi: 10.17219/acem/199321. PMID: 40699126.

5) Hendrick V, Altshuler L, Whybrow P. Psychoneuroendocrinology of mood disorders. The hypothalamic-pituitary-thyroid axis. Psychiatr Clin North Am. 1998 Jun;21(2):277-92. doi: 10.1016/s0193-953x(05)70005-8. PMID: 9670226.

6) Hendrick V, Altshuler L, Whybrow P. Psychoneuroendocrinology of mood disorders. The hypothalamic-pituitary-thyroid axis. Psychiatr Clin North Am. 1998 Jun;21(2):277-92. doi: 10.1016/s0193-953x(05)70005-8. PMID: 9670226.

7) Zhao S, Du Y, Zhang Y, Wang X, Xia Y, Sun H, Huang Y, Zou H, Wang X, Chen Z, Zhou H, Yan R, Tang H, Lu Q and Yao Z (2023) Gray matter reduction is associated with cognitive dysfunction in depressed patients comorbid with subclinical hypothyroidism. Front. Aging Neurosci. 15:1106792. doi: 10.3389/fnagi.2023.1106792

8) Beydoun, M. A., Beydoun, H. A., Kitner-Triolo, M. H., Kaufman, J. S., Evans, M. K., & Zonderman, A. B. (2013). Thyroid hormones are associated with cognitive function: moderation by sex, race, and depressive symptoms. The Journal of clinical endocrinology and metabolism, 98(8), 3470–3481. https://doi.org/10.1210/jc.2013-1813
 
9) Dibaji M, Ospel J, Souza R and Bento M (2024) Sex differences in brain MRI using deep learning toward fairer healthcare outcomes. Front. Comput. Neurosci. 18:1452457. doi: 10.3389/fncom.2024.1452457

10) Sanchis-Segura C, Ibañez-Gual MV, Aguirre N, Cruz-Gómez ÁJ, Forn C. Effects of different intracranial volume correction methods on univariate sex differences in grey matter volume and multivariate sex prediction. Sci Rep. 2020 Jul 31;10(1):12953. doi: 10.1038/s41598-020-69361-9. Erratum in: Sci Rep. 2020 Oct 29;10(1):18937. doi: 10.1038/s41598-020-75522-7. PMID: 32737332; PMCID: PMC7395772. 
