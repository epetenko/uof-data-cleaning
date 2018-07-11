# uof-data-cleaning
Use of force data cleaning process


## How we cleaned race data

The initial dataset recorded race/ethnicity exactly as it was written in the form, to ensure we captured all the raw data before delving into standardization and simplification. This meant that when the raw data was finished, there were 300+ different entries for race, too many to efficiently analyze the top categories. Another complication was Hispanic/Latino ethnicity. Some forms reported it as a separate category from race, recording subjects as "White Hispanic" or "Black Hispanic", while others reported simply "Hispanic."

To assist with this process, we created a spreadsheet that included all reported racial categories and set about manually choosing the standardized version of those entries. We relied on the New Jersey State Police racial classification system for the departments that used it. Several reporters cross-checked the data coding. We labeled ambiguous entries as "ND", or not determinable. In addition, we created optional columns that separated race and ethnicity, for entries that included both.

Here were the final racial classifications:

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


