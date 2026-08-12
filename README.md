# Life Expectancy Predictor Analysis

A statistical analysis project using multiple linear regression to identify the main predictors of national life expectancy across ~193 countries.

## Research Question

**What are the main predictors of individual life expectancy?**

Understanding which factors most strongly influence how long people live helps shape effective public health policy and identifies priority areas for intervention.

## Data Source

- **WHO Life Expectancy Dataset** from the World Health Organization Global Health Observatory (GHO)
- Kaggle mirror: https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who
- Coverage: ~193 countries, years 2000–2015
- Final dataset: ~2,900 complete observations after removing records with missing GDP, population, or Hepatitis B data

### Key Variables

| Variable | Description |
|----------|-------------|
| `Life.expectancy` | Response variable — years a newborn is expected to live |
| `Adult.Mortality` | Death rate of adults per 1,000 population (ages 15-60) |
| `GDP` | Gross domestic product per capita |
| `Schooling` | Average years of schooling for adults aged 25+ |
| `Alcohol` | Alcohol consumption per capita (liters of pure alcohol) |
| `BMI` | Average body mass index |
| `Polio` | Polio immunization coverage (%) |
| `Income.composition.of.resources` | Index of available resources for income |
| `Status` | Developed vs. Developing country classification |

## Methodology

1. **Data Cleaning**: Combined multiple yearly files; removed incomplete records (listwise deletion)
2. **Exploratory Analysis**: Summaries, boxplots for outlier detection, skewness checks
3. **Model Fitting**: Multiple linear regression with interaction term (`BMI × Status`)
4. **Model Diagnostics**: Residual vs. fitted plots, QQ-plot, Cook's distance for influential points
5. **Model Selection**: Removed non-significant predictors (Year, p > 0.05); applied log transformation to GDP
6. **Ethics Review**: National-level aggregate data; no privacy concerns

### Final Model

```
Life.Expectancy ~ Year + Status + Adult.Mortality + Alcohol + BMI +
                  Schooling + GDP + Polio + Income.composition.of.resources +
                  BMI:Status
```

## Results

- **Adjusted R² ≈ 0.78** — the model explains ~78% of variance in life expectancy
- **Significant positive predictors**: Schooling, log(GDP), Income Composition, Polio immunization, developed country status
- **Adult Mortality** has a strong negative effect (higher mortality → lower life expectancy)
- The **BMI × Status interaction** is significant, confirming BMI affects developed and developing countries differently
- **Year** was not significant after controlling for other variables
- Residual diagnostics confirm linearity and constant variance assumptions are reasonably satisfied

## Presentation Poster

[View the full project poster (PDF)](https://github.com/VinsonYuxuanLiang/STA302_Project/blob/main/Project%20302%20Poster%20-2%20(1).pdf)

The poster includes:
- Full methodology workflow
- Residual diagnostic plots
- Coefficient interpretation
- Policy implications and limitations

## Team

Carey Lin, Natalie Choy, Vinson Liang

## Course

STA302 — Introduction to Biostatistics, University of Toronto (2025)

## References

1. Wirayuda, A. A., & Chan, M. F. (2021). A systematic review of sociodemographic, macroeconomic, and health resources factors on life expectancy. *Asia Pacific Journal of Public Health*, 33(4), 335–356.
2. Afshin, A., et al. (2022). The impact of 51 risk factors on life expectancy in Canada. *Canadian Journal of Public Health*, 113(5), 607–617.
3. Nandi, D. C., et al. (2023). An investigation of the relation between life expectancy & socioeconomic variables using path analysis for SDGs in Bangladesh. *PLoS ONE*, 18(2), e0275431.
4. World Health Organization. (2015). Life Expectancy (WHO) dataset (Global Health Observatory). https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who
