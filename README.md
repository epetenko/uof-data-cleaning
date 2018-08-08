# Use of Force Data Cleaning
How we did the data cleaning for NJ.com's Use of Force project

## Background/what is this data?
In July 2017, the New Jersey Supreme Court ruled that police departments had to provide forms outlining their Use of Force when reporters or the public sent in records requests. To get the data for this project, NJ Advance Media sent OPRA (records) requests to every police department in New Jersey and got back every incident for the past five years in PDF documents. We sent those records to a contractor to peform the data entry processing while regularly checking their work.

After going through the process, we had 72,000 rows of data with roughly 30 columns each — not an unprecedented amount of data for the NJ.com data team, but one that required a lot of work to ensure we could accurately create many stories and a database without too much checking and re-checking. Thus, we decided to divide the data into three weeks of cleaning, one for each data reporter we had. After the reporter was finished, they would send their version of the data to the next reporter as well as a thorough explanation of what they did.

## Week 1

Most of the data analysis for the first week is in the Jupyter notebook in the files of this Github and performed with Python and Pandas. But a few fields were too difficult to process with Pandas, necessitating some work in the csv files and the explanations below.

### How we cleaned race data
_Erin Petenko_

The initial dataset recorded race/ethnicity exactly as it was written in the form, to ensure we captured all the raw data before delving into standardization and simplification. This meant that when the raw data was finished, there were 300+ different entries for race, too many to efficiently analyze the top categories. Another complication was Hispanic/Latino ethnicity. Some forms reported it as a separate category from race, recording subjects as "White Hispanic" or "Black Hispanic", while others reported simply "Hispanic."

To assist with this process, we created a spreadsheet that included all reported racial categories and set about manually choosing the standardized version of those entries. We relied on the New Jersey State Police racial classification system for the departments that used it. Several reporters cross-checked the data coding. We labeled ambiguous entries as "ND", or not determinable. In addition, we created optional columns that separated race and ethnicity, for entries that included both. In the end, 1.1 percent of officers and 2.3 percent of subjects had both race and Hispanic origin recorded.

#### The final racial classifications:

- WHITE: When the officer or subject was labeled as White or Caucasian.
- BLACK: When the entry was Black or African-American.
- HISPANIC: When the entry was Hispanic, Latino or Spanish. While we understand those labels may have slightly different meanings, we believed that few police departments made a distinction between the terms.
- NONHISPANIC: In the instances where ethnicity and race were both specified, and the person was labeled as not Hispanic.
- ASIAN: When the entry was Asian, South Asian, or Oriental.
- PACIFIC ISLANDER: When the entry was Native Hawaiian or Pacific Islander.
- ASIAN/PACIFIC ISLANDER: When the entry was recorded as Asian/Pacific Islander -- i.e., when the person recording race put both rather than choosing one or the other.
- NATIVE AMERICAN: When the entry was Native American, American Indian or Alaskan Native.
- OTHER: When the racial entry was a racial category that did not fit cleanly into one of the above races, particularly with Middle Eastern or North African.
- MIXED: When the entry indicated "Mixed" or recorded two distinct races, such as "White/Black."
- UNKNOWN: When the entry indicated that the race of the officer or subject was unknown.
- ND: Not determinable - When the entry was unclear, either because of poor abbreviations or unclear terminology. This includes any entry that defined race by the country of origin, such as "Ecuador," or by the religious affliation of the person. It also included obvious mistakes such as entering the gender of the person or their rank instead of their race. In all, roughly 0.4 percent of subjects and 0.2 percent of officers were coded as ND.
- DEER: When the person was not a person but actually a deer.

#### One more caveat

Race and ethnicity are in the eyes of the beholder, and in this case, the beholder was the officer writing the form. That officer makes an assumption about what the subject's race/ethnicity — based on appearance, behavior, or whatever else — that may be wildly different from the subject's own opinion on the matter. So tread with caution when it comes to how you phrase your reporting on this data.

### Criminal charges data

_Erin Petenko_

Again, the raw data contained exactly what officers wrote, leaving more than 10,000 unique charge names . To clean this, I separated the charges along commas and downloaded a copy of all unique charges in the data. I used OpenRefine's merge and cluster function to review and combine charges that were the same but had minor typos, such as "Ressiting" rather than "Resisting." Then reporter Craig McCarthy and I went through the charges that had more than 5 entries and standardized charge codes to names describing the charge. We retained the entries for each step of the process, iteratively reviewing our entries and re-classifying them. I then added the standardized charges back to the separated raw data, and combined them into one column again, again retaining the raw data in the spreadsheet in case we need to go back to it.

## Week 2
Most of this week centered around cleaning officer names. Steve Stirling created a new column merging first name, last name and the town of the officer for a unique ID. Then he zoomed in, using OpenRefine to cluster and merge, identifying officers who used slightly different capitalization or identification for different forms. The exact process of filtering and cleaning is the the file Week_2_readme.rtf.

## Week 3
Disha Raychaudhuri worked on the file for week 3, focusing on cleaning and standardizing badge names. We then tackled identifying individual officers -- for example, is John Smith, badge number 1234, the same person as John Smith, 1235, or are there two people with that name in one department? We used pension records to find officers in those instances. The exact process is outlined in disha_wk3readme.rtf.

## Weeks 4&5
With major questions identified and settled, we turned to taking a closer look at the data. Steve 
