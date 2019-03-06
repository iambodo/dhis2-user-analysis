# dhis2-user-analysis
RMarkdown script to pull and analyze user activity data from *any DHIS2 Tracker program*

DHIS2 does not have user-level analytics. Instead, DHIS2 analytics is constrained to period dimension, organization unit dimension, and a data dimension such as a data element or program indicator.

DHIS2 analytics therefore assumes that one user is active per organization unit. However, there are often multiple users working at a single organization unit, such as at a health clinic, making it impossible to know which user is entering data and when.

However, DHIS2 keeps a log of every entry of a data element into a tracker program at the */trackedentitydatavalueaudit* API endpoint, including username and timestamp, making it possible to analyze tracker data entry at the **user level**.

After you enter database and credential details, the routine checks if a SQL view based on "trackedentitydatavalueaudit" table is in the database. If not, it POSTS and executes the SQL view.

The next routine pulls data from the SQL view and performs various analysis routines:
--Total users with accounts, users with activity, users who entered tracker data
--Top stages by number of user interactions
--Analysis of user interactions, aggregated for each user group, by stage and hour 
--Analysis of user interactions for each indivdual user, by stage and by hour

Analysis for **each USER GROUP and each USER** is outputted to the working directory as separate PNG files. Thus, execution of the script may take some time, depending on the size of your DHIS2 instance.

When executing Knitr, the resulting output is a summary of the analyses performed.
(RStudio recommended to use Knitr.)

NB: This is my first RMarkdown project, so the code is inelegant and likely inefficient. Suggestions for improvements are welcome!

Possible improvements:
-Analysis by day of the week
-User-level data on tracked entity attribute and enrollments
-Combining with user-level interpretations and aggregate dataset interactions
-Extracting teidva data on "sessions", or time to complete stage by each user
-Create new sub-directories for analysis date, user graphics, and user group graphics, for better file structure.

Example graphics below.
![alt examples](https://raw.githubusercontent.com/iambodo/dhis2-user-analysis/master/example_graphics.JPG)
