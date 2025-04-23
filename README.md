# PUBH8472_DV_Mapping
PUBH8472 Project 2 - Modeling DV Exposure in the Gambia

Files Included:

Master R File - includes processing and Analysis:
  PUBH8472_Proj2.R

Also available as an Rmd file (I like to run things in chunks so also generated this)
  PUBH8472_Proj2.Rmd

Final Report:

  PUBH8472 - Project 2 Report.pdf

Gambia Data:

  The 2019 Gambia data downloaded from IPUMS-DHS is gambia_data/idhs_00032.csv
  Processing code and instructions are as included in PUBH8472_Proj2.Rmd
  Relevant variables are described at the bottom of this file.

Gambia Shapefiles:

    The 2019 Gambia shapefiles are located in gambia_data/shps
    Source: DHS Spatial Repository
    Processing code and instructions are included as part of PUBH8472_Proj2.R

Senegal Data:

  The 2019 Senegal data downloaded from The DHS Program (originally downloaded, now archived on IPUMS servers located at the University of Minnesota because Trump cronies might delete data, basically, as of now still available on DHS Program website, but new permissions aren't granted at the moment). 
  Located at senegal_data/SNIR8BFL.DTA.zip
  Warning this file is large! This is the full raw data file. It's not yet live on IPUMS-DHS, so there's no handpicked selection of variable available like for the Gambia. Processing steps are in PUBH8472_Proj2.R
  There is no full description of every single variable in this file, but variables relevant for the analysis are described below. 

Senegal Shapefiles:

  Located in senegal_data/senegal_boundaries_spa/shps
  These are technically the shapefiles from the 2019 SPA survey since the ones on the DHS Spatial Repository didn't match the regions in the region variable (v101) for Senegal 2019 DHS survey.

Variables Used in the Analysis or for Developing Variables/Indicators are listed below, in the following format:

Analysis_Var_Name - IPUMS_DHS_Varname (Gambia) / DHS_Program_Varname (Senegal)
       Regional_Aggregate_Level_Description_Here

Please note all variables have been aggregated to region level.

Further individual-level variable descriptions can be found atidhsdata.org/idhs/ by searching for either the the IPUMS_DHS_Varname or the DHS_Program_Varname

1. weight_scale - DVWEIGHT / d005
     A weighting factor for the subset of women  randomly selected and interviewed in privacy for the DHS domestic violence module. 
     The IPUMS-DHS variable does NOT need to be divided by 1e6 (see IPUMS-DHS weighting guidelines (https://www.idhsdata.org/idhs-action/variables/DVWEIGHT#description_section or https://www.idhsdata.org/idhs-action/variables/PERWEIGHT#description_section)
    The variable downloaded directly from The DHS Program for Senegal DOES need to be divided by 1e6. 

2. any_dv - NA / NA 
   An indicator variable where 1 means a woman said yes to either DVPMSEVER & DVPLSEVER or d106/d107 measuring 
   Indicates ever experiencing less severe or more severe violence from a partner

3. total_dv - NA / NA
   sum(any_dv * weight_scale)
   Used for calculating weighted DV incidence. Weighted total # of women who experienced physical IPV

4. total_pop - NA/ NA
   sum(weight_scale)
   Total weighted population count for women included in the DV module.

5. expected - NA / NA

  Expected incidence of physical IPV in a region

6. smr - NA / NA

   SMR for a region (observed/expected)

7. weight_total - NA / NA

   weights aggregated by region

8. working_percent - CURRWORK/v714

   Mean regional percetage of women who work

9. GEO_GM2013_2019 - GEO_GM2013_2019 / N/A

   Variable indicating local governmental areas denoting regions in Gambia
   Region names are in the final DF (dv_combined$DHSREGEN)

10. v101 - N/A / v101
    Variable indicating local governmental areas denoting regions in Senegal
    Region names are in the final DF as (dv_combined$DHSREGEN)

12. mean_wealth_quantile - WEALTHQ/v190
    Mean household wealth index in quintiles (Poorest/Poorer/Middle/Richer/Richest)
    NOT centered

13. mean_educlvl - EDUCLVL / v106
    Mean women's education level in a region (0 = No education, 1 = Primary, 2 = Secondary, 3 = Higher)

14. mean_hused - HUSEDLVL/v701
    Mean education level of women's husbands in a region

15. news_percent - NEWSFQ / v157
    Mean percent of women who read newspapers

16. tv_percent - TVFQ / v159
    Proportion of women who watch tv

17. radio_percent - RADIOFQ / v158
    Proportion of women who listen to the radio
  
18. internet_percent - INTERNETEVYR / v171a
  Proportion of women who use the internet

19. urban_percent - URBAN / v025
  Proportion of women living in urban vs. rural areas
  
20. mean_agefrstmar - AGEFRSTMAR / v511
  Mean age of first marriage

21. autonomy_score - N/A / N/A
  A composite variable indicating mean women's autonomy in decision making, with a 1 indicating woman has some or all the say in the decision making process. The Gambia variable includes decision making in visits to family (DECFAMVISIT), large household purchases (DECBIGHH), how her earnings are spent (DECFEMEARN), how her husband's earnings are spent (DECHUSEARN), and her own healthcare (DECFEMHCARE).
  The Senegal variable includes all these variables except for DECFEMEARN. DECFAMVISIT = v743d, DECBIGHH = v743b, DECHUSEARN = v743f, DECFEMHCARE = v743a

23. mean_age - AGE / v012
  Mean women's age

24. mean_husage - HUSAGE / v730
  Mean husband's age
  
25. mean_age_gap - N/A / N/A
  Mean age gap between a woman and her husband. Calculated as husband's age - woman's age, so positive = husband older, negative = woman older

26. pct_pahitma - DVPAHITMA / d121 
    Proportion of women who saw their fathers hit their mothers.

27. mean_dv_approve - N/A / N/A
  A composite variable indicating mean women's approval of domestic violence in a variety of situations, and ranges from 0 to 1. 1 indicates supporting a man beating his wife in all included scenarios. For Gambia, the scenarios include if she disrespects her in-laws (DVADISINLAW), if she uses contraception without consent (DVAUSEFP), if she neglects the children (DVANEGKID), if she refuses to have sex (DVAIFNOSEX), if she goes out without permission (DVAGOOUT), if she burns food (DVABURNFOOD), and if she argues with her husband (DVAARGUE). 
  For Senegal, all variables were included except for if she uses contraception without consent and if she disrespects her in-laws. DVANEGKID = v744b, DVAIFNOSEX = v744d, DVAGOOUT = v744a, DVABURNFOOD = v744e, DVAARGUE = v744c.

29. mean_wealth_work_int - N/A / N/A
    Interaction between wealth quintile and working status, calculated using a centered wealth_quintile multiplied by women's working status
    
31. dv_inter_percent
  Composite variable indicating interruption during the private DV interview. Includes variable indicating whether the woman was interrupted by her husband, other women, or other men. For Gambia, these variables are DVINTERRHUS, DVINTERRFEM, DVINTERRMALE. For Senegal, these variables are d122a, d122b, d122c
