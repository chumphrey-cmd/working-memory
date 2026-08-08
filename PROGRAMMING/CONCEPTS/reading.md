# Wire Mythos Overview
[Wired Mythos Overview](https://www.wired.com/story/anthropics-mythos-will-force-a-cybersecurity-reckoning-just-not-the-one-you-think/)

* Many companies are not capable of securing their infrastructure—that hasn’t really changed from yesterday to today,” says longtime security engineer and researcher Niels Provos. “But from what I understand, Mythos is really good at coming up with multistage vulnerabilities, and then also provides the proof of exploitation. **I don’t think it intrinsically changes the problem space, but it changes the required skill level to find these vulnerabilities and exploit them.**”
* “In the long run, you want to make sure that your defenses are machine-scale, because the attacks are machine-scale,” Patel said. “If I have billions of agents that are going to be attacking my infrastructure, I need to make sure that I can defend it effectively. What Anthropic did here is a fantastic thing, because it just creates a level of asymmetry against the bad actors.”
* “If you get a million vulnerability researchers, they can find a huge number of bugs. But humans are not very good at holding lots of contextual information in their minds for long periods of time, so finding very long chains of vulnerabilities that are actually exploitable together has been rare," she says.

# MOAK 
[Mother of All KEVs](https://moak.ai/#how-it-works)
* This is a first-of-its-kind automatic predictor of whether a CVE will be exploited in the wild within hours.
* MOAK is a defensive security research system, not an attack tool. It operates exclusively in controlled, isolated environments to help defenders understand and assess the real-world exploitability of vulnerabilities.

(#Prioritization, #Security, #SLAs, #RiskManagement)

* In light of recent events Anthropic has released a cutting edge model and restricted access to roughly 40 to 50 organizations, including major technology companies and critical-infrastructure groups, to help identify and remediate vulnerabilities. While this capability is rumored tested to be truly impactful to the world of computer security. MOAK's core claim is that “AI attackers aren’t coming, they are here,” and the project is positioned as proof that known exploited vulnerabilities (KEV) can be turned into working exploits automatically at very high rates using the current generative models that are pubically available. It doesn't take the emergence of a state of the art (SOTA) model like Mythos from Anthropic to be provided. 
* This now introduces the question of how Blue Teams and Red Teams should approach the pace of KEVs being readily exploited and, from a risk point of view, how small to medium-sized organizations look into reshaping SLAs and prioritization of published vulnerabilities as they arise and are published.
* Blue teams should treat KEV exposure and weak security posture as a time-compressed problem, not a routine backlog problem, because MOAK’s creators explicitly warn of “spray and pray” exploitation within about an hour of disclosure and AISI says Mythos can autonomously attack small, weakly defended vulnerable enterprise systems. Patch SLAs, compensating controls, and exposure management need to be tied to exploitability and external reachability rather than generic severity labels alone.

---

* Additional Blue Team challenges to consider is the collapsing the triage time for internet-facing KEVs and 1-days to aim for same-day decisioning on patch, isolate, virtual patch, or block. This also gets into a discussion about the speed at which Security Incidents and Actions are decided for public facing applications. If an AI system can turn public technical detail into an exploit path quickly, the question is no longer “Is this vuln present?” but “Can this vuln reach impact in this environment before we contain it?”

* From the Red Team point of view the Red Team should assume that AI will automate the lower half of the kill chain (e.g., Reconnaissance, Resource Development, Initial Access), so their value shifts away from proving that a missing patch exists and toward emulating adaptive, chained, objective-driven operations. Basically, there will be more focus on attack chains or systematic staging of attacks rather than isolated and one-off exploits

* From a #Prioritization POV both red and blue teams is a shift from capability-centric thinking to tempo-centric thinking. Similar to how the emergence of generative AI has speed up the code output of the individual developer. The same pace and tempo is true in the discovery and exploitation of vulnerabilities.

---

(#DeployingApplications, #Security, #SLA, #Prioritization, #TechnicalResearch)
* I try to level-set the discussion by tying these stories directly to SWF operations from what I've seen on how applications are deployed and the speed at which they are deployed. From what I understand, I believe that there should be a shift towards speed of shipping, internet exposure, and contractual uptime commitments as part of exploit priority, not as separate business concerns. What this basically means is that the organization should develop a more flexible risk mental model by considering if this feature is reachable from the internet, customer-facing, and hard to patch without downtime, how fast could it hurt my organization?
* A better prioritization mental model when securing, developing, and deploying applications could be ordered as follows (1 - highest priority to 5 - lowest priority)

1. Internet-facing authentication, session, and identity flows, because compromise there usually scales across tenants and users quickly. 
2. File upload, webhook, search, prompt-processing, admin, and integration endpoints, because AI-generated code often mishandles input validation, SSRF, injection, and auth boundaries. 
3. Dependencies and frameworks used by newly shipped features, especially where AI suggested packages, copied old examples, or reintroduced outdated patterns. 
4. Anything tied to SLA penalties, uptime guarantees, or customer contractual commitments, because remediation may be slower and impact larger. 
5. Internal-only tools with strong segmentation, because they usually have more containment options than public product surfaces.

---

(#DeployingApplications, #Security, #TechnicalResearch, #Prioritization)
* Since AI models tend to repeat the same mistakes, an attacker would need to find these bugs just once. “Millions of developers using the same models means the same bugs showing up across different projects,” he said. “Find one pattern in one AI codebase, you can scan for it across thousands of repositories.” (https://research.gatech.edu/bad-vibes-ai-generated-code-vulnerable-researchers-warn)
* The control point is not “ban AI coding”; it is forcing security gates around code that was produced faster than humans can fully reason about on first pass.
* When considering the growing emergence and incentive to ship products as fast as possible it runs into a problem that I’ve been thinking about with AI generated code. There is a huge push and also incentive for developers to deliver products and features quickly utilizing this generated code. As a result, some companies have projected that 80 to 90% of their code base will be AI generated.
* I think the practical answer is not to resist AI coding, but to redesign engineering so that AI can generate code freely inside hard security boundaries, mandatory validation, and risk-based release gates.
* A good mental model that I think about is as follows:
  * Let AI maximize coding speed
  * Let policy constrain what “acceptable” code looks like.
  * Let automation reject unsafe output before it reaches production.

---

* In theme with my current discussion on AI-generated code and #Security. From a #RiskManagement and Security POV - the broader lesson is that AI-generated code should be treated like industrialized software output or a manufacturing plant you do not secure it by inspecting every unit manually, but by building a secure factory around it (e.g., CI/CD pipelines, Static/Dynamic Application Security Testing (SAST/DAST), Software Composition Analysis (SCA)). Obviously, testing EVERYTHING is ideal, but when speed and feature delievery is of the essensce a rule of thumb like:

1. SAST and secrets scanning for source-level issues. 
2. SCA for vulnerable or hallucinated dependencies. 
3. DAST and adversarial API testing for runtime behavior. 
4. Human review for auth, crypto, tenancy, and sensitive data logic.

* If a component is high-risk, then testing each component via #UnitTests, integration tests, and end-to-end tests with meaningful coverage of expected and unexpected behavior. From a #RiskManagement and #Prioritization POV I suspect that testing in layers would be ideal, for example: "verify every high-risk path exhaustively and automatically, then add human review where design mistakes are expensive."

---

* To finish up with the series of journals, I wanted to touch on risk #Metrics that I think I as a developer should be considering when building and deploying given where the SWE industry seems to be moving. If AI will write most of the code, from a #Security standpoint, I believe I should start asking whether AI-generated changes are introducing more exposure, more risky dependencies, or more security exceptions. Some of the key metrics should be release-risk metrics, rather than authorship metrics (e.g., AI generated vs human-generated) (https://cloudsecurityalliance.org/blog/2025/07/09/understanding-security-risks-in-ai-generated-code) 

* Some useful #Metrics that I saw online for risk-based metrics are as follows:

1. Percent of AI-assisted changes that touch exposed or sensitive paths. 
2. Time to detect vulnerable dependencies added by AI-generated changes. 
3. Rate of blocked merges due to CI/CD pipeline failures. 
4. Mean-time to remediate (MTTR) security findings in AI-assisted features. 
5. Number of production incidents tied to missing validation, auth flaws, or unsafe dependency choices.

---

# Red Team Anthropic
[Red Team Anthropic](https://red.anthropic.com/2026/mythos-preview/)
* The best way to be ready for the future is to make the best use of the present, even when the results aren't perfect.
* Gaining practice with using language models for bugfinding is worthwhile, whether it’s with Opus 4.6 or another frontier model. We believe that language models will be an important defensive tool, and that Mythos Preview shows the value of understanding how to use them effectively for cyber defense is only going to increase—markedly.
* Think beyond vulnerability finding. Frontier models can also accelerate defensive work in many other ways. For example, they can:
* Provide a first-round triage to evaluate the correctness and severity of bug reports; 
  * De-duplicate bug reports and otherwise help with the triage processes; 
  * Assist in writing reproduction steps for vulnerability reports;
  * Write initial patch proposals for bug reports;
  * Analyze cloud environments for misconfigurations;
  * Aid engineers in reviewing pull requests for security bugs;
  * Accelerate migrations from legacy systems to more secure ones;
* **To summarize:** it is worth experimenting with language models for all security tasks you are doing manually today. As models get better, the volume of security work is going to drastically increase, so everything that requires manual triage is likely to benefit from scaled model usage.
* Automate your technical incident response pipeline. As vulnerability discovery accelerates, detection and response teams should expect a matching rise in incidents: more disclosures mean more attacker attempts against the window between disclosure and patch. Most incident response programs cannot staff their way through that volume. Models should be carrying much of the technical work: triaging alerts, summarizing events, prioritizing what a human needs to look at, and running proactive hunts in parallel with active investigations. During an incident itself, models can help take notes, capture artifacts, pursue investigation tracks, and draft the preliminary postmortem and root-cause analysis as the basis for further validation.

# Linus's Law
[Linus's Law](https://en.wikipedia.org/wiki/Linus%27s_law)
* Given enough eyeballs all bugs are shallow...
* Given a large enough beta-tester and co-developer base, almost every problem will be characterized quickly and the fix obvious to someone." Presenting the code to multiple developers with the purpose of reaching consensus about its acceptance is a simple form of software reviewing. Researchers and practitioners have repeatedly shown the effectiveness of reviewing processes in finding bugs and security issues.


# Anthropic Bug Finding
[Anthropic Bug Finding](https://www.anthropic.com/news/mozilla-firefox-security)
* We ran this test several hundred times with different starting points, spending approximately $4,000 in API credits. Despite this, Opus 4.6 was only able to actually turn the vulnerability into an exploit in two cases. This tells us two things. 
* One, **Claude is much better at finding these bugs than it is at exploiting them. Two, the cost of identifying vulnerabilities is an order of magnitude cheaper than creating an exploit for them**. However, the fact that Claude could succeed at automatically developing a crude browser exploit, even if only in a few cases, is concerning.
* First, when researching “patching agents,” which use LLMs to develop and validate bug fixes, we have developed a few methods we hope will help maintainers use LLMs like Claude to triage and address security reports faster.
* Claude works best when it's able to check its own work with another tool. We refer to this class of tool as a “task verifier”: a trusted method of confirming whether an AI agent’s output actually achieves its goal. Task verifiers give the agent real-time feedback as it explores a codebase, allowing it to iterate deeply until it succeeds.

# Hunted Lab Dependency Vulnerability Scanning
[Hunted Lab Dependency Vulnerability Scanning](https://huntedlabs.com/research/popping-fast-globs-hood)
(#Security, #DeployingApplications, #RiskManagment)
* There's a popular package called **Fast-glob** that's a widely used Node.js utility designed to quickly find files and folders that match specific patterns, is maintained by a single developer working for Yandex, a Russian tech company that cooperates with requests from the Federal Security Service (FSB), Russia’s security and counterintelligence agency.
* This package is at significant risk of falling under foreign ownership, control, and influence. We recommend its immediate removal from products, particularly those purchased or used by the U.S. Department of Defense or the Intelligence Community.
* A solo maintainer based in an authoritarian country—characterized by a strong security service and limited human rights protections—poses a potential risk to the security and integrity of the package, especially one with the access and popularity of fast-glob. 
* Put simply, fast-glob offers both the solo maintainer and the Kremlin an opportunity to carry out a state-sponsored attack, especially given the open-source community’s tendency to blindly adopt projects with little to no information about the contributors behind them. We cannot overstate the risks. 
* While `mnmInc` has no current ties to any threat actors, the profile could be compromised with near-zero effort. Once that happens, `mnmInc` could push or be influenced to make updates to more than 5,000 projects without oversight from any other GitHub user. This would allow Russia attack vectors immediate access to thousands of known projects—not to mention an unknown number of undisclosed and private projects, including the entire Node.js community. A compromise of that magnitude could infiltrate and disrupt critical infrastructure across government, commercial, healthcare, and financial systems, not to mention the countless other vital industries that citizens around the world rely on every day.

[Data Transfer Objects (DTOs)](https://medium.com/@vishamberlal/understanding-data-transfer-objects-dto-in-spring-boot-ac06b575a1d5)
(#Architecture, #DesignPatternBasics, #RelationalDatabaseBasics)

[Simplifying Unit Testing with Mockito](https://medium.com/@kaustubh.saha/simplifying-java-unit-testing-with-mockito-f4fa6e1ca2fb)

(#UnitTesting, #SpringBasics, #TestDrivenDevelopment)

[Code Review Commentary](https://docs.google.com/document/d/1FKr3MThNbb08SaQuBRftiDcz62ZHEqUwagsAsVOiMtY/edit?tab=t.0)
(#Pairing, #Metrics, #Prioritization, #BalancedTeam)


# DORA Development Metrics
[DORA Development Metrics](https://dora.dev/guides/dora-metrics/)
(#Metrics, #Prioritization, #DeployingSoftware)

* DORA has identified five software delivery performance metrics that provide an effective way of measuring the outcomes of the software delivery process.
* These software delivery performance metrics can be viewed as both leading and lagging indicators. Leading indicators typically signal potential future changes in a system while lagging indicators reflect past performance and outcomes.
* DORA metrics function as to identify:
  * Leading indicators for organizational performance and employee well-being 
  * Lagging indicators for software development and delivery practices.

* The set of DORA metrics are grouped into **`Throughput`** and **`Instability`**
* Basically, **throughput** and **instability** are used to give teams a high-level understanding of their software delivery performance.

**Throughput:**
Throughput is a measure of how many changes can move through the system over a period of time. Higher throughput means that the system can move more changes through to the production environment. DORA uses three factors to measure software delivery throughput:
1) Change lead time: The amount of time it takes for a change to go from committed to version control to deployed in production. 
2) Deployment frequency: The number of deployments over a given period or the time between deployments. 
3) Failed deployment recovery time: The time it takes to recover from a deployment that fails and requires immediate intervention.

**Instability:**
Instability is a measure of how well the software deployments go. When deployments go well, teams can confidently push more changes into production and users are less likely to experience issues with the application immediately following a deployment. DORA uses two factors to measure software delivery instability:
4) Change fail rate: The ratio of deployments that require immediate intervention following a deployment. Likely resulting in a rollback of the changes or a “hotfix” to quickly remediate any issues.
5) Deployment rework rate: The ratio of deployments that are unplanned but happen as a result of an incident in production.

> [!NOTE]
> Speed and stability are not tradeoffs. In fact, we see that the metrics are correlated for most teams. Top performers do well across all five metrics, and low performers do poorly.
> These metrics work for any type of technology your organization is delivering, but are best suited for measuring one application or service at a time. Whether you are building large language models, retail banking applications, mobile food ordering applications, or mainframe-based travel systems, these five metrics can help you assess the delivery performance of your application. 
> Context matters. Apply the metrics in the context of the application or service your team is delivering. The context for your application, organization, and users will vary from other applications that your organization is delivering. While it may be tempting to blend metrics across multiple teams or entire organizations these differences in context mean that doing so can be problematic.

**Common Pitfalls**

* The full list of common pitfalls can be found [here](https://dora.dev/guides/dora-metrics/#common-pitfalls). I've included the set of pitfalls that resonated with me the most...

**Setting metrics as a goal** - this basically means that a team should ignore broad statements that box in an application (e.g., "every application must deploy multiple times per day by year's end"). The result of this are teams attempting to simply game the metrics that they are being assessed on. [Goodhart's law](https://en.wikipedia.org/wiki/Goodhart%27s_law) summarizes this nicely by stating, "When a measure becomes a target, it ceases to be a good measure". Additionally, in the words of Charles Munger - "Show me the incentive, and I'll show you the outcome..."

**Having one metric to rule them all** - this means that teams should avoid attempting to measure complex systems with the idea that only one metric matters. Teams should identify multiple metrics, including some with a healthy amount of tension between them [measurment framework](https://dora.dev/insights/measurement-frameworks/). Essentially we should seek to have a diversity of metrics to assess the efficiency of an application.

**Using industry as a shield against improving**. For example, some teams in highly regulated industries might claim that compliance requirements prevent them from disrupting the status quo (e.g., the ASWF operating within a larger bureaucratic organization where process and procedure are sacrosanct.)

**Competing**. The goal is to [improve your team’s performance over time](https://dora.dev/guides/how-to-empower-software-delivery-teams/), not to compete against other teams or organizations. Use the metrics as a guide for identifying areas for growth and celebrating progress. Often times, teams may forget what they are... a TEAM. The goal is to improve the entire organization and the products that it creates!

**Focusing on measurement at the expense of improvement.** To me this means that a manager or technical lead may overfit or overemphasize the goal of getting the most real-time and purest measurement metrics rather than opting for a simpler discussion with less technical overhead (e.g., building integrations to multiple systems to get precise data about your software delivery performance rather than simply having a discussion about the metrics using something like [DORA Quick Check](https://dora.dev/quickcheck) or other [available products](https://dora.dev/resources/#source-available-tools)).

# The Bitter Lesson

Ref: [Bitter Lesson](https://www.cs.utexas.edu/~eunsol/courses/data/bitter_lesson.pdf)

* Seeking an improvement that makes a difference in the shorter term, researchers seek to leverage their human knowledge of the domain, but **the only thing that matters in the long run is the leveraging of computation**. These two need not run counter to each other, but in practice they tend to. Time spent on one is time not spent on the other.
  
> [!NOTE]
> *The investment and **moat** of a company should be spent on computation rather than comprehensive know-how...*

* And the human-knowledge approach tends to complicate methods in ways that make them less suited to taking advantage of general methods leveraging computation.
  
> [!NOTE]
> *The information that you know and are exposed to tends to blind you information that is obvious, what Rich Sutton explains as "belated learning" or the curse of knowledge where you are so familiar with a concept that you miss the obvious in-efficiencies*
> *There's also the idea of **DOMAIN DEPENDENCE** whereby you're expertise blinds you to seeing alternative solutions*

* Entrants included a host of special methods that took advantage of human knowledge - knowledge of words, of phonemes, of the human vocal tract, etc. On the other side were newer methods that were more statistical in nature and did much more computation, based on hidden Markov models (HMMs). 
  
> [!NOTE]
> *Statistical methods won over the human-knowledge-based methods. This led to a major change in all of natural language processing, gradually over decades, where statistics and computation came to dominate the field.*
> *The power of statistics and raw computation over tactic human knowledge...*

* To see this, and to effectively resist it, we have to understand **the appeal of these mistakes**. We have to learn the bitter lesson **that building in how we think we think does not work in the long run**. The bitter lesson is based on the historical observations that:
  1) AI researchers have often tried to build knowledge into their agents
  2) This always helps in the short term, and is personally satisfying to the researcher
  3) In the long run it plateaus and even inhibits further progress
  4) Breakthrough progress eventually arrives by an opposing approach based on scaling computation by search and learning.

* The lessons that should be taken from the bitter lesson: 
  1) The power of general purpose methods that continue to scale with increased computation even as the available computation becomes very great. The two methods that seem to scale arbitrarily in this way are *search* and *learning*.
  2) Our minds are complex and difficult to replicate, we need to simplify how we represent the contents of our minds. We should build in only the meta-methods that can capture arbitrary complexity. We want AI agents that can discover like we can, not which contain what we have discovered. Building in our discoveries only makes it harder to see how the discovering process can be done.

> [!NOTE]
> *Don't underestimate the power of brute-force techniques even if they are computationally expensive*
> *The advantage to companies and people the leverage and have a monopoly on electricity/electrons is Pareto distributed and makes it difficult for other companies to duplicate*
> *We want AI agents that can discover like we can, not which contain what we have discovered. Building in our discoveries only makes it harder to see how the discovering process can be done.*


# Extreme Programming 

* I'm currently reading Extreme Programming (XP) and I've run across the idea of the "basics of software development" which are **coding**, **testing**, **listening**, and **designing**. Coding, testing, and designing seem immediately apparent. After some thinking I found that #Feedback and #Facilitation fit quite nicely into this XP idea. Before encountering the idea, I interpreted feedback specifically as **ONLY** the response that a mentor or potential pair would give you on how you were performing while building an application. But I've discovered that it also represents the response and commentary from the end user and stakeholder about applications/features that you are building as well. In XP, #Feedback directly informs what exact feature you build, iterate, or discard next. The book also explains that #Feedback is also a part of the **listening** basics where, as a developer you pay very close attention to what your core customer/audience demand from you.
* I've noticed that I, as a developer, should also find way to use #Facilitation to create a productive and open discussion with my end-user and the rest of the #BalancedTeam to actually address and accomplish the goal/target of value. 
* I used to believe that the engineers' sole job was only focusing on building the highest quality thing. But I've learned that it's a much more collaborative process to ensure that you don't waste time building what the customer doesn't want. 
* For example, if the user story for a local quiz tool states that the user wants a feature to modify the settings of their current quiz session so that, when using a quiz tool, they can adjust configurations of the quiz in real time. The developer, PM, designer, and PE need to accommodate that concern and make a focused and concerted effort to bring that setting feature to life (assuming that this feature would add significant value for that customer).
* The developer can then receive #Feedback both in the initial feature addition that they create and while discussing with the customer and rest of the #BalancedTeam on feasibility of what they want to ship to ensure that the customer vision aligns with what will be built.

## Splitting Business and Technical Responsibility

* In Extreme Programming, this idea of splitting the responsibility between business (PM/PDs) and development (SWE/Platform) came up. The specific section covering this was that "...a project must be driven by business decisions, but business decisions must be informed by technical decisions about cost and risk." If either one gains too much power the project suffers hitting on the fundamental importance of a #BalancedTeam.
* The result of the business side of things beings in charge, the project takes on too much effort and way too much risk for too little return. Here, the business specifies too much, some of the items are essential and some are not); the criteria for success is unclear and risky. 
* If development is in charge there is too much effort and way too much risk for too little return. Here, the engineers swing for the fences, install the latest tooling and technologies because they are cutting edge, but don't consider if it's actually adding the most amount of value.

* This makes sense to me, both the teams work in tandem, each not overpowering one another and is why #Pairing between different disciplines is so essential. You get to avoid the drawback of siloing context and drawbacks that come from under/over estimating risk, cost, and benefit. 
* This got me thinking about how to properly estimate and make good decisions for #Prioritization and how to accurately assess and measure the #Metrics of the success of a project. The author, Kent Beck states the following for how business and development should handle this. For business, the following should be chosen:
  * The scope or timing of releases.
  * The priorities of the features.
  * The exact scope of the proposal features.
* To the decisions the development organization should contribute:
  * Estimates of the time required
  * Estimates of the consequences of technical alternatives.
  * The set of practices that will be used and the process they will review the effects of those practices and experiment with changes (e.g., #Pairing frequency, coding style, etc.)
* Another interesting idea that I came across was the idea of "cost". Initially I view cost as primarily monetary, what was insightful is that cost for the latest and greatest also include costs in maintenance, learning curve for the team, and cost of time it takes individuals to migrate and begin to adopt the new technology. 


# Eisenhower Matrix - In Progress
* https://sps.columbia.edu/sites/default/files/2023-08/Eisenhower%20Matrix.pdf

# OWASP Risk Rating Methodology - In Progress
* [OWASP Risk Rating Methodology](https://owasp.org/www-community/OWASP_Risk_Rating_Methodology)

# Kent Beck Realted Ideas

## Forest vs. Desert

[1] https://medium.com/@csharpwriter/from-forests-to-deserts-kent-becks-powerful-metaphor-for-modern-software-teams-reflections-from-ab5f162b1579
[2] https://tidyfirst.substack.com/p/forest-and-desert
[3] https://nakamotoinstitute.org/library/the-cathedral-and-the-bazaar/

* The "forest and the desert" is a useful heuristic to describe a place of work/work culture. Something to note is that it's agnostic to any discipline or domain. While Kent Beck doesn't explicitly state that one is superior to another, he provides useful analogies that characterize how one environment would handle specific circumstances and change compared to the other.

### Purpose Between Environments
* In the desert, management knows everything, and workers are paid to perform as instructed. In the forest, purpose flows from within. Teams are self-directed, driven not by blind obedience but by a shared mission. [1]

### Development
* Developing in the desert - a lack of resources, adventure and investment need to be thoroughly planned to ensure survival. Kent Beck explains that the desert implies that there is a lack of:
  * Time, Skills, Learning, Purpose, Clarity, Relationships, Reflection, Improvement, Alignment

### Profitability
* "Despite all this hunger & thirst teams manage to deliver enough software that’s good enough to be insanely profitable." [2]
* Bad software still makes money. The desert is profitable, no doubt. But we’re eating crumbs off the floor. In the forest, there’s a better way: personal development, skill growth, social intelligence, and accountability. That’s where you find the cake.

### Predictability vs. Change
* In the forest, change is embraced, it's expected, and welcomed. In the desert, teams cling to prediction as a survival tactic. If you don’t reach the waterfall on time, you die. Long-term roadmaps exist in both worlds, but only in the forest are they crafted with wisdom, not fear. [1]

### Use of Metrics
* In the forest, metrics are used as indicators—to reflect reality, help us learn, and guide better decisions. In the desert, metrics are turned into control systems. And the moment a metric becomes a goal, it stops being useful. [1]

## Bazaar vs. Cathedral
* https://nakamotoinstitute.org/library/the-cathedral-and-the-bazaar/

* This is a heuristic that describes the methodology and approach to building software. The former is indicative of open-source projects, releasing early and often, involve as many trusted contributors in a project as you can (effectively agile development). The latter is a legacy approach to building software (e.g., waterfall) where everything is carefully crafted, involves isolated artisans/mages that intend to release the final and completed product.

* The author provides these examples for how to conceptualize each heuristic:
  * **Cathedral (Windows OS)**: "...the most important software (operating systems and really large tools like the Emacs programming editor) needed to be built like cathedrals, carefully crafted by individual wizards or small bands of mages working in splendid isolation, with no beta to be released before its time." The idea here
  * **Bazaar (Linux OS)**: "...release early and often, delegate everything you can, be open to the point of promiscuity—came as a surprise. No quiet, reverent cathedral-building here—rather, the Linux community seemed to resemble a great babbling bazaar of differing agendas and approaches (aptly symbolized by the Linux archive sites, who’d take submissions from anyone) out of which a coherent and stable system could seemingly emerge only by a succession of miracles."

* "In fact, I think Linus’s cleverest and most consequential hack was not the construction of the Linux kernel itself, but rather his invention of the Linux development model. When I expressed this opinion in his presence once, he smiled and quietly repeated something he has often said: “**I’m basically a very lazy person who likes to get credit for things other people actually do.**” Lazy like a fox. Or, as Robert Heinlein famously wrote of one of his characters, too lazy to fail." [3]

* Programming Pearls (Jon Bentley) - "If you plan to throw one away, you will throw away two." He is almost certainly right. The point of Brooks's observation, and Bentley's, isn't merely that you should expect first attempt to be wrong, it's that starting over with the right idea is usually more effective than trying to salvage a mess."

### Linus's Law

* Given a large enough beta-tester and co-developer base, almost every problem will be characterized quickly and the fix obvious to someone (*“Given enough eyeballs, all bugs are shallow.” - Linus's Law (dubbed by Eric S. Raymond)*)

#### Cathedral and Bazaar within Linus's Law
* **Cathedral:** "...bugs and development problems are tricky, insidious, deep phenomena. It takes months of scrutiny by a dedicated few to develop confidence that you’ve winkled them all out. Thus, the long release intervals, and the inevitable disappointment when long-awaited releases are not perfect."

* **Bazaar:** "...you assume that bugs are generally shallow phenomena - or, at least, that they turn shallow pretty quickly when exposed to a thousand eager co-developers pounding on every single new release. Accordingly, you release often in order to get more corrections, and as a beneficial side effect you have less to lose if an occasional botch gets out the door."
  * This "wisdom of the crowd" or **[Delphi Effect](https://en.wikipedia.org/wiki/Delphi_method)** (e.g., Poly-Market) allows for greater accuracy.
  * In the bazaar, self-selection occurs. People that want to contribute or "haggle in the Bazaar" for an open-source projects are typically self-selected. 
  * Contributions are received not from a random sample, but from people who are interested enough to use the software, learn about how it works, attempt to find solutions to problems they encounter, and actually produce an apparently reasonable fix. Anyone who passes all these filters is highly likely to have something useful to contribute.

* Adding more beta-testers may not reduce the complexity of the current “deepest” bug from the developer’s point of view, but **it increases the probability that someone’s toolkit will be matched to the problem in such a way that the bug is shallow to that person**.

> [!NOTE]
> Something that should be taken into consideration is that the trust and quality of the contributions made to open-source projects due to coding assistants have degraded trust. Maintainers are inundated with a large number of pull requests that they are unable to properly vet.
> This is the same outcome (inflationary effect) when printing excess currency and how that devalue buying power and dilutes your own currency within a market. There needs to be a reliable governer, both in capital markets and the open-source ecosystem that can vet the quality of pull requests. A potential solution could be an agentic triage agent that validates the quality and criteria of the findings and can deconflict with other pull requests that have already been submitted.
> "Linus’s innovation wasn’t so much in doing quick-turnaround releases incorporating lots of user feedback (something like this had been Unix-world tradition for a long time), but in **scaling it up to a level of intensity that matched the complexity of what he was developing**... he cultivated his base of co-developers and leveraged the Internet for collaboration harder than anyone else, this worked."

### Principles of the Cathedral and Bazaar

1. Every good work of software starts by scratching a developer’s personal itch.
2. Good programmers know what to write. Great ones know what to rewrite (and reuse).
3. Plan to throw away one; you will anyhow
4. If you have the right attitude, interesting problems will find you.
5. When you lose interest in a program, your last duty to it is to hand it off to a competent successor.
6. Treating your users as co-developers is your least-hassle route to rapid code improvement and effective debugging.
7. Release early. Release often. And listen to your customers.
8. Given a large enough beta-tester and co-developer base, almost every problem will be characterized quickly and the fix obvious to someone (*“Given enough eyeballs, all bugs are shallow.” - Linus's Law (dubbed by Eric S. Raymond)*)

## Tussle in Cyberspace (David Clark)

* https://groups.csail.mit.edu/ana/Publications/PubPDFs/Tussle2002.pdf
* The idea that if you change one thing well engineering, you want to minimize the impact of that change. Essentially looking to localize and keep the changes tightly coupled...

#  CI/CD - Trivy pull_request_target GitHub Actions Vuln

[1] https://www.endorlabs.com/learn/github-actions-security-lessons-from-trivy
[2] https://www.crowdstrike.com/en-us/blog/from-scanner-to-stealer-inside-the-trivy-action-supply-chain-compromise/

* There have recently been a slew of Continuous Integration/Continuous Deployment (CI/CD) bugs and vulnerabilities. This is a quick crash course on what has been occuring and how I believe it impacts software development in general...
* From what I've read this falls into the category of Initial Access, Code Execution, Credential Access, Lateral Movement, and Exfiltration within the MITRE ATT&CK framework.
* Misconfigured GitHub Actions workflow in Aqua Security's Trivy repository.

> [!NOTE]
> `aquasecurity/trivy-action` is a GitHub Action published by Aqua Security that wraps its open-source vulnerability scanner, Trivy. It's widely adopted for scanning container images, file systems, and infrastructure-as-code for known vulnerabilities as part of CI/CD pipelines.
> if an action's code is modified, whether by its maintainers or by someone who gained write access, every pipeline that references it will trust and execute the new code on its next run, all with full access to that pipeline's secrets, credentials, and infrastructure [2].

* An attacker exploited a `pull_request_target` trigger to extract a privileged Personal Access Tokens (PAT) from the CI environment.
* As explained by Endor Labs [1], the `pull_request_target` event lets workflows run in the context of the base repository when a pull request is opened, even if that PR comes from an external fork. This means the workflow has access to the base repository’s secrets, tokens, and write permissions.
* The danger arises when such a workflow checks out code from the incoming pull request and then executes it. Untrusted code from any external contributor can run with full access to your repository’s secrets (this doesn't directly impact the ASWF since we don't host anything externally facing and out GitLab Repos are internally facing, however, it's a nuance that I'm taking into account as I create my own CI/CD pipeline's for my external projects).
* The overall attack chain is as follows:
  * The attacker submits a pull request fork on the main Aqua Security Trivy Action repo
  * The default `pull_request_target` workflow checks out the PR’s code 
  * Attacker’s code executes with access to repository secrets
  * Privileged Personal Access Token (PAT) is exfiltrated and can be used to push malicious code to replace the legitimate code that end users will use.

* The two main vulnerabilities exploited were 1) `pull_request_target` and 2) Mutable Git Tagging:

## 1) pull_request_target

[3] https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#pull_request_target
* Runs your workflow when activity on a pull request in the workflow's repository occurs. For example, if no activity types are specified, the workflow runs when a pull request is opened or reopened or when the head branch of the pull request is updated.
* This event runs in the context of the default branch of the base repository, rather than in the context of the merge commit, as the `pull_request` event does. **This prevents execution of unsafe code from the head of the pull request that could alter your repository or steal any secrets you use in your workflow**. This event allows your workflow to do things like label or comment on pull requests from forks. Avoid using this event if you need to build or run code from the pull request. 
* To ensure repository security, branches with names that match certain patterns (such as those which look similar to SHAs) may not trigger workflows with the pull_request_target event.

> [!NOTE]
> Normally, code SHOULD NOT be executed with this GitHub action is created. In the event of Trivy's CI/CD repo the misconfiguration existed in Trivy's repo from October 2025, was publicly flagged by a static analysis tool on November 29, 2025, and sat unpatched for 3+ months before being exploited.

## 2) Mutable Git Tagging

* We as developers are normally told to pin dependencies to latest (e.g., @v0.12.3) however, Git tags are mutable and anyone with write access to the upstream repo can force-push a tag to point to a completely different (malicious) commit, and your workflow file looks completely unchanged . **The only truly immutable reference is a full commit SHA** (e.g., `trivy-action@a1b2c3d4e5f6...`)
* Some mitigations are as follows:
  * Monitor outbound network connections from CI runners to suspicious domains.
  * Pin GitHub Actions to **full commit SHAs** instead of version strings which can be modified.

## Fixes and Considerations

* CI/CD vulnerabilties are pretty new for me but Endor Labs [1] gave some suggestions on what to check for and mitigations against this type of credential exfiltration and unintentional vulnerabilities.
* An interesting perspective that was mentioned was that GitHub actions should be considered dependencies and components given the same scrutiny as typically dependencies components brought installed for your application normally.