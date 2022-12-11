---
title: Evaluating and Improving Transaction Monitoring Systems - Is there a better
  way ?
author: Govind Nair
date: '2022-12-11'
slug: evaluating-and-improving-transaction-monitoring-systems-is-there-a-better-way
categories:
  - Article
tags:
  - Anti Money Laundering
  - AI
subtitle: ''
summary: 'Rethinking AML Transation Monitoring'
authors: []
lastmod: '2022-12-11T11:53:56-05:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---
Transaction monitoring has been a critical component of AML compliance for the last twenty years. Financial institutions devote a tremendous amount of resources to maintain, optimize and enhance transaction monitoring systems in order to keep pace with the rapid changes in financial crime and the evolving nature of regulations.

The work horse of transaction monitoring over the past two decades has been rule based systems commonly referred to as scenarios. Scenarios are essentially simple if-else statements that trigger an alert if a specified combination of conditions are met. E.g. **If X > a and Y > b or Z  > c**. In industry parlance, X ,Y and Z are parameters while a,b and c are thresholds.


Financial institutions can deploy anywhere between a few to several dozen scenarios depending on the size and risk profile of the institution. New scenarios are also deployed in response to new products that the institution brings to market.


## Scenario tuning, and its limitations

The foremost challenge in running an effective transaction monitoring system is ensuring that the system is monitoring the right activity, in other words – Is the system appropriately tuned? If the thresholds of the scenario are too low, you could end up generating too many false positives, if they are too high, you could end up with false negatives - a scary proposition for most institutions.

Financial institutions have traditionally used Above The Line (ATL) and Below The Line (BTL) testing to evaluate whether a scenario is appropriately tuned. There are several limitations with this approach.

Firstly, each scenario is evaluated and tuned independently; this ignores an important property of the system – scenarios do not operate in isolation. Multiple scenarios interact and overlap to create a monitoring mesh. 

In team sports, evaluating the players in a team independently does not tell you about the quality of a team. In transaction monitoring, evaluating each scenario independently does not necessarily tell you about the quality of the overall system. 

Just as 11 of the best players do not make the best team, using eleven conservatively tuned scenarios need not make a high-quality transaction monitoring system. There could be blind spots in the monitoring system that could still be exploited by sophisticated actors. Conversely, you can often build a great team by identifying the right players who complement each other’s strengths and weaknesses. A team can be much more than the sum of its individual parts. Could the same dynamics apply to transaction monitoring systems?  Is it possible to evaluate and improve a transaction monitoring system holistically rather than reductively?

Secondly, several institutions use the analysis of ATL data to determine if BTL testing is necessary. If the ATL data indicates an absence of effective alerts near current thresholds, BTL testing is deemed unnecessary.

The absence of effective alerts ATL might be a necessary but not sufficient condition for AML risk below the line. When scenarios are deployed to provide coverage rather than to detect specific activity, ATL results may not be a good predictor of BTL risk. This also doesn’t mean it is prudent to indiscriminately do BTL testing for every scenario.

Is there a more systematic way to determine whether there is AML risk below the line for a scenario based on which a decision can be made to carry out BTL testing?

Thirdly, when a decision to do BTL testing has been made, institutions determine the threshold to be tested fairly arbitrarily using 5,000 or 10,000 dollar increments. There is simply no reason why increments should be in multiple of  5,000 or 10,000 or 2,450.

Is there a more methodical, explainable way to determine the right threshold below the line that should be tested?

Finally, consider the fact that ATL and BTL tuning is typically carried out on 12 -18 months of historical data. The data issues permeating this historical data are well understood by most institutions. Most of the good alerts or SARs used to tune a scenario (e.g. Rapid Movement of Funds) are not a result of activity of interest to the scenario. In fact, these alerts might have been tagged as suspicious due to entirely tangential reasons (e.g. Negative News on the focal entity). Many institutions continue to use this problematic data to tune scenarios as removing these will leave them with very little signal to tune the scenario.


The overwhelming majority of customers at financial institutions are law abiding citizens. Stringent KYC procedures ensure that any individual or corporation with even a whiff of suspicion are denied services or have the banking relationship terminated. This means the historical data used to evaluate transaction monitoring systems are largely from benign customers.

Using historical transaction data to evaluate transaction monitoring systems is akin to evaluating the strength of the financial system in 2008 using data from the boom years preceding the financial crisis. This never revealed weaknesses in the system. After the great recession of 2008, regulators mandated that institutions carry out stress tests to evaluate the robustness of the financial system.

In AML, is it sufficient to evaluate our transaction monitoring system with data that is equivalent to that of the pre-crisis boom years? How can we stress test the system so that its weaknesses become apparent, giving us the opportunity to fix it before a sophisticated money laundered exploits it?


## A Better Way

### A holistic approach

I believe that a better way of evaluating transaction monitoring requires us to take a holistic perspective. Scenarios interact and overlap in ways that impact the system’s performance. Viewing transaction monitoring systems through this holistic lens will 
a)	Reveal opportunities to retire scenarios and relax thresholds by identifying redundancies
b)	Alert us to gaps in the system that can be fixed by raising thresholds or deploying a new scenario.

### An adversarial approach

A modern approach to evaluating and improving transaction monitoring systems can also learn from ethical hacking in the cybersecurity domain.


>Ethical hacking is a process of detecting vulnerabilities in an application, system, or organization's infrastructure that an attacker can use to exploit an individual or organization. They use this process to prevent cyberattacks and security breaches by lawfully hacking into the systems and looking for weak points.
Ethical hackers learn and perform hacking in a professional manner, based on the direction of the client, and later, present a maturity scorecard highlighting their overall risk and vulnerabilities and suggestions to improve


I believe a transaction monitoring system should be evaluated by determining how effectively it can resist an adversarial money launderer who is seeking to move money through the bank. A robust transaction monitoring system will make it infeasible for the money launderer to move money through the bank in a reasonable length of time without triggering alerts.

## A Modern Approach to evaluating Transaction Monitoring Systems

A system that takes such a holistic, adversarial perspective can address the limitations of scenario tuning approaches used by financial institutions today.

The solution is to simulate a money launderer who can test the transaction monitoring system for gaps, much like how an ethical hacker probes a cybersecurity system for vulnerabilities.

Such an agent can probe the entire transaction monitoring system rather than each scenario in isolation.
Further, the patterns identified by such an agent can be used to identify real BTL risks for each scenario which in turn can inform which scenarios should be subjected to BTL testing and which thresholds BTL should be tested.

Besides addressing the limitations discussed earlier, this new system will be able to highlight the pathways or gaps a potential money launderer could exploit. It can also recommend threshold changes and scenarios that can plug these gaps. 

If an institution wants to launch a new product, the system will be able to determine what the resulting AML risk to the institution is. It will be able to mitigate this AML risk by recommending threshold changes to existing scenarios or recommend new scenarios to monitor this product.

Obviously, unlike in cybersecurity, financial institutions do not have the option to hire ethical money launderers to help evaluate the system. How can Financial Institutions implement such an adversarial, intelligent approach to evaluating transaction monitoring systems? 

Advances in deep learning and reinforcement learning have made it possible to solve a problem that has been intractable up to this point. At Oracle, we are building  Compliance Agent, a product that attempts to solve this problem using deep reinforcement learning to train such an adversarial agent.

OFS Compliance Agent will assess the transaction monitoring system of an institution holistically, identify gaps, recommend changes to address these gaps and also provide an estimate of the operational impact of these changes.

If you are interested in learning more, feel fee to reach out to me. I will be happy to set up a deep dive and present some of these ideas in more detail. We are also looking for forward thinking financial institutions to enroll in the Beta program for  Compliance Agent - so join us to help create the future!
