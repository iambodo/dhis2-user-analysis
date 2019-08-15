# dhis2-user-analysis
RMarkdown script to pull and analyze user activity data from *any DHIS2 Tracker program*

DHIS2 does not have user-level analytics. Instead, DHIS2 analytics is constrained to period dimension, organization unit dimension, and a data dimension such as a data element or program indicator.

DHIS2 analytics therefore assumes that one user is active per organization unit. However, there are often multiple users working at a single organization unit, such as at a health clinic, making it impossible to know which user is entering data and when.

DHIS2 keeps a log of every entry of a data element into a tracker program at the */trackedentitydatavalueaudit* API endpoint, including username and timestamp, making it possible to analyze tracker activity at the **user level**.

After downloading packages, you enter database URL and credential details, plus parameters for your analysis.

The next routine pulls data from the SQL view and performs various analysis routines:
* Total users with accounts, users with activity, users who entered tracker data
* Top stages by number of user interactions
* Analysis of user interactions, aggregated for each user group, by stage and hour 
* Analysis of user interactions for each indivdual user, by stage and by hour
* Percent of interactions within "work hours" for user groups and users
* Day of week and time of day charts
* Session duration (time between first and last change user made on stage)

Analysis for **each USER GROUP and each USER** is outputted to the working directory as separate PNG files. Thus, execution of the script may take some time, depending on the size of your DHIS2 instance.

When executing Knitr, the resulting output is a summary of the analyses performed.
(RStudio recommended to use Knitr.)

Future possible improvements
* User-level data on tracked entity attribute and enrollments
* Combining with user-level interpretations and aggregate dataset interactions

Example graphics below.
![alt examples](https://raw.githubusercontent.com/iambodo/dhis2-user-analysis/master/example_graphics.JPG)
