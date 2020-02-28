---
layout: post
title: Forecasting Risk inside an Organization
---
[How can a red team help risk measurement?  1]()

[How did we use forecasting to measure uncertainty?  2](#How-did-we-use-forecasting-to-measure-uncertainty?)

[What does it look like in practice?  2]()

[Step 1: Take the predictions  3]()

[Scenario 1 Round 1  3]()

[Scenario 2 Round 1  3]()

[Forecast Prediction Summary  4]()

[Step 2: Execute operations or wait for scenarios to occur/timeout  4]()

[Step 3: Conclude and score forecasts  4]()

[Learning Points: Scenario Design  5]()

[How do you measure improvement over time?  6]()

[Step 4: Implement improvements and new controls  6]()

[Step 5: Forecast again  6]()

[Scenario 1 Round 2  6]()

[Visualizing the prediction  7]()

[Scenario 2 Round 2  7]()

[Visualizing the prediction  8]()

[Step 6: Calculate Accuracy  9]()

[Learning Points: Accuracy  9]()

[Conclusion  10]()

  

From 2018-2019 I experimented with using forecasting for measuring the effectiveness of red team operations inside Atlassian. I’m publishing my research  so that others can benefit from the effort I put into doing this and see the learnings, failures and successes of the methodology. I am not an expert in statistics, so becoming a subjective bayesian and navigating the challenges, contradictions and uncertainty (lol) in a discipline outside of my normal expertise was no easy task. That being said, I really do believe methodologies like this will have a place in risk measurement in security in the next few years, and can be combined with red team exercises or other external validation sources such as bug bounty. I hope this blog helps someone navigate their entry into this topic.

  

## How can a red team help risk measurement?

I define an effective red team as one that contributes to improving the security posture of the company. The tricky part is measuring that improvement. One of the ways a red team can improve the security posture of an organization is by providing information that allows more accurate risk assessment. Having accurate knowledge of risk scenarios means investments can be made in the correct areas to improve security.

  

Forecasting utilizes the findings of red team exercises as data points to inform our prediction of risk scenarios. Forecasters will have a more thorough understanding of the likelihood of a certain scenario occurring when the red team reveals that they accomplished that task, or tried and failed. Over time, a company will hopefully be able to measure that the likelihood of the most important risks to their business has gone down due to controls implemented, and can validate that those controls work by red team exercises.

  

## How did we use forecasting to measure uncertainty?

In 2019 I published a list of 20 scenarios my panel of forecasters made predictions about for the upcoming 12 months. The forecasters are given training, are calibrated, and use their diverse knowledge of the workings of the organization to discuss each scenario and then estimate the likelihood of those events occurring. This experiment had the goal to reduce [uncertainty](https://magoo.github.io/simple-risk-analysis/) about the chances of these events occurring and therefore have a better understanding of the security posture of the company.

  

At the time I originally wrote this article the forecasters had only done two forecasts. They continued to forecast four times over the last year. They were scored on their accuracy as each forecast concluded and the hope was they would become accurate at making predictions.

  

Being able to measure the *accuracy* of your prediction team is a key benefit of forecasting. You are not simply guessing whether an action will happen and then not measuring (or not being able to measure) if you were correct as is the case in the traditional risk matrix approach. In our methodology each prediction will be concluded as correct or incorrect at the end of the time period (in our case 12 months, or as soon as the outcome occurs) and their prediction accuracy scored using the Brier Score formula. If, after a period of learning/induction training our forecasters are not showing reasonably accurate results, then they should be removed from the program. If they are predicting events accurately, we know that we have accurate predictions of risk!

  

## What does it look like in practice?

I’ll show you how to interpret and then use forecast results by outlining two of the scenarios I tracked with make-believe numbers and example outcomes so you can observe the process. After that I will enter into a hypothetical discussion of potential next steps you could take to continue measuring the tracked risks over time.

  

### Step 1: Take the predictions

Eight people from different departments in security, operations, and compliance participated in the forecast panel. Without going into the step by step process here are two of the scenarios proposed.

  

#### Scenario 1 Round 1

In the next 12 months, during the course of a red team operation, the red team:

1.  compromised one or more employee assigned computers
    
2.  did not compromise any employee computers.
    
| Panelists | A (compromise occurs) | B (no compromise) |
|-----------|-----------------------|-------------------|
| Marissa   | 100                   | 0                 |
| Seth      | 100                   | 0                 |
| Summer    | 80                    | 20                |
| Ryan      | 80                    | 20                |
| Sandy     | 80                    | 20                |
| Kirsten   | 90                    | 10                |
| Juie      | 95                    | 5                 |
| Jimmy     | 90                    | 10                |
| Average   | 89.38                 | 10.63             |
  

#### Scenario 2 Round 1

In the next 12 months if the red team compromises an employee computer the security team

1.  Detects it with an automated alert in less than 48 hours
    
2.  Detects it with an automated alert more than 48 hours after the compromise
    
3.  Does not detect it, it detects it after 7 days or the red team intentionally triggered detection.
    
| Panelists | A (Detects <48 hours) | B (Detects 1d - 7d) | C (No detection or > 7d) |
|-----------|-----------------------|---------------------|--------------------------|
| Marissa   | 30                    | 50                  | 20                       |
| Seth      | 50                    | 50                  | 0                        |
| Summer    | 40                    | 30                  | 30                       |
| Ryan      | 30                    | 40                  | 30                       |
| Sandy     | 40                    | 40                  | 20                       |
| Kirsten   | 20                    | 40                  | 40                       |
| Juie      | 45                    | 45                  | 10                       |
| Jimmy     | 20                    | 60                  | 20                       |
| Average   | 34.38                 | 44.38               | 21.25                    |
  
#### Forecast Prediction Summary

The forecast shows that the group believes that there is an 89% chance that during a red team exercise in the next 12 months there will be a compromised system and that there is a 34% chance of alerting to that compromise within 48 hours of it occurring, 44% chance of alerting on the compromise after 48 hours but before 7 days and 21% chance of it remaining undetected, being detected after 7 days, or the red team intentionally triggering detection because it remained undetected.

  

### Step 2: Execute operations or wait for scenarios to occur/timeout

Next, the security team plans a red team operation attempting a breach involving an external compromise with an attempt at installing malware on and controlling an employees computer. The red team attempts their operation and succeeds in their end goal without being detected, installing and maintaining malware on several employee laptops during the course of the operation. They continue to maintain access to the network and make sure they are accessing target systems for 7 days, giving a chance for detection by the blue team. They then initiate one of the Game Moderator’s (GM) planned incident response trigger scenarios, so that the blue team can start investigating a potential incident and discover what has happened.

  

### Step 3: Conclude and score forecasts

Because the scenarios that were forecasted have met one of the possible outcomes, we can conclude them and calculate the panelists accuracy. To do this we calculate the Brier* score. Brier scores range from 0 being the best possible score and 2 being the worst.

  

*The Brier score is the squared error of a probabilistic forecast. To calculate it, we divide the forecast by 100 so that probabilities range between 0 (0%) and 1 (100%). Then, we code reality as either 0 (if the event did not happen) or 1 (if the event did happen). For each answer option, we take the difference between the forecast and the correct answer, square the differences, and add them all together.

  

In the first scenario the red team did compromise employee computers. So option A is the final outcome and is coded as 1. In the second scenario the computer compromises remained undetected for more than 7 days, so option C is the final outcome, coded as 1.

  
| Scenario           | A (compromise occurs)     | B (no compromise) |
|--------------------|---------------------------|-------------------|
| Panel Prediction % | 89.38                     | 10.63             |
| Coded Outcome      | 1 (This outcome occurred) | 0                 |

  
Brier score calculation:

(1-.8938)^2 + (0-.1063)^2 = 0.02257813

Close to 0, this is an accurate forecast by the panel!
| Scenario           | A (Detects <48 hours) | B (Detects 1d - 7d) | C (No detection or > 7d)  |
|--------------------|-----------------------|---------------------|---------------------------|
| Panel Prediction % | 34.38                 | 44.38               | 21.25                     |
| Coded Outcome      | 0                     | 0                   | 1 (This outcome occurred) |
  

Brier score calculation:

(0-0.3438)^2 + (0-0.4438)^2 + (1-0.2125)^2 = 0.93531313

  

In terms of the first scenario, the panelists were fairly accurate in predicting the outcome. Also, both of our predictions show that panelists already have a better idea than the baseline of total uncertainty about the scenarios. Total uncertainty would be 50% for each outcome in scenario 1 and 33% for each outcome in scenario 2. But where do we go from here?

#### Learning Points: Scenario Design

I’m going to say that these scenarios are actually not ideal for using in this exercise (and this is one of the learnings I made during this experiment). This is because when designing a scenario all potential outcomes for that scenario must be accounted for. In the detection scenario, many other things could happen that might not be covered with an automated detection in the time frame given. For example an employee reports a phishing email after the compromise, while the red team is still operating, concluding the test early and not giving time for detection alerts to fire on further activity.

  

Additionally, over the course of many rounds of forecasting I leaned towards only detection scenarios when relating to red team or penetration testing. The objectives of my team changed fairly often as we try different types of attacks and use different tactics. It was extremely difficult to come up with adequate scenarios when it relates to the red team achieving something, or how they will be detected. I’d love to know your scenarios and if you have any that have worked well over extended periods of time!

## How do you measure improvement over time?

So now that the first forecast is complete, you might be wondering what potential next steps might look like and how to proceed from here.

### Step 4: Implement improvements and new controls

Post red team exercise, the red team sits down with the blue team and helps them understand all the actions that occurred during the exercise. The blue team comes up with several large projects that need to be implemented company wide to lower the chance of this being able to happen again, and many ideas for detections and alerts that they can implement based on the techniques used by the red team. Is that the end of the story? Not at all. We really want to know if the fixes that are planned are going to impact the chances of these attacks being done in the future.

  

You might even have an ideal end state in mind, a certain percentage or level or risk that you would like the team to reach in the future. That’s fine and could even be a goal or metric that is tracked and worked towards. In this example I’ve added some hypothetical 1 year goals, just to add some more data to the visualizations and suggest an idea of how this information could be used to set goals for a team.

### Step 5: Forecast again

It's time for the next quarterly forecast. All the panelists are brought together, and they consider the same scenarios as last time. A briefing of the red team exercise as it related to the scenarios is given and each person is invited to discuss the changes that have occurred since the last forecast and their implications.

  

The IT manager discusses one of the large scale preventative projects has been rolled out to 50% of corporate systems. They believe this will lower the chance of an endpoint compromise. The compliance manager mentions that monthly audits are now automated to check if any unknown accounts are added to the company domain, and believes this may slightly increase detection chances. The offensive operations manager highlights that the company has decided to bring in an external consultancy to supplement additional red team exercises for the next 6 months, and thinks that the new ideas the external group will bring may increase chances of compromise, but also thinks their use of generic tooling and malware may increase chances of detection.

  

The group then makes their individual forecasts and here are the numbers.

#### Scenario 1 Round 2

| Panelists | A (compromise occurs) | B(no compromise) |
|-----------|-----------------------|------------------|
| Marissa   | 95                    | 5                |
| Seth      | 90                    | 10               |
| Summer    | 85                    | 15               |
| Ryan      | 80                    | 20               |
| Sandy     | 100                   | 0                |
| Kirsten   | 85                    | 15               |
| Juie      | 70                    | 30               |
| Jimmy     | 100                   | 0                |
| Average   | 88.125                | 11.875           |

##### Visualizing the prediction

![](https://lh3.googleusercontent.com/iHxl03dYFeT1biDBW8Uj5yWi1lPe5V6axMdJSeCxSGfxkX0xsh3Uj1KgH2NvGRa_VVA5NFTavnoF6foOj5m98p22eZOwa53gTQxPNRAhj7EL2OCqIcWg1ofoCkIYKq95UbzQTqZt)

 
  

The number hasn’t really moved too much in terms of what the panel believes will happen in the next 12 months.

#### Scenario 2 Round 2

| Panelists | A (Detects <48 hours) | B (Detects 1d - 7d) | C (No detection or > 7d) |
|-----------|-----------------------|---------------------|--------------------------|
| Marissa   | 2                     | 58                  | 40                       |
| Seth      | 30                    | 50                  | 20                       |
| Summer    | 30                    | 50                  | 20                       |
| Ryan      | 30                    | 30                  | 40                       |
| Sandy     | 0                     | 70                  | 30                       |
| Kirsten   | 40                    | 10                  | 50                       |
| Juie      | 10                    | 60                  | 30                       |
| Jimmy     | 25                    | 40                  | 35                       |
| Average   | 20.875                | 46                  | 33.125                   |

  

##### Visualizing the prediction

![](https://lh5.googleusercontent.com/7gaNVYqRDG1rY7DcdcDxhMRGYPuuvefC_aXY5k_OvP4Vq6oFUEtVHO-phqnhjdYNzSaKkRzYf_O3v8y4iM7vk6iWxI-PSd3DPXLu3yTnLzSICxzMSI49NGxRvig2M8V9n1bzHv-v)

  

The second scenario is currently tracking in the opposite direction of the imaginary goal (60% chance of automatically detecting a red team compromise in under 48 hours), meaning that the panelists are more certain that they won’t detect a compromise within 48 hours than they were before the first red team exercise.

  

It might not seem it, but this is good! Why? This is an important point to grasp, so I’m going to explain it in a bit more depth.

  

At the beginning of this unholy long blog post I mentioned the goal of this experiment was to “reduce uncertainty”. This means that we don’t really mind whether the forecast for the scenario moves in a “bad” direction.

  

To further elaborate, think about the following situation.

  

Scenario: An AWS key is used by an attacker to access Company data.

Say that the last quarter the forecasters put this at 50% chance of happening. An incident has occurred since then, and the outcome was that this happened. The new forecast is taken and the panel judges the likelihood at 80% now. This looks “bad” right?

  

The panelists are actually a lot more certain about the chance of this happening now, assuming they are generally well calibrated and are forecasting effectively and have low brier scores. This is how an outcome that isn’t moving in the direction wanted is actually ‘good’. They are more certain about the security posture than previously.

  

So for the second scenario, even though it isn’t moving towards the end “goal” yet, the chance of this event occurring has definitely moved in a direction that shows the company that if they want to move towards a 60% chance of detection they will need to significantly invest in their detection capabilities.

  

### Step 6: Calculate Accuracy

These numbers don’t mean anything if red team activities are not regularly undertaken which include playing out the scenarios. Seeing the outcome of a particular scenario allows calculation of the Brier score which shows whether the panelists are making realistic, accurate predictions, or are guessing out of their asses.

  

You won’t know what a *good* Brier score is for each scenario, this will become more evident as time goes on. This happens after a number of Brier scores have been gathered and you can determine approximately what range should be expected for the scenario in question.

  

In our examples above what we know currently is our average Brier score for the first scenario is better than random. 0 is perfect, random would be 1 and 2 is completely wrong. The panel Brier score is 0.02 for scenario 1 and 0.94 for scenario 2.

  

#### Learning Points: Accuracy

Due to poor scenario selection and spreadsheet update exhaustion, I wasn’t able to calculate the ongoing Brier scores for my panelists over the time I was taking their forecasts. Strong commitment to accuracy score calculation and to finding the right balance of plausible and relevant scenarios is necessary to run a successful forecast program.

  

## Conclusion

I went in search of a better way to measure cyber risk in an organization. There is a never ending debate on whether or not quantitative measure are “better” than qualitative when it comes to enumerating risk at a high level, but I do believe that having statistical data with percentages, numbers that can be measured, and the ability to track if predictions are correct or not is a large step in the right direction away from relying on one persons estimate of “high, medium or low” for example.

  

If a better system or application existed to make this framework simple to track over time, then I can most likely say I would still be tracking various scenarios as it relates to not only red team activities but bug bounty findings, real incidents, and anything and everything in between. I think right now it's only available by paying consulting companies. But it is totally do-able and if you want to try it yourself, I hope this post and my mistakes are helpful to your mission.

