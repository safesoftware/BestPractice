# Best Practice Audit #

Suggestions and reports still to do.

## Report Structure ##

Ways to improve the layout and structure of the HTML report

- Improve the style of the HTML
- Check whether 'Custom HTML' can now replace some aspects of the 2016.1 implementation
- Include a list of links to the subsections either before or immediately after the header to facilitate navigation
	- This needs a way to set an ID in a header. Either custom HTML or FME update (Filed PR#77044)

## Report 1: Header ##

Suggestions and updates for the report header


## Report 2: Workspace ##

Suggestions and updates for the Workspace report

- Check for a workspace devoid of content (ie no readers, no writers, no transformers): ERROR
- Check how long it takes to open the project/file size - or some other metric to indicate that the project is too large
- Add a section that checks for startup and shutdown scripts.
- Check for embedded database connections as a security issue - readers, writers, transformers
	- Currently we can't tell in the FMW reader what is a db connection and which is embedded


## Report 3: STYLE ##

Suggestions and updates for the Style report

- If we knew the position of objects we might identify crossing connections (unlikely, but hey)

## Report 4: BREAKPOINTS ##

Suggestions and updates for the Breakpoints report

## Report 5: READERS ##

Suggestions and updates for the Readers report

- Give a warning if Readers/Reader FTs are not connected (possible in 2017?)
- If we knew what connections exist (this might now be possible in 2017) then test for all Reader FT's connected to same transformer - in which case a merge filter could be used
- Information or warning where it would be possible to implement a where clause on a reader (for instance if there's a tester right after a reader).
- Test connections to databases and file locations using the information in the workspace


## Report 6: WRITERS ##

Suggestions and updates for the Writers report

## Report 7: Transformers ##

Suggestions and updates for the Transformers report

- List the most-used transformer category
	- This would need a lookup table from transformer<->category, since category is not returned by the FMW reader
- 	Where parameters are set to an attribute value, warn to include error checking to ensure the attribute exists
	- Currently we can't tell if a parameter is set to an attribute value (or whether it is a fixed string)
- Check the possibility of losing features / lack of error trapping. For instance if there exists a tester with a connection only to the Passed port
- Check groupings (ie common sections of transformers) eg to say "this should be a custom transformer"
- Test if transformer names have been changed (if not, could not be best practice?) Or check where there is a long series of _1, _2, _3, _4, etc on transformer names
- Ping URLs used in a HTTPCaller to see if they respond


## Report 8: PERFORMANCE ##

Suggestions and updates for the Performance report

## Report 9999: SUMMARY ##

Suggestions and updates for the report summary

- Report the number of tests carried out
	- Maybe add published parameters for the user to select which tests to carry out
	- Report the number of tests, number of passes, number of Warnings, number of fails, number of N/A (eg no readers).
- Create a quality report
	- Maybe score the workspace as (objects/((errors*2)+(warnings)))?
	- Maybe if any errors exist, the workspace fails (should not be put into production)
	- If WARNs only then it can be put into production, but not without first confirming these warnings are not a problem.
	- If PASSes only then it can be put into production. Well done.
- Report the time taken to process the workspace
- Report the number of readers, writers, transformers


## New Reports or Projects ##

### Screenshotting ###

Can we somehow open a workspace and screenshot it? That way we could add screenshots to the report

### Log File Analysis ###

Analyze a log file to look for best practice issues.

- Look for time discrepancies
- Look for low memory or disk space
- Look for temp folder on same drive as operating system
- Look for warnings and errors

### Template Analysis ###

The ability to submit a template, have it run, and analyze the log file (maybe use as a benchmark??)
