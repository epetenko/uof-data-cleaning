# Use of Force Data Cleaning
How we did the data cleaning for NJ.com's Use of Force project

## Background/what is this data?
In July 2017, the New Jersey Supreme Court ruled that police departments had to provide forms outlining their Use of Force when reporters or the public sent in records requests. To get the data for this project, NJ Advance Media sent OPRA (records) requests to every police department in New Jersey and got back every incident for the past five years in PDF documents. We sent those records to a contractor to peform the data entry processing while regularly checking their work.

After going through the process, we had 72,000 rows of data with roughly 30 columns each — not an unprecedented amount of data for the NJ.com data team, but one that required a lot of work to ensure we could accurately create many stories and a database without too much checking and re-checking. Thus, we decided to divide the data into three weeks of cleaning, one for each data reporter we had. After the reporter was finished, they would send their version of the data to the next reporter as well as a thorough explanation of what they did. Then we continued to adjust the dataset in the analysis process as we continued to attempt to refine our data to make it easier to analyze.

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
With major questions identified and settled, we turned to taking a closer look at the data. 
- Erin went over the criminal charges again, adding in more standardization to ensure that the vast majority of charges were standardized. 
- Steve identified duplicate forms by creating a unique key for each form, then lining up the data to find forms where all of the information was the same. 
- Erin added the second and third officers from a form to the main column of officers to ensure that those officers were on the same level of analysis as the first officer, then identified duplicates in the data again using Steve's method. 

More information about those processes are in steve_wk4readme, Second_third_officer_check.ipynb and UOF_data_cleaning_get_crime_data_from_disha.ipynb.

## Officer-involved shootings
After identifying a potential blind spot for fatal force cases in the data, we learned that the AG's office had previously provided to researchers 10 years' worth of forms similar to use of force reports known as "notifications of fatal force," which county prosecutors are required to provide to the attorney general any time an officer in their county fires his or her weapon. Those forms supplemented our dataset in a crucial area: instances in which an officer used fatal force, which we learned from sources did not always result in the completion of a standard use of force report because of some departments' policies regarding the rights of an officer under investigation.

Once we collected those forms from the AG's office, we put them into the Use of Force data using the same Google form that we used to put in the original documents.

## Part 2: The cleaning continues
Although we set aside more than a month devoted solely to data cleaning, we quickly discovered our work was not over just because we had begun analysis. As we set aside reporters to clean portions of the data, we saved old versions on a hard drive and passed around the hard drive with the latest version to continue our analysis.

### Nature of force
Disha standardized the nature of force used by going through the unique values and standardizing them to different terms, such as "Tackled to the ground" rather than "Escorted to the ground" and "Brought to the ground." She standardized any force used that appeared more than 5 unique times in the data. Erin helped to stitch the new standardized column back onto the rest of the database with the same method used for charges.

### Animals
Craig, Disha and Erin looked at rows where subjects were not named, firearms were not discharged, or the incident type included an animal term such as "deer" or "goose" or any animal Craig could think of. We took out any instance where a wild animal was euthanized, but left in any instance where a dog or pet attacked an officer, as we felt those still reflected a type of force that carried a human cost.

### EDPs
EDP stands for "Emotionally Distressed Persons," used broadly for any subject with a mental illness, mental health issue or disability that affected his/her interaction with officers. Erin created a dataset of all unique incident types, and Craig went through that dataset and added a label in another column if the incident type included keywords that indicated an EDP incident, such as "Suicidal," "Mental," "Psych," or "PESS," which is the organization that often responds to a scene to take an EDP to the hospital. Then Erin added a column to the data that labeled whether or not the case was EDP.

### Officer names, again
Carla went through the entire officer list of more than 20,000 officers and sorted it by county, police department, and created an alphabetical list of all officers. Then she went through and selected officers that appeared to be listed twice in error, either because of middle names, nicknames, misspellings or another reason. She created a Google spreadsheet with those 4,000-plus selected names, and the entire team, particularly Steve, cross-checked the names against the New Jersey pension database and retired pension database and made sure there was only one officer of that name in a department.
