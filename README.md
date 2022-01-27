# Projections of COVID19 Epidemic Outcomes and Healthcare Demands for NYC

Authors: 

Wan Yang(1), Sasikiran Kandula(2), Jeffrey Shaman(2), Haokun Yuan(1)

(1)Department of Epidemiology, (2)Department of Environmental Health Sciences, Mailman School of Public Health, Columbia University

Contact: Wan Yang (wy2202@cumc.columbia.edu)

Acknowledgement: We thank the NYC Department of Health and Mental Hygiene (DOHMH) for sharing of data and allowing this public posting. We also thank the Columbia University Mailman School of Public Health for high performance computing and Safe Graph (safegraph.com) for providing mobility data. 

Caution: Please note that there are large uncertainties in our model projections due to unknown disease transmission dynamics (model misspecification), changing behavior and policies, delay in reporting, and under-reporting. In particular, the data our projections are based on reflect situations ~2 weeks ago due to time lags from interventions implemented to transmission events (a couple days to weeks), from infection to symptom onset (~2-6 days), from symptom onset to seeking treatment (~2-7 days), from seeking treatment to getting tested and then reported in the surveillance system (~2-7 days). In addition, how the epidemic would unfold also depend largely on behavior changes over time.  

***Projections posted from 1/5/22 onward represent measures (cases, hospitalizations, deaths, etc.) due to the Omicron variant alone and do not include Delta or other variants***

## Main Model Settings, Assumptions, Inputs, and Outputs

### 1. Model Form

#### 1.1. City-level SEIR model: 
Susceptible-Exposed-Infectious-Removed (SEIR) model accounting for reporting delay for case diagnosis, and delay from infection to hospitalization, ICU admission, and death for estimating the numbers of hospitalization, ICU, and death by week, respectively.  This model was used for projections generated from March 16 – April 3, 2020.

#### 1.2. SEIR model by age group: 
For this model, the same SEIR construct is used; however, the model parameters account for differences by age (e.g. reporting rate and disease severity) and the model is trained using age-specific incidence data for eight age groups: <1, 1-4, 5-14, 15-24, 25-44, 45-64, 65-74, and 75+ years, separately. This system is used for projections generated from 4/3/2020 onwards.  

#### 1.3. Network SEIR model by age group: 
This system accounts for spatial heterogeneity using a network model capturing connections among 42 United Hospital Fund (UHF) neighborhoods in NYC. This system also incorporates mobility data provided by Safegraph.com to gauge changes in transmission within each UHF neighborhood and between pairs of neighborhoods. The model is trained using age-specific, UHF-specific incidence data. 
For further detail, see Yang et al. 2020a medRxiv 

Note that UHF locations are based on residential address and may not match with hospital locations and catchment area. 

#### 1.4. Network SEIRS model by age group: 
This system, built on Model 1.3, further accounts for waning immunity over time. Currently, large uncertainties remain surrounding whether prior infection of SARS-CoV-2 can confer immunity (i.e. protection against future infection) and if so, the duration of such immunity. 
For simplicity, here we assume the duration of immunity is around 3 years. This assumption is in part based on our study of human endemic coronaviruses which suggests an immunity period of ~3 years for all the four human coronaviruses combined and ~5-6 years for OC43 (a beta-coronavirus in the same genus as SARS-CoV-2; unpublished data). Prior studies have also shown immunity up to ~6 years post infection for SARS-CoV-1 (Tang et al. 2011 J Immunol 186:7264-8).
In general, our simulations comparing the length of immunity (at ~1, ~3, or ~6 years) showed the magnitude of further epidemic wave would be larger if the duration of immunity were short-lived (1 year vs. 3-6 years; see Yang et al. 2020 report)

Note that UHF locations are based on residential address and may not match with hospital locations and catchment area. 

#### 1.5. Network SEIRSV model by age group: 
This system, built on Model 1.4, further accounts for vaccination. For the additional vaccination module, we model two doses of vaccine, according to currently available vaccines like the Pfizer-BioNTech vaccine. Based on Polack et al., we assume that vaccine efficacy is 85% fourteen days after the first dose and 95% seven days after the second dose. Note that here we use a vaccine efficacy estimate slightly lower than that reported for the first dose (~90% within 3-4 week of follow-up for the Pfirzer-BioNTech or Moderna vaccines) to account for the potential of lower efficacy outside the 3-4 week window should the 2nd dose be delayed. For more detail, please see https://www.medrxiv.org/content/10.1101/2021.01.21.21250228v1  

#### 1.6. Network SEIRSV model by age group, trained on covid case, ED visit, and mortality data
This system uses the same model as Model 1.5. However, in addition to case and mortality data, the model is further trained on age-grouped, UHF specific data on confirmed covid emergency department (ED) visit. This addtional dataset likely allows more accurate estimates for younger age groups (those <45 years), for whom infection fatality risk is relatively low.   

#### 1.7 Projection for the Omicron pandemic wave in NYC
Due to the dramatic changes following the surge of the Omicron variant in the city, we have re-initiated our projection system. That is, we are treating the Omicron wave separately and only use data from the week of 11/21/21 onward to generate model projections. Thus, **projections posted from 1/5/22 onward represent measures (cases, hospitalizations, deaths, etc.) due to the Omicron variant alone and do not include Delta or other variants**. As such, corresponding estimates during 11/21/21 - 1/10/22 may be lower than the city's overall data which include Delta. 

For these projections, we assume: 1) the risk of severe outcomes (hospitalization, ICU admissions, need for ventilator use) due to Omicron would be 40% of that for Delta infection; 2) Duration of hospitalization/ICU/ventilation is half of that for Delta infection. and 3) Uptake of boosters is not explicitly accounted for, as we do not have detailed data; rather, such an impact is adjusted by the filter. For other key model state variables (e.g. population susceptibility) and parameters (e.g., infection-fatality risk), we estimate them using the model-inference system using COVID-19 case, ED visit, and mortality data attributed to Omicron (here the overall counts multiplied by the percentage of cases tested positive for Omicron, after adjusting for corresponding time-lag). 

In addition, please note that due to limited data for model training (i.e. only from 11/21/21 onward), there are large uncertainties with these projections. So please use with caution. 

Updates: 
[1/27/22] projections posted from 1/27/22 also account for boosters. 

### 2. Data

Confirmed cases of COVID-19 in New York City (from Week 10, i.e. March 1-7 of 2020 to the most recent week, date labeled in the Results folder), provided by NYC DOHMH. 

#### 12/15/2020 Update on data
For this weeks' projections, we included probable COVID cases and combined them with confirmed cases for model training (ie. calibration). 
The projections may be less accurate as we continue to learn how these new data may impact the model system. 
Therefore, we caution the large uncertainties in our model projections generated this week and likely the next few weeks.   


### 3. Model Training and Assumptions

Bayesian inference approach in which the DOHMH data are used to partially constrain the model parameters and state variables prior to making a projection. The form is similar to that used for influenza forecasting; however, here the data are very limited (3 weeks) so the model is less well constrained.  Initial prior ranges are set as: transmission rate (β): [0.5, 1]; latency period (Tei): [2, 5] days; infectious period (Tir): [2, 5] days; mean reporting delay (i.e., from viral shedding to being diagnosed; Td.mean): [3, 9] days; standard deviation of reporting delay (Td.sd): [1, 3] days; and reporting rate (i.e., the proportion of infections that are diagnosed; ⍺): [5, 80]%. These parameters are estimated based on the weekly confirmed case data.  

In addition, for the delay from infection to hospitalization, ICU, and death, we used reported time from symptom onset of SARS-CoV-2 to the corresponding event (Yang et al. 2020; Zhou et al. 2020; Wang et al. 2020). To compute the numbers of different health outcomes from the model estimated total infections, we used the following probability ranges: 3-9% for hospitalization (severe and critical cases); 1-3.6% for ICU. These probabilities are based on reported numbers among diagnosed cases in NYC (information from NYC DOHMH), China (China CDC, 2020) and other countries and assuming a 20-30% ascertainment rate (Li et al., 2020). To compute the healthcare demands for each week, we used reported retention times in hospitals and ICU (Zhou et al. 2020) for corresponding estimates. COVID-19 infection fatality risk is estimated based on both case and mortality data using our model-inference system. See full method in Yang et al. 2020a

UPDATE (11/27/20): In light of recent treatment improvement and changing patient demographics, we update the healthcare related parameters to as follows: 
Length of stay in hospitals overall: mean = 12.1 days, sd = 5.2 days; 
Length of stay in ICU: mean = 13.3 days; sd = 5.9 days; 
Duration on ventilator: mean = 8.6 days; sd = 3 days; 

UPDATE (12/10/20): mean values based on information from NYC healthcare systems:
Length of stay in hospitals overall: mean = 9.1 days, sd = 5.2 days; 
Length of stay in ICU: mean = 11 days (may not be accurate); sd = 5.9 days; 
Duration on ventilator: mean = 7 days; sd = 3 days; 

### 4. Model Scenarios

Seasonality: There are 4 endemic coronaviruses infecting humans (OC43, 229E, NL63, HKU1).  These viruses typically cause mild cold-like symptoms and exhibit a pronounced seasonality with peak incidence in January-February and very little incidence in summer. The cause of this seasonality is unknown, but its presence has led to speculation that SARS-CoV-2, the virus causing COVID-19, may wane during summer months in New York City.  Consequently, we used the seasonality of OC43, which is well observed and a betacoronavirus, like SARS-CoV2, to estimate a seasonal reduction of transmissibility for SARS-CoV2 during summertime.  We then generated projections from the 2 forms for all scenarios: 1) With seasonal changes to virus transmissibility; and 2) Without seasonality. 

We generated the following projections, each with 10 model runs to provide a distribution of possible outcomes:

- No Control (i.e. Worst Case) Scenario: For these projections, the model posterior (i.e. an ensemble of model simulations with parameters and state variables as estimated following training with weekly confirmed case data) estimated with data from Week 10 (March 1-7) of 2020 (an earlier week with minimal interventions) was integrated 8 weeks into the future to create a reference, no control, “worst case” scenario. 

- As Is (i.e. Status Quo) Scenario: For these projections, the model posterior estimated using data from Week 10 through the most recent week, was integrated 8 weeks into the future to create a reference, As Is, “status quo” scenario.  While very preliminary, these projections provide a rough assessment of effectiveness of current interventions, compared to the "no control" scenario. 

Control Scenarios: Five control scenarios, using the model posterior as initial conditions and adjustment of model parameters (relative to the As Is scenario estimates) to represent different levels of interventions:

- Moderate (25%) reduction in contact rate (via social distancing) 
- Moderate (25%) reduction in contact rate (via social distancing) and moderate (25%) reduction in infectious period (via case isolation/self-quarantine/treatment, etc.)
- Large (50%) reduction in contact rate (via social distancing) and no reduction in infectious period
- Large (50%) reduction in contact rate (via social distancing) and moderate (25%) reduction in infectious period (via case isolation/self-quarantine/treatment, etc.)
- Large (50%) reduction in contact rate (via social distancing) and large (50%) reduction in infectious period (via case isolation/self-quarantine/treatment, etc.) 

Rebound Scenarios: In light of the recent uptick in mobility and potential rebound in transmission rate, from 5/1/2020 onwards, we also simulate two rebound scenarios, using the model posterior as initial conditions and adjustment of model parameters (relative to the As Is scenario estimates) to represent different levels of transmission rebound:

- Moderate (25%) increase in contact rate (relaxed social distancing) 
- Large (50%) increase in contact rate (relaxed social distancing)  

Note there is no particular specification of how reductions in contact rates or spread are achieved.  In a model of this form different reduction options (e.g. isolation vs. quarantine) are not represented explicitly; rather, they are effected by adjusting the estimated (posterior) contact rate and infectious period within the model, relative to estimates for the most recent week (the As Is scenario).

### 5. Model Output 

We use the model to estimate new weekly numbers of total infections, reported/observed infections, hospitalizations, patients in ICU, and deaths. For the latter three health outcomes we accounted for delay from infection to corresponding event as described above. 

-	New total infections are directly estimated by the model without a delay and are an unobserved quantity that includes subclinical/undiagnosed infections.  

-	New reported/observed infections include a reporting delay; the reporting rate estimated at the last day of model training was used for the entire forecast period; thus, these numbers may largely differ from observations depending on changes in testing.

-	New total hospitalizations: we assume 15-30% of reported infections are hospitalized and time from symptom onset to hospitalization of 5 days (mean; SD = 3 days; estimates from China: China CDC, 2020, adjusted for NYC). 

-	New ICU admissions: we assume 4-8% of reported infections are critical and enter ICU and time from symptom onset to ICU admission of 11 days (mean; SD=5 days; estimates from China: China CDC, 2020). 

-	New non-ICU hospitalizations: computed as the difference between new total hospitalizations and ICU admissions. 

-	New patients needing ventilators: we assume 60-100% of patients admitted to the ICU need ventilators (per data from NYC DOHMH).

-	New deaths: we assume an infection mortality risk of 0.05-1.5% based on data in NYC and elsewhere in the world and time from symptom onset to death of 10 days (mean; SD = 4 days; per data from NYC)

To support logistics and planning, we also use the model to estimate the numbers of hospital beds and ICU beds needed each week under each scenario:

-	Demand for hospital beds: projections are based on new hospitalizations each day and length of stay in hospital (Mean=24 days; SD=5.2 days, per data from the US and elsewhere). 

-	Demand for ICU beds: projections are based on new ICU admissions each day and length of stay in the ICU (Mean=21 days; SD=5.9 days, per data from the US and elsewhere). 

-	Demand for ventilators: projections are based on new ICU admissions each day and length of use (Mean=12 days; SD=3 days, per estimates from the CDC). 


We also report the estimated attack rate as the number of New Yorkers (total population size: 8,398,744 as of 2018) infected in the next 8 weeks.

### 6. Results – See tables and figures.

### NOTES ON MODEL UPDATES
#### Updates on model projections (6/6/2020):   
The City entered phase 1 reopening on Monday 6/8/2020. For projections generated during the Week stating 6/7 and Week starting 6/14, we updated model settings to anticipate potential changes. As no plan has been set for Phase 2 yet, for all projection scenarios, we assumed that the next 8 weeks will remain at Phase 1. 

- "As Is" scenario:  We incorporated historical mobility data from SafeGraph.com to anticipate increases in mobility in the coming weeks following reopening.  We assumed industries under the Phase 1 category would operate at 50% capacity during the first week, 75% during the second week, and 100% during the third and later weeks.  Based on these projected mobility changes, we further projected changes in transmission rate and infectious period based on model estimates from March 1 – June 6, 2020.  In addition, we in part accounted for potential reduction in transmission due to preventive measures (e.g. mask wearing).  [Note: here we did not account for the recent demonstrations which could increase transmission; see the Rebound scenarios below.]

With enhanced public health interventions (e.g. the contact tracing program and onsite preventive measures), reduction in transmission rate is possible.  Thus, we included 2 Control scenarios as follows:

- "Ctrl 1 moderate reduction in transmission" scenario: 25% reduction in the transmission rate with respect to the projected estimates per the "As Is" scenario. 
- "Ctrl 2 large reduction in transmission" scenario: 50% reduction in the transmission rate with respect to the projected estimates per the "As Is" scenario. 

In contrast, increase in transmission is also possible, e.g. due to mass gatherings.  Thus, we included 2 Rebound scenarios as follows:
- "Rebound 1 moderate increase in transmission" scenario: 25% increase in the transmission rate with respect to the projected estimates per the "As Is" scenario.
- "Rebound 2 large increase in transmission" scenario: 50% increase in the transmission rate with respect to the projected estimates per the "As Is" scenario.

#### Updates on model projections (6/24/2020):   
The City entered phase 2 reopening on Monday 6/22/2020. For this week's projection, we thus updated model settings to anticipate potential changes. As no plan has been set for Phase 3 yet, for all projection scenarios, we assumed that the next 8 weeks will remain at Phase 2. 
In addition, based on observations during phase 1 reopening, we make the following adjustment to the projection scenarios regarding the transmission rate:
- "Ctrl 1 moderate reduction in transmission" scenario: 10% reduction in the transmission rate with respect to the projected estimates per the "As Is" scenario. 
- "Ctrl 2 large reduction in transmission" scenario: 25% reduction in the transmission rate with respect to the projected estimates per the "As Is" scenario. 
- "Rebound 1 moderate increase in transmission" scenario: 10% increase in the transmission rate with respect to the projected estimates per the "As Is" scenario.
- "Rebound 2 large increase in transmission" scenario: 25% increase in the transmission rate with respect to the projected estimates per the "As Is" scenario.

#### Updates on model projections (6/27/2020):   
The City entered phase 2 reopening on Monday 6/22/2020 and is poised to enter phase 3 on July 6. For this week's projection, we thus updated model settings to anticipate potential changes including the phase 3 reopening. 
Per NYS guideline, all projections assume 50% maximum occupancy for industries allowed to open. In addition, for the 'As Is' scenario, we assume all New Yorker continue to wear masks, which effectively reduces transmission. PLEASE WEAR FACE MASKS WHEN YOU ARE OUTSIDE.

#### 7/22/2020
The City entered Phase 4 on Monday 7/20/2020. With the additional safety measures (more stringent restrictions) in place for Phase 4 to curb COVID-19 spread, our anticipated mobility without accounting for such restristions are likely higher than the actuals. 
As such, our projections (under the 'As Is' scenario) likely overestimate the epidemic outcomes (cases, hospitalizations etc.)
We will incorporate near real-time mobility data as they become available to improve accuracy of the projections. 

#### 7/24/2020
For this week's projections, we tentatively project the changes in mobility based on trends in the past few weeks. Hopefully, this would improve accuracy of the projections. 

#### 9/11/2020
For this week's projections, we include projected changes following re-opening of gyms, schools, and indoor dining per the city's current plans. 

#### 11/27/20 UPDATE on model parameters: 
In light of recent treatment improvement and changing patient demographics, we update the healthcare related parameters to as follows: 
Length of stay in hospitals overall: mean = 12.1 days, sd = 5.2 days; 
Length of stay in ICU: mean = 13.3 days; sd = 5.9 days; 
Duration on ventilator: mean = 8.6 days; sd = 3 days; 

#### 12/10/2020 UPDATE on model parameters: mean values based on information from NYC healthcare systems:
Length of stay in hospitals overall: mean = 9.1 days, sd = 5.2 days; 
Length of stay in ICU: mean = 11 days (may not be accurate); sd = 5.9 days; 
Duration on ventilator: mean = 7 days; sd = 3 days; 

#### 12/15/2020 Update on data
For this week's projections, we included probable COVID cases and combined them with confirmed cases for model training (ie. calibration). 
The projections may be less accurate as we continue to learn how these new data may impact the model system. 
Therefore, we caution the large uncertainties in our model projections generated this week and likely the next few weeks.   

#### 12/28/2020 Updates on model projections:   
Currently (as of 12/28/20), there is no evidence that the newly reported SARS-CoV-2 variants have arrived in NYC. However, to anticipate the potential impact of these more infectious variants, we have added a projection scenario (labeled: New Variant). Basic model assumptions: 1) the new variants would be ~70% more infectious; 2) the new variants would replace the current one in the next 4 weeks; 3) Increased infectiousness would be mainly due to increased transmission rate (based on data showing higher viral load) and a slightly longer infectious period (no data on this yet); 4) No changes in disease severity; and 5) No changes in interventions during the projection period.


#### 1/27/2021 Updates on model projections: 
Starting this week, based on more recent data, we adjust 1) the relative infectiousness of the new variant(s), from ~70% more infectious to ~50% comparied to the 'widetype' virus; and 2) the timing of new variant replacement, from 4 weeks to 6 weeks. Note that we have not yet adjusted the infection fatality risk (IFR); i.e. the same IFR is used for the 'New Variant' scenario.

#### 2/3/2021 Updates on model projections: 
Starting this week, our model projections also account for vaccination. For model training, observed vaccination rates by age and UHF are used as model input. For model projections where future vaccination rates are not available, we use projected estimates. We assume vaccine efficay (VE) 14 days after the first vaccine dose is 85% and after 7 days of the second dose is 95%. For more detail, see https://www.medrxiv.org/content/10.1101/2021.01.21.21250228v1

#### 2/10/2021 Updates on model projections: 
Starting this week, we use Model 1.6 (see above) for our projections. In addition to case and mortality data, the model is further trained on confirmed covid emergency department (ED) visit data. This likely allows more accurate estimates for younger age groups (those <45 years), for whom infection fatality risk is relatively low.   

Please also note that we are in the process of updating estimated seasonal trend for COVID. As such, please include both projections with and without seasonality for planning in the next few weeks. (update on 3/24/21 - problem resolved)

#### 2/24/2021 Caution on potential underestimation of hosptial bed and ventilator demands
Please note that our model has under-estimated in-patient counts and intubated patient counts in recent weeks (since the week starting 1/24), when compared to data from HERDS. We are investigating reasons for this under-estimation. Before we update the relevent parameters (e.g. duration of hospital stay), please take this into account when using our model projections related to hosptial bed demands and ventilator demands. 

update on 3/24/21 - problem resolved

#### 7/27/2021 Update on Projection Scenarios due to increased circulation of the Delta variant
From this week onwards, we update the No Control (i.e. Worst Case) scenario to reflect estimated parameters for the Delta variant.  In addition, we stop generating projections for the "New Variant" scenario, because as of the Week of 7/10/2021, the dominant variant in NYC has become the Delta variant.  

### References

China CDC. Vital Surveillances: The Epidemiological Characteristics of an Outbreak of 2019 Novel Coronavirus Diseases (COVID-19) — China, 2020, 2020, 2(8): 113-122 (http://weekly.chinacdc.cn:80/en/zcustom/volume/1/2020)

Li R, Pei S, Chen B, Song Y, Zhang T, Yang W, Shaman J. Substantial undocumented infection facilitates the rapid dissemination of novel coronavirus (COVID-19) Science 16 Mar 2020:
eabb3221. doi: 10.1126/science.abb3221

World Health Organization, Coronavirus disease (COVID-2019) situation reports, 2020. https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports/.

Yang  X, Yu  Y, Xu  J, Shu  H, Xia  J, Liu  H, et al. Clinical course and outcomes of critically ill patients with SARS-CoV-2 pneumonia in Wuhan, China: a single-centered, retrospective, observational study. Lancet Respir Med. 2020;S2213-2600(20)30079-5; Epub ahead of print.

Zhou F, Yu T, Du R, Fan G, Liu Y, Liu Z, Xiang J, Wang Y, Song B, Gu X, Guan L. Clinical course and risk factors for mortality of adult inpatients with COVID-19 in Wuhan, China: a retrospective cohort study. The Lancet. 2020 Mar 11.

Wang et al., Clinical Characteristics of 138 Hospitalized Patients With 2019 Novel Coronavirus–Infected Pneumonia in Wuhan, China - JAMA, February 7, 2020

Tang F, Quan Y, Xin ZT, et al. Lack of peripheral memory B cell responses in recovered patients with severe acute respiratory syndrome: a six-year follow-up study. J Immunol 2011; 186(12): 7264-8.

Polack FP, Thomas SJ, Kitchin N, Absalon J, Gurtman A, Lockhart S, Perez JL, Pérez Marc G, Moreira ED, Zerbini C, Bailey R, Swanson KA, Roychoudhury S, Koury K, Li P, Kalina WV, Cooper D, Frenck RW, Hammitt LL, Türeci Ö, Nell H, Schaefer A, Ünal S, Tresnan DB, Mather S, Dormitzer PR, Şahin U, Jansen KU, Gruber WC. Safety and Efficacy of the BNT162b2 mRNA Covid-19 Vaccine. New Engl J Med. 2020. doi: 10.1056/NEJMoa2034577.

Yang W, Kandula S, Huynh M, et al. Estimating the infection fatality risk of COVID-19 in New York City, March 1-May 16, 2020. medRxiv 2020: 2020.06.27.20141689. https://www.medrxiv.org/content/10.1101/2020.06.27.20141689v1

Yang W, Kandula S, Huynh M, Greene SK, Van Wye G, Li W, Chan HT, McGibbon E, Yeung A, Olson D, Fine A, Shaman J. Estimating the infection-fatality risk of SARS-CoV-2 in New York City during the spring 2020 pandemic wave: a model-based analysis. The Lancet Infectious Diseases. doi: 10.1016/S1473-3099(20)30769-6. https://www.thelancet.com/journals/laninf/article/PIIS1473-3099(20)30769-6/fulltext

Yang W, Kandula S, Shaman J. Simulating Epidemic Outcomes under Different Re-opening Policies. 5/26/2020. Available at https://github.com/wan-yang/re-opening_analysis/blob/master/report1_reopenTiming.pdf
 
Yang W, Shaff J, Shaman J. Effectiveness of non-pharmaceutical interventions to contain COVID-19: a case study of the 2020 spring pandemic wave in New York City. Journal of The Royal Society Interface. 2021;18(175):20200822. doi: doi:10.1098/rsif.2020.0822. https://royalsocietypublishing.org/doi/10.1098/rsif.2020.0822

Yang W, Kandula S, Shaman J. Simulating the impact of different vaccination policies on the COVID-19 pandemic in New York City. medRxiv. 2021:2021.01.21.21250228. doi: 10.1101/2021.01.21.21250228. https://www.medrxiv.org/content/10.1101/2021.01.21.21250228v1


