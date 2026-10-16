# Preventing-Supply-Chain-Cyberattacks-A-Case-Study-of-the-SolarWinds-Orion-Attack

## Abstract

At the end of 2020, when the world was dependent on technology a catastrophic event disturbed top tech companies and US agencies. There was a supply chain breach that involved the SolarWinds Orion system. The breach in SolarWinds' system not only hampered the single company but also thousands of organizations and agencies. But why did a single company’s loss trigger disturbance within other organizations? It had a domino effect on them. The software company provides system management tools for network and infrastructure monitoring and other services required to most of the organizations around the globe. Orion is a system that primarily monitors the software performance of a product. The system had access to all the critical information and system performance data, which was therefore a golden loophole. Using this golden opportunity, the hack compromised the data, networks, and systems of thousands of application users, which acted as an update but actually was the backdoor malware. All this happened via the method known as a supply chain attack, which works by using the third party to manipulate the organization’s system rather than directly attacking the network. In simple terms, consider this a Trojan’s horse. Instead of attacking the main door, it secretly enters via the backdoor, dressed as a trusted individual, and has direct access to all the private information. This report is a qualitative single-case study. It explains how the attack worked, why it stayed hidden for about 14 months, how it was contained, and what the case teaches about preventing similar attacks. It also compares SolarWinds with software supply chain attacks reported in 2026 to show that the problem is still very much alive. The main finding is that the weak point was misplaced, automatic trust in a signed update, made worse by powerful monitoring tools and little visibility into how software is built. Layered defences such as zero trust, software bills of materials (SBOMs), secure build pipelines and honest incident disclosure can shrink the attacker's window.

 

---

## 1. Introduction

Several organizations, agencies and IT firms are interdependent and prevalently use third-party software for monitoring and operations. Trust between users and providers is built gradually, and that gives rise to an increased number of customers in the market over time. Such trust can lead long-term customers to usually ignore or overlook occasional updates due to the overall trustworthiness and integrity of the company. The supply chain attack was something nobody fathomed because of its sheer scale and the credibility associated with SolarWinds. As part of scrutiny, user companies often have protocols that look for digital signatures as a token of proof of credibility. At the end of 2020, the cybersecurity company FireEye (Mandiant) warned of the breach through a Trojanised update to the SolarWinds Orion system. Emergency directives commanded all users to disconnect or shut down their devices till further notice.

### Problem statement:

Traditional security relies on the assumptions that the threats come from outside and the software from a trusted vendor is safe. A supply chain attack contradicts both of these assumptions. This report addresses the following questions: how was an ordinary update turned into a tool for cyberattack, why did the existing defences not detect it for such a long period of time and what can be done differently.

### Why this topic is relevant to today's challenges:

The SolarWinds attack occurred some years ago, but it is not outdated. Supply chain attacks became very common in the current threat landscape. According to the last data, the XZ Utils compression library was found to have a backdoor in 2024, which CISA (2024) identified as CVE-2024-3094. The frequency of supply chain attacks continues to increase in 2026. Zscaler's ThreatLabz team reported five major software supply chain attacks in March 2026, one of them is the compromise of the Axios npm package (Zscaler ThreatLabz, 2026). Axios is a JavaScript library with over 100 million weekly downloads (Trend Micro, 2026). Microsoft described the ChainDrop worm that spreads itself and steals credentials, which was hidden in over 400 npm packages (Microsoft Threat Intelligence, 2026a).

### Objective

- To explain in detail how the SolarWinds Orion supply chain attack was carried out.
- To find the gaps and loopholes that allowed an unusually long dwell time.
- To propose a methodology to mitigate the unseen attack and constant self monitoring
- To compare SolarWinds with current (2026) supply chain incidents and draw practical lessons for prevention.

---

## 4. Methodology

We are considering the MAFIA game and all the resources as the villagers. Our drawback in the case study is that the attack is hidden and is left undiscovered, hence we are modelling our software ecosystem as a village, with villagers not knowing who the mafia is. With endless hidden security keys and constant monitoring (that again will be hidden), it is easy to separate out that part of the resource which is compromised.

In our scenario, the moderator shall do his work silently and monitor every movement with eyes open but as a silent spectator. The hidden state of moderator will be a trap for the mafia and thus protecting the entire village.

Every villager is linked or dependent to other villagers, same way the software packages have similar dependencies. We are also using a priority queue to investigate the abnormality based suspicious packet first. By following this, the defender can focus on the most urgent threats. The resource is huge in our case and hence we can find a genuine compromise. There are possibilities of countering false positives and hence we measure detection time, affected packages and recovery time. We then compare these results with the original workflow and then determine whether prioritization and early containment actually improve security.

Our above study is one method and the other method we are using is an analysis of a single case in SolarWinds Orion attack. The timeline is rebuilt from public reports (Mandiant, CISA, Microsoft), and the attacker’s actions resemble the MITRE ATT&CK framework.

| | |
| --- | --- |
| Villager | A software package |
| Mafia | Compromised package |
| Links between the villagers | Interdependency |
| Moderator | Hidden monitoring layer that is a silent spectator |
| Night attack | Spread of attack by using interdependency |
| Alienating or casting out a villager | Isolating the suspicious package. |

### Model design:

- A graph (data structure analysis, G=(V,E)) is taken into consideration and will help us show the dependency.
- We will randomly choose a node and consider it as compromised.
- A moderator will be allotted, who will keep an eye on all the movements, updates and in the scenario will give a score to each node between 0 and 1. The basis of the score will be determined by the behaviour and obnoxious network connections.
- Using the score all the nodes will be arranged in max heap order, this helps us find the highest score node at priority and securing the other part that is not affected.
- This process will help us segregate the compromised node and save the other nodes from getting attacked.

### Baseline and Comparison

The infected graph is run under two circumstances, first being baseline and other will be the proposed workflow(priority queue and hidden monitoring). The baseline will have no priority and follow the FIFO concept, this aligns with our concept of routine updates that were held by SolarWinds.

In this workflow what we are procuring is detection time, affected packages, recovery time and the false positive rates. These parameters determine the efficiency of our proposed methodology.

---

## 7. Implementation Details and Proposed Security Controls

### Algorithm:

```text
1. Build dependency graph G with N nodes
2. Infect one random seed node
3. Repeat each time step:
   a. Infected nodes infect dependents with probability p
   b. Moderator updates anomaly scores (infected: high, healthy: low, plus noise)
   c. Baseline: pick next node by FIFO | Proposed: pop highest score from heap
   d. If node is infected: isolate it and queue its dependents
      Else: record a false positive
4. Stop when no infected nodes remain; record the four metrics
```

---

## 10. Conclusion

The SolarWinds attack was an eye-opener for several companies and government firms for using credible software updates. We never know the uncertainties and flaws that lie in a trusted resource. It is essential to go through all the terms and conditions without haphazardly accepting them. The above methodology is a small solution and a step that should be deployed by all the open source software users for monitoring purposes. Even though the third party software is providing their services, it is essential for the company to have its own monitoring system that keeps track of what exactly is taking place inside.

Companies that recognized such as FireEye also went with the similar strategies and there are cyber security companies that are still working on this massive hack that is still operational till date. As per our understanding and knowledge we brainstormed and came to this solution of using ‘Mafia Game’ and try to minimize the effect that shall eventually mitigate the spread of infection.
