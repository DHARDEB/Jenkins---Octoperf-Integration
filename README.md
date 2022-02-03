# Jenkins_Octoperf_Integration to automatically schedule routine performance tests via Jenkins

What is Octoperf? 

Octoperf is like Blazemeter which offers test environment where you can upload jmx files & design performance scenarios & execute/analyze test results. 

Idea: To schedule tests using Jenkins so that the daily scheduled tests can be automatically triggered every day, removing the process of manually running it from Octoperf.

Problem Statement: Everyday, PE team needs to manually run two token creation test from Octoperf .

Implementation Status: Implemented for automatically running Token creation test every day at 11:05 AM IST.

**Steps to be followed:**

Preconditions:

1.	Configure & create a Jenkins account.

2.	Install the Jenkins-Octoperf Plugin & update Jenkins if required. From here : https://wiki.jenkins-ci.org/display/JENKINS/OctoPerf+Plugin

Steps:

1.	In the manage credentials section of Jenkins, sign in with your Octoperf Credentials.

2.	Create a New Project, in build triggers>>Build Periodically give the appropriate CRON expression for running the test automatically every day.

 	Format of CRON expression to be given in triggers:

 	Jenkins used a CRON expression, & the different fields are:

 	A. MINUTES Minutes in one hour (0-59)

 	B. HOURS Hours in one day (0-23)

 	C. DAYMONTH Day in a month (1-31)

 	D. MONTH Month in a year (1-12)

 	E. DAYWEEK Day of the week (0-7) where 0 & 7 are Sunday

If you want to schedule your build every 5 minutes, this will do the job : */5 * * * *

If you want to schedule your build every day at 8h00, this will do the job : 0 8 * * *
 

3.	Now, in the build section, map the scenario from Octoperf which you want to run automatically. You can add multiple scenarios, or a single scenario based on your requirement.

4.	In the Post- build actions, select the project you want to run after the current project is complete. For example, say we have Scenario 1 & Scenario 2, Scenario 2 needs to be run only after scenario 1 is successful. Then, in the post-build actions section of scenario 1 , select scenario 2 to be executed after scenario 1 is successful.

5.	Click apply & save.

JUnit Reporting:

The Jenkins plugin generates & stores a JUnit report at the end of the test in the file junit-report.xml. This is especially useful if the build should be marked as unstable or failed when errors or assertion failures are encountered during the test run.

Source: https://doc.octoperf.com/integrations/ci/jenkins/

