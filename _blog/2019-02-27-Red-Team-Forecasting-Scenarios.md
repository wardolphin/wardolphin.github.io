---
layout: post
title: Red Team Forecast Scenarios
---
These are the forecast scenarios that I used internally at Atlassian to measure our security improvement over time. The inputs to concluding many of these forecasts come directly from the red team. This allows a quantifiable and measurable method of taking red team operation outputs and using them to show improvements in the security program. This demonstrates real value!

This is based on [@magoo's] (https://twitter.com/magoo) work on [Risk Measurement](https://magoo.github.io/simple-risk/). 

Forecasters make predictions every quarter predicting the likelihood of the events occuring in the next 12 months. Whenever a forecast concludes by one of the outcomes becoming “true” we calculate the forecasters [brier scores] (https://www.gjopen.com/faq), inform them of the outcome of the scenario and present them their results and brier score. 

Each scenario also implies that the scenario will only conclude if the red team attempts the action in question. Don’t score scenarios that were never attempted because it will affect brier scores. All of these are starter scenarios and shouldn’t be copypasta to your organization. You should adapt the questions and outcomes to the needs and goals that you are trying to achieve.
 
For each scenario there are several provided outcomes. Each outcome should be given a probability. The probabilities must add up to 100. 

For additional reading on how to get started, [this page] (https://magoo.github.io/simple-risk-analysis/) is helpful.

## Scenario 1- compromised computer
In the next 12 months, during the course of a red team operation, the red team:
* compromised one or more employee assigned computers
* did not compromise any employee computers. 

## Scenario 1 - Detection
In the next 12 months, an employee computer was compromised by the red team, and:
* the security team detected the compromise in less than 66 hours.
* the security team detected the compromise more than 66 hours after compromise 
* the security team did not detect it, it was detected after 7 days or  red team intentionally triggered detection.

## Scenario 2 - Employee Corporate Account Compromise
In the next 12 months, during the course of a red team operation, the red team
* gained control of one or more employees corporate accounts.
* did not gain control of any employees corporate accounts.

## Scenario 2 - Detection
In the next 12 months, during the course of a red team operation, the red team gained control of one or more atlassian employees corporate accounts and
* it was detected in less than 66 hours.
* it was detected after 66 hours 
* it was not detected, it was detected after 7 days or red team intentionally triggered detection.

## Scenario 3 - Customer Data Compromise
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team
* accessed customer data stored in our products. 
* did not access customer data stored in our products. 

## Scenario 3 - Detection
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team accessed customer data stored in our products and
* it was detected in less than 66 hours. 
* it was detected after 66 hours
* it was not detected, was detected after 7 days or the red team intentionally triggered detection.

## Scenario 4 - Cloud Infrastructure Compromise
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team
* will gain unauthorized access to AWS resources owned by $COMPANY. 
* will not gain unauthorized access to AWS resources owned by $COMPANY. 

## Scenario 4 - Detection
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team gained unauthorized access to AWS resources owned by $COMPANY and
* it was detected in less than 66 hours. 
* it was detected after 66 hours 
* it was detected after 7 days, not detected or the  red team intentionally triggered detection.

## Scenario 5 - Trust Boundary Violation
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team
* will compromise differing systems across significant trust boundaries
* will not compromise differing systems across significant trust boundaries

##Scenario 5 - Detection
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, a compromise across significant trust boundaries*
* was detected in less than 66 hours. 
* was detected after 66 hours 
* the security team did not detect it, it was detected after 7 days or  red team intentionally triggered detection.

##Scenario 6 - Source Code Compromise
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team
* accessed full source code of one or more $COMPANY products. 
* did not access source code of one or more $COMPANY products. 

## Scenario 6 - Detection
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team accessed full source code of one or more $COMPANY products and
* it was detected in less than 66 hours. 
* it was detected after 66 hours and in less than 7 days (without red team intentionally triggering detection). 
* the security team did not detect it, it was detected after 7 days or  red team intentionally triggered detection.

## Scenario 7 - Confidential Information Stolen
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team
* accessed information that could be greatly damaging to $COMPANY if released publicly
* did not access information that could be greatly damaging to $COMPANY if released publicly

## Scenario 7 - Detection
Given that an employee laptop is compromised: In the next 12 months, during the course of a red team operation, the red team accessed information that could be greatly damaging to $COMPANY if released publicly and
* it was detected in less than 66 hours. 
* it was detected after 66 hours and in less than 7 days (without red team intentionally triggering detection). 
the security team did not detect it, it was detected after 7 days or  red team intentionally triggered detection.

##Scenario 8 - Production Detection
Given a red team compromise on a randomized engineer laptop: The red team
* will observe production customer data in less than two weeks without detection. 
* will not observe production customer data or will be detected in less than two weeks of the compromise. 

## Scenario 9 - Incident after source code compromise
Given all of an products source code is compromised:
* $COMPANY will publicly disclose an incident with leaked customer data within a quarter. 
* There will not be a publicly disclosed incident with leaked customer data within a quarter. 

## Scenario 10 - AWS credential leak
Given an AWS role credential on a random public facing server is compromised:
* $COMPANY will publicly disclose an incident with leaked customer data within a quarter. 
* There will not be a publicly disclosed incident with leaked customer data within a quarter. 

## Scenario 11 - Hunt Sev1/0
Given a specialized Splunk hunt investigates the last 30 days of all Splunk logs:
* $COMPANY will initiate a severity 0 or severity 1 incident related to the Splunk log hunt findings. 
* $COMPANY will not initiate a severity 0 or severity 1 incident related to the Splunk log hunt findings. 

## Scenario 12 - Hunt Sev1/0
Given a specialized CloudTrail hunt investigates the last 30 days of logs:
$COMPANY will initiate a severity 0 or severity 1 incident related to the Cloudtrail logs. 
$COMPANY will not initiate a severity 0 or severity 1 incident related to the Cloudtrail logs. 

## Scenario 12 - Hunt Sev1/0
In the next 12 months, an external communication*
* will trigger a severity 0 incident. 
* will not trigger a severity 0 incident. 

