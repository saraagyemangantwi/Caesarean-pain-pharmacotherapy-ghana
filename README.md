# Real-world effectiveness of pain pharmacotherapy for caesarean section in a low- and middle-income setting

**A multicentre cross-sectional study in Ghana**

This repository holds the R analysis code for a multicentre cross-sectional study of how analgesic strategies relate to acute post-surgical pain after caesarean section, in routine clinical practice in Ghana.

---

## Background

Caesarean section is one of the most common surgical procedures worldwide. In low- and middle-income countries (LMICs), post-operative pain is often managed with limited resources and uneven access to analgesics. Evidence on what works under these routine conditions is scarce. This study looks at real-world prescribing practice to find out which pharmacological approaches are linked to lower acute post-surgical pain.

## Objectives

1. Estimate the association between analgesic regimens (opioids and multimodal analgesia) and acute post-surgical pain after caesarean section.
2. Adjust for maternal age group and anxiolytic use.
3. Test how robust these associations are, using sensitivity analyses: leave-one-variable-out (LOVO) models and bootstrap resampling.

## Study design

| Item | Description |
|---|---|
| Design | Multicentre cross-sectional study |
| Setting | Hospitals in Ghana (LMIC setting) |
| Population | Women who underwent caesarean section |
| Outcome | Acute post-surgical pain category (binary) |
| Exposures | Opioid use; multimodal analgesia |
| Covariates | Maternal age group; anxiolytic medication use |

## Variables used in the analysis

| Variable name in dataset | Description | Role |
|---|---|---|
| `Category_AcutePostsurgeryPain` | Acute post-surgical pain category | Outcome |
| `Opioids` | Opioid analgesic use | Exposure |
| `Multimodal_Analgesia` | Use of multimodal analgesic regimen | Exposure |
| `Age_Group_Coded` | Maternal age group (coded) | Covariate |
| `AnxietyMeds_coded` | Anxiolytic medication use (coded) | Covariate |

The analysis uses complete cases only (`na.omit()`).

## Statistical analysis

All analyses were carried out in **R**.

1. **Primary model.** Multivariable binary logistic regression (`glm`, binomial family) of acute post-surgical pain on opioids, multimodal analgesia, age group and anxiolytic use. Results are reported as odds ratios (ORs) with 95% confidence intervals.
2. **Multicollinearity.** Variance inflation factors (VIF) were computed with `car::vif()`.
3. **Bootstrap stability analysis.** The model was refitted on 1,000 bootstrap resamples (`boot`, `set.seed(123)`). For each coefficient, the mean and the 2.5th–97.5th percentile interval were summarised. Iterations that failed to converge were excluded.
4. **Leave-one-variable-out (LOVO) sensitivity analysis.** The model was refitted four times, each time leaving out one predictor, to see how much each variable affects the remaining estimates.

## Key findings

- **Robust effect:** multimodal analgesia was consistently linked to about 69% lower odds of the higher acute post-surgical pain category (OR 0.31). The effect held across the primary, LOVO and bootstrap analyses.
- **Unstable effect:** the estimate for opioids was imprecise and was not stable under resampling.
- **Non-dominant modifiers:** age group and anxiolytic use had small or inconsistent effects.

Taken together, the results suggest that post-caesarean pain outcomes in this setting depend mainly on an **integrated (multimodal) analgesic strategy** rather than on any single drug class or psychological modifier.

## Reproducing the analysis

### Requirements

- R (≥ 4.0)
- Packages: `readxl`, `dplyr`, `broom`, `boot`, `car`

```r
install.packages(c("readxl", "dplyr", "broom", "boot", "car"))
```

### Running

1. Download the dataset from [Zenodo](https://doi.org/10.5281/zenodo.15349612) and save it in your R working directory.
2. Update the file path in the R script to match where you saved the dataset.
3. Run the R script in this repository.

The script prints the following, in order:

- the model summary
- the odds-ratio table
- VIFs
- the bootstrap summary
- the LOVO model outputs

## Data availability

The dataset for this study is openly available on Zenodo: [https://doi.org/10.5281/zenodo.15349612](https://doi.org/10.5281/zenodo.15349612)

## Ethics

This study received ethical approval from the Committee on Human Research, Publication and Ethics (CHRPE), Kwame Nkrumah University of Science and Technology (KNUST), Kumasi, Ghana (approval number: CHRPE/AP/240/24).

## Citation

If you use this code, please cite:

> Agyemang Antwi S, Owusu-Ansah A, Agasiya PN, Mensah KB, Ansah C. Real-world effectiveness of pain pharmacotherapy for caesarean section in a low- and middle-income setting: A multicentre cross-sectional study in Ghana. *Br J Clin Pharmacol*. 2026; 1-8. doi:[10.1002/bcp.70862](https://doi.org/10.1002/bcp.70862)

## Author

**Dr. Sara Agyemang Antwi**
Department of Pharmaceutical Sciences, Kumasi Technical University, Ghana

## License

The code in this repository is released under the [MIT License](LICENSE).
