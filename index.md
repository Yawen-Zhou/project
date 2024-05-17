# Project
# Self-Reported Health
## 1. Data Acquisition and Preparation:
- ### Survey Data:
  - Import the survey data from the [1999-2000 National Health and Nutrition Examination Survey (NHANES)](https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT):
     ```stata
     import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
     ```
- ### Mortality Follow-up Data:
   - Obtain follow-up mortality data to analyze over a 20-year period from the [National Center for Health Statistics (NCHS)](https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/NHANES_1999_2000_MORT_2019_PUBLIC.dat).
     ```stata
     //data
     global mort_1999_2000 https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/NHANES_1999_2000_MORT_2019_PUBLIC.dat

     //code
     cat https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/Stata_ReadInProgramAllSurveys.do
     ```
     
## 2. Code Development:
- ### Edit and Rename Provided Script:
   - Download, modify, and upload the [Stata_ReadInProgramAllSurveys.do](https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/Stata_ReadInProgramAllSurveys.do) file for linking the DEMO.XPT data to mortality follow-up data. Rename this file to ```followup.do``` and commit it with the description: “Updated DEMO.XPT linkage .do file”. Remember to edit the hardcoded filepath.
- ### Data Merging:
   - Merge the survey data with the mortality data, ensuring alignment on the unique sequence numbers:
      ```stata
      //use your own username/project repo instead of the class repo below
      global repo "https://github.com/jhustata/intermediate/raw/main/"
      do ${repo}followup.do
      save followup, replace 
      import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
      merge 1:1 seqn using followup
      lookfor follow
      ```
      
## 3. Key Parameters for Week 7s Analysis:
- ### Self-Reported Health Assessment:
   - Import the specific health questionnaire data and prepare it for analysis in Week 7:
      ```stata
      import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/HUQ.XPT", clear
      ```
      
## 4. Inferences
- Please review [documentation](https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/HUQ.htm) for the file ```HUQ.XPT```, which includes the variable ```huq010```
- Employ 95%CI and p-values
- Write a brief abstract-style conclusion
- Code for reference:
   - code 1
      ```stata
      merge 1:1 seqn using demo_mortality, nogen
      sts graph, by(huq010) fail
      stcox i.huq010
      ```   
   - code 2
      ```stata
      import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/HUQ.XPT", clear 
      huq010 
      desc huq010
      codebook huq010
      ```

## 5. Results of survival analysis_week 7
- Please click [here](dyndoc.html) to see the results
