# Protocol

## Title:
Cost-Effectiveness of Onasemnogene Abeparvovec versus Nusinersen for Spinal Muscular Atrophy Type 1: A Markov Cohort Cost-Utility Analysis Protocol

## Project Aim:
The aim of this project is to conduct a reproducible cost-utility analysis in R comparing one-time onasemnogene abeparvovec (Zolgensma) with lifelong nusinersen (Spinraza) treatment for infants with spinal muscular atrophy (SMA) Type 1, from the Dutch healthcare payer perspective. All model logic will be implemented from scratch in base R, without specialized health-economic packages, in order to make every modelling assumption explicit and inspectable; the analysis environment is minimal (base R plus `ggplot2` for visualization), the software versions will be reported in the final report, and all stochastic analyses will be fully reproducible through a single random seed.

## Background
Spinal muscular atrophy is an autosomal recessive neuromuscular disorder caused by insufficient levels of the survival motor neuron (SMN) protein, most commonly due to homozygous deletion or mutation of the survival motor neuron 1 (*SMN1*) gene. The estimated incidence is approximately 1 in 10,000 live births, making SMA one of the most common genetic causes of infant mortality [@verhaart2017]. Disease severity is modified primarily by the number of copies of the *SMN2* backup gene: infants with two or fewer *SMN2* copies typically develop SMA Type 1, the most severe form, which accounts for approximately 60% of new cases [@verhaart2017]. Before the availability of disease-modifying therapies, SMA Type 1 was characterized by progressive, irreversible motor neuron loss; in the natural-history cohort of the Pediatric Neuromuscular Clinical Research (PNCR) network, most untreated infants died or required permanent assisted ventilation before two years of age [@finkel2014; @day2021].

The treatment landscape for SMA Type 1 has been transformed by three disease-modifying therapies. Nusinersen, an intrathecally administered antisense oligonucleotide that modifies *SMN2* pre-messenger RNA splicing, was the first approved therapy. In the randomized, sham-controlled ENDEAR trial, 51% of treated infants achieved a motor-milestone response versus 0% under sham control, the hazard ratio (HR) for death or permanent ventilation was 0.53, and the HR for death alone was 0.37, leading to early trial termination [@finkel2017]. Onasemnogene abeparvovec is a one-time intravenous gene therapy delivering a functional *SMN1* transgene via an adeno-associated virus serotype 9 (AAV9) vector, established first in the phase 1/2 START study [@mendell2017] and subsequently in the single-arm phase 3 STR1VE trial, in which 13 of 22 infants (59%) achieved independent sitting and 20 of 22 (91%) were alive and free of permanent ventilation at 14 months of age, compared with 26% in a matched natural-history cohort [@day2021].

These clinical advances have created an exceptional economic problem. Onasemnogene abeparvovec launched with a United States list price of US$2.125 million, the highest of any drug at the time of approval [@icer2019], with an expected price of approximately €2.0 million in the Netherlands [@broekhoff2021]. Nusinersen carries a lower per-dose price (a Dutch media-reported list price of approximately €70,000 per 12 mg dose) but requires lifelong recurring administration: four loading doses followed by maintenance dosing every four months, with no stopping rule in the product label, which accumulates to a lifetime acquisition cost that can exceed that of the gene therapy. In the Netherlands, reimbursement decisions are guided by informal willingness-to-pay reference values of €10,000 to €80,000 per quality-adjusted life-year (QALY), scaled to the severity of the disease [@zin2016]. Under these reference values, published economic evaluations conclude that neither therapy is cost-effective at list prices: the Dutch early cost-effectiveness analysis by Broekhoff et al. reported an incremental cost-effectiveness ratio (ICER) of €53,447 per QALY for onasemnogene abeparvovec versus nusinersen, estimated that the gene-therapy price would need to decrease to €680,000 to comply with Dutch willingness-to-pay reference values, and showed that uncertainty about long-term treatment durability ("relapse") can multiply the ICER severalfold [@broekhoff2021].

To date, no randomized head-to-head trial has compared onasemnogene abeparvovec with nusinersen; the pivotal evidence derives from a randomized trial against sham control (ENDEAR) and a single-arm trial against natural history (STR1VE), and long-term durability of the gene therapy beyond available follow-up is unknown. Comparative cost-effectiveness must therefore be estimated through decision-analytic modeling, in which the best available clinical and economic evidence is synthesized within an explicit model structure, with the unanchored nature of the treatment comparison and the durability uncertainty acknowledged and explored rather than hidden.

Therefore, the objective of this project is to conduct a Markov cohort cost-utility analysis to compare onasemnogene abeparvovec with nusinersen for symptomatic SMA Type 1 infants from the Dutch healthcare payer perspective, and to quantify how the conclusion depends on parameter uncertainty and, separately, on structural assumptions about treatment durability and treatment continuation.

## Research Question
In infants with genetically confirmed, symptomatic spinal muscular atrophy Type 1 treated before six months of age, is one-time onasemnogene abeparvovec cost-effective compared with lifelong nusinersen treatment from the Dutch healthcare payer perspective, and how sensitive is the conclusion to parameter uncertainty and to structural assumptions about long-term durability and comparator treatment continuation?

## PICO

### Population
Infants with genetically confirmed SMA Type 1 (bi-allelic *SMN1* mutation, two or fewer *SMN2* copies), symptomatic at treatment initiation, treated before six months of age, corresponding to the enrolled populations of the ENDEAR and STR1VE trials [@finkel2017; @day2021].

### Intervention
Onasemnogene abeparvovec (Zolgensma): a single intravenous infusion of 1.1 × 10^14 vector genomes per kg, administered once, with no subsequent disease-modifying treatment.

### Comparator
Nusinersen (Spinraza): 12 mg intrathecal doses administered as four loading doses (day 0, 14, 28, and 63) followed by maintenance doses every four months, continued for life as long as the patient is alive, consistent with the absence of a stopping rule in the product label.

### Outcomes
Outcomes will be ranked a priori to define which analyses are confirmatory and which are exploratory, to avoid selective reporting.

#### Primary Outcome
- **Incremental net monetary benefit (INMB) of onasemnogene abeparvovec versus nusinersen at €80,000 per QALY**: the most decision-coherent summary statistic for this evaluation, because the ICER is numerically unstable when incremental QALYs approach zero and does not itself encode the Dutch willingness-to-pay decision rule, whereas the INMB expresses the comparison directly against the reference value on the monetary scale.

#### Secondary Outcomes
##### Key secondary (confirmatory)
- **ICER** (incremental cost per QALY gained, onasemnogene abeparvovec versus nusinersen), reported alongside the direction of the incremental pair (dominance or extension), since the ICER remains the conventional reporting metric of Dutch and international cost-effectiveness appraisal.
- **Total discounted costs and QALYs per strategy**, as the decomposition underlying the incremental analysis.

##### Exploratory
- **Cost-effectiveness acceptability curve (CEAC)** over a willingness-to-pay grid of €0 to €500,000 per QALY.
- **Expected value of perfect information (EVPI)** across the same grid.
- **Durability-scenario results**: ICER and INMB under annual SMA-event ("relapse") probabilities from 0% to 10% from year 2 onward.
- **One-way deterministic sensitivity ranges** (tornado diagram) on the INMB.

### Timing (if applicable)
The analysis will be conducted over a lifetime horizon with annual cycles, and outcomes will be evaluated as discounted totals over that horizon. Scenario analyses will repeat the evaluation over 10-year and 20-year horizons to assess the influence of the horizon choice.

### Perspective
The Dutch healthcare payer (Zorginstituut Nederland) perspective: direct medical costs only (drug acquisition, administration, and health-state care). Productivity costs and patient/family transfers are excluded.

### Discounting
Costs will be discounted at 4.0% and effects at 1.5% per annum, in accordance with the Dutch pharmacoeconomic guideline [@zin2016]. A scenario analysis will apply 3.0%/3.0% discounting, the convention used in most non-Dutch evaluations, to enable cross-study comparison.

### Willingness-to-Pay
The primary willingness-to-pay reference value will be €80,000 per QALY, the upper rung of the severity-proportional Dutch reference range appropriate for a disease with very high burden [@zin2016], with acceptability curves reported over €0 to €500,000 per QALY.

## Eligibility Criteria

Eligibility criteria are defined for evidence sources informing model parameters, since the analysis synthesizes inputs of several types rather than including primary studies into a pooled effect estimate.

### Inclusion Criteria
- Phase III randomized controlled trials of nusinersen in infantile-onset SMA reporting event-free survival (death or permanent ventilation) or motor-milestone outcomes (ENDEAR) for transition probabilities of the comparator arm.
- Phase III single-arm trials of onasemnogene abeparvovec in symptomatic infants with two *SMN2* copies reporting survival free of permanent ventilation and motor milestones (STR1VE) for the intervention arm. **Single-arm evidence is eligible only because no randomized evidence exists for this intervention; its use constitutes an unanchored (naive) indirect comparison and is acknowledged throughout as the principal comparability limitation.**
- Peer-reviewed published cost-effectiveness analyses and health technology assessment (HTA) reports of SMA therapies (e.g., ICER, Zorginstituut Nederland, NICE documents), as sources of applied transition probabilities, utilities, and cost inputs.
- Peer-reviewed utility studies using preference-based instruments (e.g., EQ-5D) in SMA populations.
- Official price lists, HTA reports, and the Dutch costing manual as sources for drug acquisition, administration, and health-state care costs [@hakkaart2015].

### Exclusion Criteria
- Studies in presymptomatic infants (e.g., SPR1NT) or later-onset SMA (e.g., CHERISH), because these populations are outside the decision problem.
- Phase I/II studies, except where no phase III evidence exists for a required input; the START study is retained for background context only, not for parameter extraction.
- Conference abstracts, letters, editorials, and study protocols without extractable data.
- Duplicate publications of the same trial; the publication with the most mature follow-up will serve as the primary source.
- Non-peer-reviewed media sources, except as a last-resort documentation of drug list prices, in which case the input is explicitly flagged for verification in the parameter table.

## Search Strategy

### Databases
PubMed will be searched from database inception to August 2026, complemented by ClinicalTrials.gov to cross-check trial registrations and identify the most mature follow-up publications. Targeted searches of the gray literature will be performed on the websites of Zorginstituut Nederland, the National Institute for Health and Care Excellence (NICE), and the Institute for Clinical and Economic Review (ICER) for HTA assessments and applied economic inputs. Reference lists of all included economic evaluations will be manually screened for additional parameter sources.

### Search Terms
The search will include terms for:
Population: "spinal muscular atrophy", "SMA", "infantile-onset", "SMA type 1", "SMA type I".
Interventions: "nusinersen", "Spinraza", "onasemnogene abeparvovec", "Zolgensma", "AVXS-101", "gene therapy".
Economic and utility concepts: "cost-effectiveness", "cost-utility", "economic evaluation", "quality of life", "utilities", "EQ-5D".
Boolean operators (AND/OR) will be used to combine search terms, and database-specific syntax will be applied as appropriate.

### Study Selection Process
Records identified through the searches will be screened against the predefined eligibility criteria, first at the title/abstract level and then at full text. Selection will be conducted by a single reviewer (ZB) due to the scope and resource constraints of this project. This approach differs from the standard practice of independent screening by two reviewers and is acknowledged as a methodological limitation. Reasons for exclusion will be documented per parameter domain.

### Language restrictions:
No language restrictions will be applied. Studies published in English and Dutch will be assessed directly. Studies published in other languages will be considered where a reliable translation is available.

### Limitations:
Due to the lack of institutional access to subscription-based databases, Embase and MEDLINE (via Ovid) will not be searched; some relevant records may therefore not be identified. In addition, negotiated drug prices in the Netherlands are confidential, and official list prices are not always publicly documented; where the Dutch list price could not be verified against an official source, a media-reported price is used, flagged for verification, and assigned a wide uncertainty range in sensitivity analyses. Access to paywalled HTA appendices may similarly be limited; where a required Dutch input was not retrievable, values from comparable jurisdictions were substituted with wide ranges, and the substitution is documented in the parameter table.

## Data Extraction

### Parameter-Specific Primary Sources
For each model parameter, data will be extracted from the most credible available source, with the complete parameter-level provenance recorded in `data/processed/parameters.csv`:
- **Onasemnogene abeparvovec year-1 event probability**: STR1VE, 20 of 22 infants alive and free of permanent ventilation at 14 months [@day2021], parameterized as a Beta distribution directly from trial counts.
- **Nusinersen year-1 event probabilities**: ENDEAR-derived monthly transition probabilities (death 0.0184, permanent ventilation 0.0355 per month) as applied in a published cost-effectiveness analysis [@finkel2017; @wang2022], converted to an annual competing-risk probability (see below).
- **Mortality on permanent ventilation**: survival of ventilated SMA Type 1 patients [@gregoretti2013], as applied in [@wang2022].
- **Utilities**: EQ-5D values for SMA Type I [@thomson2017] for the permanent-ventilation state, as applied in [@thokala2020]; treated-state utilities as tabulated in [@wang2022], combined into a milestone-weighted event-free utility (see below).
- **Drug acquisition costs**: expected Dutch price of onasemnogene abeparvovec [@broekhoff2021]; Dutch media-reported list price of nusinersen, flagged for verification.
- **Administration and health-state care costs**: Dutch costing manual conventions [@hakkaart2015] and published cost-effectiveness inputs [@wang2022; @icer2019], with all assumptions flagged.
- **Background mortality**: Gompertz approximation calibrated to Dutch period life expectancy (approximately 81.5 years; Statistics Netherlands [@cbs]).

### Variables to Extract
A standardized parameter extraction form will be used, recording for every parameter: name, description, value, unit, assumed uncertainty distribution, derivation of the standard error, plausible range for deterministic sensitivity analysis, full source citation, and a flag for any assumption requiring verification. The parameter table will be piloted on the transition-probability inputs before completing the full extraction, and every value in the table must carry a citable source or an explicit assumption flag.

### Outcomes
**Handling of unreported inputs:** Where only monthly probabilities are available (ENDEAR-derived inputs), annual transition probabilities will be computed under a discrete-time competing-risk conversion rather than by simple multiplication, and the arithmetic will be documented in the model code. Where no Dutch-specific value is retrievable (health-state care costs, administration costs), values from comparable jurisdictions will be substituted and assigned wide ranges that are propagated through the sensitivity analyses; all substitutions are flagged in the parameter table and no input is imputed silently. The event-free utility will be derived as a milestone-weighted combination of treated-state utilities (proportion achieving independent sitting in STR1VE multiplied by the sitting utility, plus the complementary proportion multiplied by the not-sitting utility). Kaplan-Meier digitization and individual-patient-data reconstruction [@guyot2012], followed by parametric survival extrapolation, are acknowledged as the methodological next step for the survival inputs but are out of scope for this analysis.

## Risk of Bias Assessment
No formal risk-of-bias instrument will be applied to the parameter sources, because the analysis extracts diverse input types (trial event rates, prices, utilities, care costs) for which no single validated tool applies; this is acknowledged as a methodological limitation. Instead, the credibility of each input will be handled through an explicit evidence hierarchy: randomized trial evidence (ENDEAR) will be regarded as the least susceptible to bias for the comparator arm; single-arm trial evidence (STR1VE) will be regarded as inherently more susceptible to bias and confounding by natural-history comparison, which is why the unanchored nature of the between-arm comparison is stated as the principal limitation of the evaluation; and HTA, peer-reviewed economic evaluations, and official price documents will be preferred over media sources, which are used only under an explicit verification flag. The credibility of the model itself will be assessed through validation following good-practice guidance for decision-analytic modeling [@caro2012], reported in a dedicated validation document.

## Statistical Analysis

### Cost-Effectiveness Model
A three-state Markov cohort model will be used, with states: event-free (alive without permanent ventilation), permanent assisted ventilation, and dead. All patients enter the model in the event-free state at treatment initiation (approximately six months of age). The model will run in annual cycles over a lifetime horizon (99 cycles), with transitions parameterized separately for year 1 (trial-derived event probabilities) and subsequent years (durability events plus background mortality), following standard cohort state-transition conventions [@alarid2023]. Background mortality will be modeled with a Gompertz hazard calibrated to Dutch period life expectancy [@cbs], combined with disease-specific mortality under a competing-risks formulation. Costs and QALYs will be accumulated with half-cycle correction, and Dutch differential discounting (4.0% costs, 1.5% effects) will be applied [@zin2016]. The model will be implemented in base R with in-code assertions at every cycle (transition probabilities bounded and row-stochastic, cohort conservation, monotone death accumulation), so that structural errors trigger immediate failure rather than silent propagation.

### Base-Case Analysis
The base-case analysis will report total discounted costs and QALYs per strategy, incremental costs and QALYs, the ICER, and the INMB at €80,000 per QALY. A strategy will be considered cost-effective at a given willingness-to-pay threshold if it yields the highest expected net monetary benefit; dominance (cheaper and more effective) will be stated explicitly rather than expressed as a negative ICER.

### Deterministic Sensitivity Analysis
One-way deterministic sensitivity analyses will be conducted on the INMB, varying each key parameter across its prespecified plausible range (recorded in the parameter table) while holding all others constant. Ranges will be fixed before analysis to avoid post hoc selection. Results will be presented as a tornado diagram. **Parameter ranges for flagged assumptions (nusinersen price, care costs) are deliberately wide, and the tornado diagram is the primary vehicle for communicating how much of the conclusion rests on those unverified inputs.**

### Probabilistic Sensitivity Analysis
A probabilistic sensitivity analysis will be conducted with 5,000 draws from the joint parameter distribution, using a single random seed for reproducibility. Probabilities and utilities will be assigned Beta distributions and costs Gamma distributions, parameterized by the method of moments; the onasemnogene abeparvovec year-1 event probability will be drawn from a Beta distribution parameterized directly from trial counts (2 events among 22 infants), so that the stochastic uncertainty of the small pivotal trial is propagated. Long-term durability will be represented as a wide distribution on the annual relapse probability, reflecting the absence of long-term follow-up. Results will be presented on the cost-effectiveness plane and as cost-effectiveness acceptability curves over €0 to €500,000 per QALY.

### Assessment of Structural Uncertainty
Structural uncertainty will be assessed through prespecified scenario analyses rather than through the probabilistic analysis, because the principal structural assumptions are discrete choices that cannot meaningfully be represented as continuous parameter distributions: (1) durability of onasemnogene abeparvovec, varied from permanent cure (0% annual relapse) to 10% annual relapse from year 2, following the relapse-scenario design of the Dutch reference evaluation [@broekhoff2021]; (2) continuation of nusinersen, contrasting lifelong dosing per the label with treatment stopped after five years, since real-world discontinuation is a documented source of divergence between published evaluations; (3) discounting (Dutch 4.0%/1.5% versus international 3.0%/3.0%); (4) time horizon (lifetime versus 10 and 20 years); and (5) the numerical effect of the half-cycle correction, evaluated by rerunning the model with and without it.

### Value of Information Analysis
The expected value of perfect information (EVPI) will be computed across the willingness-to-pay grid from the probabilistic analysis output, and translated to an annual population level using an illustrative incident cohort of 20 SMA Type 1 births per year in the Netherlands. **Interpretation caveat:** an EVPI of approximately zero does not mean that uncertainty is absent; it means that parameter uncertainty, as parameterized, cannot change the decision. Decision-relevant uncertainty that resides in structural assumptions (durability, treatment continuation) is quantified through the scenario analyses instead, and the report will state this distinction explicitly rather than presenting EVPI as a comprehensive uncertainty measure.

### Model Validation
Validation will follow good-practice guidance for decision-analytic models [@caro2012] and will be reported in a dedicated validation document. Internal validity will be established through in-code assertions at every cycle and an automated validation suite. Cross-validation will compare year-1 model outcomes against the source trials (event-free survival at one year versus STR1VE and ENDEAR) and compare incremental results against the published Dutch evaluation [@broekhoff2021], with divergences traced to their assumption-level sources (principally treatment continuation). Face validity will be assessed by verifying that every sensitivity result moves in the clinically and economically expected direction.

## Confidence in the Evidence
Confidence in the model results will be characterized qualitatively rather than with a formal grading framework, in acknowledgment of the scope of this project. Three considerations will structure this assessment: (1) parameter uncertainty, quantified through the probabilistic and deterministic sensitivity analyses, is dominated by the small pivotal trial (n = 22), the heterogeneity of utility values across published sources (which range from below zero to above 0.8 for comparable states [@wang2022]), and the flagged cost inputs; (2) structural uncertainty (durability and comparator continuation) cannot be quantified probabilistically and is reported through scenario analysis, and is expected to be more decision-relevant than parameter uncertainty; and (3) the comparability of the two arms rests on an unanchored indirect comparison between a randomized sham-controlled trial and a single-arm study, which no sensitivity analysis can resolve. These limitations will be stated alongside the results in the final report.

## Reporting Standard
The final report will conform to the Consolidated Health Economic Evaluation Reporting Standards 2022 (CHEERS 2022) [@husereau2022]. The completed CHEERS 2022 checklist will be included as a supplement, and all deviations related to the educational scope of the project (e.g., single-reviewer data extraction, flagged assumptions) will be reported transparently.

## Reproducibility
Analyses will be conducted in R, with the R version and package versions reported in the final report. All model logic will be implemented from scratch in base R; `ggplot2` is the only non-base dependency, so the environment footprint is deliberately minimal and no package-locking is required. All analysis scripts will be numbered and version-controlled in the project repository, all stochastic analyses will use a single prespecified random seed, and a master script (`analysis/main_analysis.R`) will reproduce every figure and table in the final report from a clean clone of the repository.

## References
References will be managed using the references.bib bibliography file.
