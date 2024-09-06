# module1-codexes-claims-analysis

# I put into the Google Colab notebook a lot of my notes as I went along using ## to parce them out from the coding.
# First, I installed pandas and uploaded the link to the CSV of the inpatient data into Google Colab
# Then I played around with different views of the columns in the data
# Then I tried to figure out which 8 unique codes I was going to use to pull data from, but I found a lot of duds in the beginning so it took me a while to figure out which ones to search in. 
# I then ran each code one at a time, to make sure it had some data I could use. 
I excluded some because #several NaN in the beginning, very different IDs in the end.
# I tried to identify ICD codes as data, but kept getting error codes. (I tried this again later after naming them the ICD specific code I was using, and still received an error message)
# Then I started again, with my 8 unique codes:
# CLM_ID
# CLM_UTLZTN_DAY_CNT
# CLM_FROM_DT
# CLM_PMT_AMT
# CLM_TOT_CHRG_AMT
# PRNCPAL_DGNS_CD
# ICD_DGNS_CD1
# HCPCS_CD
# I ran them using df.
# then did the count using count = df.CLM_ID.unique()
# len(count)
# then tested the value counts with df['CLM_ID'].value_counts()
# Then ran the describe code and added additional notes about the code from the data dictionary
# df['CLM_ID'].describe()
## instead of .value, use .describe to give us the descriptive statistics for a particular column
## count is the number of rows it's using to generate these descriptive stats
# CLM_ID label means Claim ID
# This is the unique identification number for the claim
# Type: CHAR
# There are 20867 unique Claim ID numbers in the data set
I did the above steps for all 8 codes
I tried the ICD data codes again, this time trying to label them with the names of my specific ICD code used in this colab, but I kept getting errors
Thanks to a classmate's help, I ran the code for the codex_columns
codex_colums = ['CLM_ID',
                'CLM_UTLZTN_DAY_CNT',
                'CLM_FROM_DT',
                'CLM_PMT_AMT',
                'CLM_TOT_CHRG_AMT',
                'PRNCPAL_DGNS_CD',
                'ICD_DGNS_CD1',
                'HCPCS_CD' ,
]
for column in codex_colums:
    print(f"Frequency counts for {column}:")
    print(df[column].value_counts())
    print("\n")
    This gave us the top 5 most frequent outputs for each of the 8 unique datasets.
    For CLM_ID the most common IDs were 
    -10000930775141    46
-10000930521375    34
-10000930487748    34
-10000931409722    32
-10000931016403    30
I was unable to find a website that could make sense of these claim numbers. I kept getting back to the resdac.org website, but when I tried to click for inpatient claim ID numbers it kept looping me back to the same webpage.
CLM_UtLZTN_DAY_CNT was for number of days, so the top 5 most common were 0, 1, 2, 4, 5 days
Frequency counts for CLM_FROM_DT:
CLM_FROM_DT
09-Jan-2021    101
29-Oct-2022     88
15-Jan-2023     80
20-Jan-2021     79
02-Mar-2022     74
These were the 5 most common days for the CLM_FROM-DT (above)

Frequency counts for CLM_PMT_AMT:
CLM_PMT_AMT
950.31      529
166.97      525
1140.09     524
1358.56     473
108.86      463

These were the 5 most common payment aounts for CLM_PMT_AMT (above)

Frequency counts for PRNCPAL_DGNS_CD:
PRNCPAL_DGNS_CD
Z733      11469
Z608       7216
T7432X     3314
Z604       3227
Z7682      3092

These were the 5 most common diagnosis codes, which indicated:
Z733 - stress that is not classified elsewhere
Z608 - indicates other problems related to social environment, such as inadequate social support or a lack of emotional support
T7432X - child physchological abuse, confirmed, subsequent encounter
Z604 - social exclusion and rejected based on personal characteristics such as unusual physical appearance, behavior, and social isolation
Z7682 - awaiting organ transplant status

While the high number of diagnosis codes involving stress or social-related problems seemed to coincide with the general public's views on healthcare and mental health these days, I was shocked and saddened to see that subsequent encoutners of child psychological abuse was ranked third most common. I was also surprised to see awaiting organ transplant to be in the top 5. I don't know what I was expecting aside from mental health, but it definitely wasn't that. 

Frequency counts for HCPCS_CD:
HCPCS_CD
99221    8298 - initial hospital inpatient or observation care for patients with low complexity conditions
G0444    7990 - annual depression screening that takes up to 15 minutes
96156    5080 - used to report health behavior assessment and reassessment services
99408    4196 - indicates medical providers performed a 15-30 minute structured screening and brief intervention for alcohol or substance abuse
99495    3867 - reports transitional care management (TCM) services for patients who require moderate medical decision making, includes a face to face office visit within 14 days of discharge

It makes sense that the most common HCPCS code is for conditions that are straightforward medical decisions. The second is for the annual depression screening, sounds like the questions asked at a patient's annual physical exam. 

The most interesting datasets were my last two, I was dismayed that I had such trouble finding datasets with more codes such as these to use for my analysis. 

When trying to find which unique codes to look up, a lot of my ICD codes had 0 data points. I spent a lot of time looking for codes with various data points, and spent a lot of time asking for help to make sure I was on the right track. After reviewing the zoom recorded class, and the 3 github links, I had a little more direction, and then thanks to a classmate I was able to run the code for the top 5 most frequent data points. 

While a lot of my searches were about dollar amounts, dates, and number of items, the last 2 sections were the most interesting, with healthcare codes that gave some insight into the most common inpatient visits. It is sad to see how many interventions are needed for alcohol and substance abuse, coinsiding with stress, emotional, and psychological problems which in a way connect the last two datasets.
