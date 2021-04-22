# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Reading csv file from server
3. Generating pdf report based on analysis
4. Sending notification when report is available


### Mark the System Boundary

What is included in the software unit-test? What is not? 

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No			      | We do not test the PDF report generation (Mocked)
Computation of minimum 		  | Yes			      | Part of the analysis that needs to be done on csv file
Counting the breaches       | Yes			      | Part of analysis that needs to be done on csv file
Detecting trends            | Yes			      | Part of analysis that needs to be done on csv file
Notification utility        | Yes		      	| Email to be sent if report is available (Mocked)


### List the Test Cases

Template -> `<expected output or action>` from `<input>` / when `<event>`

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Count the number of breaches from a csv containing positive and negative readings and write to pdf 
4. Identify trends from the csv data to find date and time about when it was increasing for more than 30 mins and write to pdf
5. Send email notification if report is available after analysis
6. Do not email send notification if report is not available after analysis



### Recognize Fakes and Reality

| Functionality            | Input        				    | Output                      | Faked/mocked part
|--------------------------|--------------------------|-----------------------------|---
Read input from server     | csv file     				    | internal data-structure     | Fake the server store
Validate input             | csv data     				    | valid / invalid             | None - it's a pure function
Notify report availability | email ids to notify   	 	| None						            | Fake email sending part
Report inaccessible server | server path of csv file 	| true /false                 | Fake the server path						
Find minimum 			         |internal data-structure		| minimum value               | None, its a pure function
Find maximum 			         |internal data-structure		| maximum value               | None, its a pure function
Detect trend               |internal data-structure		| date and time value         | None, its a pure function
Write to PDF               |analysis output				    | None				                | Fake the pdf generator	
