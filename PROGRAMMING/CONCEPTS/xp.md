# Extreme Programming (XP)

[Extreme Programming](https://en.wikipedia.org/wiki/Extreme_programming) (XP) is a software development methodology intended to improve software quality and responsiveness to changing customer requirements. As a type of agile software development, it advocates frequent releases in short development cycles, intended to improve productivity and introduce checkpoints at which new customer requirements can be adopted.

Currently, I'm reading *XP Explained* by Kent Beck. The basic tenets are as follows:
* XP is a lightweight, efficient, low-risk, and flexible way to produce software.
* It focuses on continuous feedback from short cycles.
* Incremental planning of features.
* Flexibility in scheduling and implementation of functionality.
* It focuses heavily on automated tests (e.g., JUnit5 for backend, Jest for frontend testing). **Writing tests for your applications developed via XP is non-negotiable; if you don't write tests, then you aren't doing XP!**
* It relies on the close **collaboration of programmers with ordinary skills**.
* Other elements of XP include: programming in pairs, extensive code review (pairing is essentially continuous code review), not programming features until they are actually needed, a flat management structure, code simplicity and clarity, and frequent communication with the customer.
* The methodology takes its name from the idea that the beneficial elements of traditional software engineering practices are taken to "extreme" levels.

## Manifesto for Agile Development

* https://agilemanifesto.org/
* **Individuals and interactions** over processes and tools
* **Working software** over comprehensive documentation
* **Customer collaboration** over contract negotiation
* **Responding to change** over following a plan

> [!NOTE]
> While there is value in the items on the right, we value the items on the left more.

## Development Principles

### Don't Repeat Yourself (DRY)
* Extracting repeatable functions and logic to make them modular and reusable across your application.
* *Goal:* Reduce technical debt by ensuring that a change in business logic only needs to be updated in one place.

### You Ain't Gonna Need It (YAGNI)
* Write the minimum functionality POSSIBLE to accomplish the immediate goal.
* **Lean slice:** Build strictly to the specifications of what is needed *right now*.
* Skip building out "future-proof" features until there is an actual business requirement for them.
* Write code for today's problems, not tomorrow's hypothetical problems.

### Tell - Don't Ask
* Tell objects what to do, don't ask them about their state to make decisions for them outside of the object.
* Call methods that perform actions *inside* the objects themselves.
* *Why:* It keeps data and the logic that operates on that data bound closely together, reducing loose coupling and massive `if-else` chains in your main application flow.

### SOLID Principles
* **Single Responsibility Principle (SRP):** A class should only have one reason to change, splitting large classes into smaller, focused ones.
  * *E.g.,* If a class is over a certain amount of lines in length, or handles both database saves and UI rendering, split it.
  * *E.g.,* In Linked Lists: The `Node` class only cares about holding data and a pointer, while the `LinkedList` class handles the insertion/deletion logic.
* **Open-Closed Principle (OCP):** Software entities should be open for extension, but closed for modification. Promotes stability and preserves tested behavior.
  * *E.g.,* Extending functionality by adding new classes or overloading methods, without altering the existing, working internal code of the parent. Avoids breaking existing dependencies.
* **Liskov Substitution Principle (LSP):** A superclass should be replaceable with objects of a subclass without affecting the correctness of the program. The minimum functionality for something to work should be inside the parent, and all subclasses can inherit and safely be used in its place.
  * *E.g.,* `AccStudent` (has an ACC ID, email, name). The subclasses (`SwfAccStudent`, `TraditionalAccStudent`, `NonTraditionalAccStudent`) all extend the base `AccStudent`. If a function expects an `AccStudent`, passing it a `SwfAccStudent` shouldn't crash the program.
* **Interface Segregation Principle (ISP):** Clients should not be forced to depend on interfaces they do not use. Keep interfaces small, specific, and relevant.
  * *E.g.,* Instead of one giant `IWorker` interface with `work()`, `eat()`, and `sleep()` methods, split it into `IWorkable`, `IEatable`, and `ISleepable`. This way, if you create a `Robot` class, it only has to implement `IWorkable` and isn't forced to write a useless, empty `eat()` method.
* **Dependency Inversion Principle (DIP):** High-level modules should not depend on low-level modules; both should depend on abstractions (interfaces).
  * *E.g.,* Your `PaymentProcessor` class shouldn't depend directly on a hardcoded `StripeAPI` class. Instead, it should depend on a generic `PaymentGateway` interface. This makes it trivial to swap Stripe for PayPal later, or to mock the database/API during testing.

# Pairing Practices

## What is Pairing?
* Pair programming is an agile software development technique where two developers work together at a single workstation (or shared screen). One types the code while the other actively reviews, strategizes, and checks for defects. It is essentially real-time, continuous code review and knowledge sharing.

## Types of Pairing
* **Discipline Pairing:** Pairing within your own discipline. Two people of the same role (e.g., two backend engineers) work on the same problem at the same time on the same machine.
* **Cross-Discipline Pairing:** Pairing with people in different disciplines (e.g., a Developer pairing with a Product Designer, QA, or UI/UX engineer) to bridge the gap between design, testing, and implementation.

> [!NOTE]
> Pairing on a single feature is good, but rotating pairs across multiple features (Promiscuous Pairing) is better. The big issue with static pairs is the **lack of shared context**. Rotating developers ensures that knowledge of the codebase spreads across the entire team, preventing knowledge silos and single points of failure.

## Techniques to Try
* **Driver and Navigator:** The standard setup. The **Driver** controls the keyboard and focuses on the micro (syntax, typing, immediate logic). The **Navigator** observes, focuses on the macro (architecture, spotting bugs, thinking about the next test), and guides the direction.
* **Ping Pong:** Heavily tied to Test-Driven Development (TDD). Developer A writes a failing test (Red). Developer B takes the keyboard, writes the code to pass it (Green), and then writes the next failing test (Red) before passing the keyboard back. Keeps both devs highly engaged.
* **Tour Guide:** A variation of Driver/Navigator usually meant for onboarding or domain exploration. The Navigator (a senior dev or domain expert) acts as a "tour guide," explicitly guiding the Driver (a junior dev or someone new to the codebase) step-by-step through a complex system.
* **Pomodoro:** Time-based pairing. Short, intense bursts of work (e.g., 25 minutes of focused pairing followed by a 5-minute break). You layer this timing method on top of another technique (like Ping Pong) to prevent mental fatigue.
* **Task List:** Pairing guided by a highly specific checklist of subtasks. Instead of swapping based on an arbitrary timer, developers swap roles every time a specific subtask or test is completed.

> [!NOTE]
> The best process is the process that works for your team!
> The best technique is the one that works for you and your pair. Communicate early and often about what is and isn't working.

__**START HERE**__

## Pairing with Design

* Pairing with Design to create a mid-fi mock up in Figma
* Simply using gray-scale to avoid over-complicating the mock-up
* Only including features that have actually been user-tested

# User Stories

> [!NOTE]
> Basically this serves as a way to focus on what ACTUALLY produces value.
> From the Lean Start Up it's used to focus developer time (the most precious resource),
> It's no longer a question of can it be built, it's a question of SHOULD IT BE BUILT.
> It's like TDD for the meta-view of features.

* Used to narrow and determine what actually needs to be accomplished.

* Technical Stories
* Chores: Task that are necessary, but provide no direct or obvious value to the user (e.g., logging, authentication)
  * Spikes: area of technical investigation, not sure how we're going to implement it, but we're going to play with it. **Feature-find** (similar to Blue-Green testing)

* **Bugs**
  * Where found
  * How found
  * What was the expected behavior
  * What I observed
  * Can you reproduce it/verifiable

## Gherkin Modeling
* [Gherkin Modeling](https://medium.com/@nic/writing-user-stories-with-gherkin-dda63461b1d2)

* User Story (Why we are building the thing??)
  * The Why - user action
  * As a "user/persona" - persona name
  * I want "action" - to accomplish a task using this product/soltion
  * So that "outcome" - something about the users life outside the product/solution changes for the better.

* Acceptance Criteria (The How and Acceptance Criteria):
  * **Given** (how things begin)
  * **When** (action taken)
  * **Then** (outcome of taking action)
  * **And** (can be used at any stage to ensure that you are building and designing the right feature)**

* The who, what, and why of a feature. Intentionality of your choices!

### Instrumentation
* What is the thing that we are trying to implement SO THAT we learn if its  being used in teh way we assume?
  * Here we link to design files
  * Decisions the team has made related to the story
  * Outstanding questions that team needs to answer
  * Anything else the team finds noteworthy

> [!NOTE]
> Don't immediately look to build a software solution when a simple process update is much more efficient!

# Balanced Team

* A balanced team typically comprises includes a product manager (PM), designer, developer, and platform engineer (PE). Each provide different perspectives and contribute to the idea of a balanced and dynamic team.
* The caveat here is that each role can be adopted/inherited by other roles, for example, a Platform Engineer is able to also assume PM duties in the event that the original PM is away or is unable to make a application decision.
* There's another idea/heuristic of using **desire (designer)**, **technical feasibility (PE and developer)**, and **viability (PM)** to address specific aspects of the balanced team.
* All aspects of the balanced team should work in tandem (e.g., Venn diagram )

## Designers
* Focus on the UI/UX of the thing that you are building, the emphasis here is on the end user via user centered design (UCD) (identification of direct pain points that the user may face).
* The goal of the designer is to hold the individual sacrosanct in the development process and ensure that the features that are being added discrete value to the end user above all else.

## PMs
* Focus on the direction and larger picture of the application/product, their job is to see "the forest from the trees" and provide direction for the project.
* The interact and are the direct touch point between the stakeholder, customer, and the balanced team.
* They are the internal advocates for the team and work with external environment to safegaurd the team from excessive bureaucracy that adds unnecessary complexity to the development environment.

## Devs
* Sanity check, provide feasibility and technical ability and feasibility.
* How to extract the essence and basics of implementation.
* Identify the need for more technical research.

## Standup Basic Elements

### "3" Qs
* What did I do yesterday?
* What am I doing today?
* What blockers do I have?

### Reviewing as Pairs
* What did the pair accomplish yesterday?
* What blockers did the pair have?
* What is the pair planning to do today?

## Iteration Planning Meeting (IPM)

Yesterday I also learned about iterative planning meetings (IPMs) and how they influence #Prioritization or what needs to be worked on and how proper prioritization contributes to higher quality #Metrics like time it takes to deliver of features.

* The goal of pre-IPMs and IPM as they relate to the balanced team is to bring the entire balanced team together to identify, prioritize, approximate complexity, and ultimately rank order how work should be completed. 
* Pre-IPM and IPM is set during team norming and each typically happens at least once per week (**NOTE:** this can be modified to as development after inception takes place) but at a bare minimum it should occur at least once per week so that work can be prioritized and accounted for.
* My initial thought when norming on this idea was, "oh great, another meeting that gets in the way of actually learning and building...", but after some discussion I realized that it's essential and non-negotiable for an efficient balanced team.
* The idea that comes to mind is "measure twice and cut once". If engineering and building time is valuable, and you want to extract the most value out of each team without overworking the team, YOU HAVE TO PRIORITIZE AND IDENTIFY THE MOST VALUABLE USE OF THE TEAMS TIME. 
* From what I currently know about how a balance team operates, this is one of the best ways bring all parties and opinions to the table. In more traditional work environments, engineers are brought into the planning process after what management and other members determine what is important and simply give engineers that work to be done. The builders of the product are not taken into account and complexity of what's being built is not identified by the managers of the team leading to unrealistic product timelines and #Metrics related to estimations of project/feature completion great skewed and inaccurate.

# Facilitating Retrospectives (Retros)

1) Make your work visible - meaning that during team norming you provide space for your team to see/hear about the work that you've completed (e.g., the previous 24 hours). To me, this ensures that each individual is held accountable for the work that they are doing.
2) Ensure that you have retrospectives - from what I've heard, this is part of the norming process whereby the team gets together to decide what the consistent patterns they will follow (e.g., morning and evening standup times, tempo of retros, determining success criteria for the retro that's agreed upon, etc.). It's essentially a ritual gathering at the end of a project to review events and learn from actions taken... 

* Warm-up Games
* Essentially a reflection (at regular intervals) that you take with your team to reflect on how the team is doing (e.g., once per week or at the end of a project...)
* It serves to **fix the thing when it breaks**, you want to take it apart and do it again. Basically the idea of an internal teams [andon cord](https://en.wikipedia.org/wiki/Andon_(manufacturing)).

**Question** During a retro, how do you avoid the dilemma of having learning as a goal when you fail?

* It's okay if "**learning**" is the goal here, the retros are incremental and should enable you to learn incrementally.

## Feedback and Retrospectives

1) Set the Stage
2) Gather Data
3) Generate Insights
4) Decide What To Do
5) Close the Retro

### Set the Stage
* Use some form of mantra or shared agreement of radical open-ness about the purpose of this project
* Determine success criteria for the retro that's agreed upon

### Gather Data
* Starfish
* Future-spective: where you position yourself as if you are in the future and looking back on the items that you want to learn...
* Before you start discussing your ideas, gather then silently (silent writing)

### Generate Insights
* Draw a picture of the last iteration (used to create an image of how the previous project worked).
* What is your understanding of what X is saying?
* How do you understand the situation?
* Root-cause analysis

> [!NOTE]
> Don't blame the end user, it's difficult to diagnose a single systematic cause due to the complexity)

* Are you willing ot support the proposal?
* What concerns, if any, do you have about supporting the decision?
* Is this a decision you can support and implement
* Close with appreciations (what did people in the group get right)

#### Truth Seeking Methodologies

I was recently doing some thinking about how some of the greatest entrepreneurs use #Facilitation, or at least extreme versions of it, to move forward with the product that they are buidling. Specifically I recall learning about Jeff Bezos' mentality when it comes to handling disagreement within groups aptly named, "Truth Seeking Methodologies". He goes into explaining his approach to this in the following ways:  
1) **Truth over Consensus** - meaning that when objective facts are knowable, you should never compromise. For example, if you think a ceiling is 11 feet and a colleague thinks it is 12 feet, compromising at 11.5 feet is incorrect. Using a tape measure to find the absolute truth is the only acceptable method. An example that comes to mind is the process of #Prioritization during pre-IPM and IPM sessions. The purpose of each of the sessions is to identify, rank order, and ruthlessly organize the backlog of task to be done with all members of the balanced team. If there is some ambiguity with a specific deadline coming up for delivery of an MVP along with the complexity of what it takes to accomplish a feature, rather than guess about the deadline, we should identify the specific and agreed upon deadline along with using some User Story estimation using the ranking of 1 = Good to go, TFB = too freaking big, and NFC = no freaking clue.

2) **Disagree and Commit** - in the event that a definitive truth cannot be measured, such as a subjective strategy choice or direction and path for an application, and a colleague disagrees with you, Bezos suggests the idea of "disagree and commit". Instead of watering the idea down through compromise, the dissenting party acknowledges the opposing view, fully commits their energy to executing the decision, and allows the team to move forward with 100% commitment. What's useful is: 1) the team is able to rapidly in one direction and 2) quickly pivot if the direction is incorrect. 

3) **Embrace Exhausting Debate** - Lastly, Bezos believes that you should not compromise for the sake of "social cohesion". He actively encourages lengthy, passionate, and sometimes exhausting arguments (arguments here don't mean that someone is disrespectful). He demands that teams hash out every angle of a problem until the strongest evidence-based path becomes clear. Obviously, when working within a balanced team and your using #Facilitation to iron the performance, the mediator shouldn't be the one in heated discussion, but should work with the team to direct the conversation in a respectful manner.

#### Preparation Checklist for Facilitation

* Validate your selection as facilitator (am I the right one for the job??)
* Check in with the team (is there any context that I'm missing??)
* Ensure time and date
* Make a lightweight plan

## Retrospective Extended Learning
* Project Retrospectives
* Agile Retrospectives
* Retrospective Antipatterns

# Estimating 

(#Metrics, #Prioritization)

* Estimating is quite difficult in product development and management. Some common ways to get around this issue is to use a **Flow Efficiency** calculation which is the ratio of the total time spent in value-added work activities **`Active Time`** divided by the total flow time **`Total Lead Time`**.

* Active Time: The actual time spent actively working on or adding value to the item (e.g., coding, testing, designing).
* Total Lead Time: The entire elapsed calendar time from the moment work begins to the point of delivery. This includes active **work time**, **wait time**, **blocked time**, and **time spent in queues**.
  * Wait Time: The invisible downtime where the work is idle (e.g., waiting for code reviews, approvals, environment provisioning, or dependency handoffs). Essentially all the time spent not working on adding value.

There's also the idea of User Story estimation:
**Use when in earlier into the development process, or you're with a new team...**
* 1 = Good to go 
* TFB = "too freakin' big" and the story can be split into leaner slices 
* NFC = "no freakin' clue" and the story requires more research or a spike before it can be estimated or worked on

**Fibonacci Estimation or T-shirt Estimation... use when you have worked with you team for a longer period of time, and you're accustomed to the velocity of the output and can better intuit what you and your team can produce.**

## Volatility, Uncertainty, Complexity, and Ambiguity (VUCA)

* Ref: https://www.pmi.org/disciplined-agile/vuca-volatility-uncertainty-complexity-and-ambiguity

* Another aspect seen in estimation is VUCA which is a selection of variables that surrounds the knowledge work that is performed. 
* **Volatility**: is the dynamic rate of change. As the pace of our world increases, what we need to do to be effective in it is constantly changing. 
* **Uncertainty**: is the lack of predictability and information. It is the “fog of war” we face. While it would be nice to have clarity on what to do, we rarely know what our customers want and what our competitors are doing and how they will respond. 
* **Complexity**: describes interdependent systems that do not have apparent cause and effect. Your company, your clients, and even your competitors comprise a system that interacts with each other, but for which many of the relationships can’t be seen or well understood. 
* **Ambiguity**: acknowledges the challenge we have in understanding and assessing reality. It is hard to know what is going on and what we need to do to improve it.

# Discovery and Framing

1. Problems
2. Prioritize
3. Solutions
4. Prioritize


**__START HERE__**

## How Might We (HMW) / How Might We Not (HMWN)

(#BalancedTeam, #Facilitation)

* We recently discussed this idea of HMW and HMWN as it relates to DNF, identifying the next steps forward for development after midpoint, and general problem-solving/brainstorming of ideas in general.
* The main advantage of this technique is that it enables the entire team to contribute any and all broad ideas (e.g., idea storming) towards a single goal.
* It seems to be the most helpful at beginning points before a new development sprint or general initiative begins and benefits the most from divergent thinking.

## Usability Testing

* Normally all you need is ~5 tests to fix ~70% of issues with a product...
* When using usability tests you want to be less prescriptive and ensure that the task is more goal oriented that captures subtleties that the user may experience.

### Findings and Synthesis

* Normally, this form of synthesis is done during usability testing.

* Red = Fail
* Green = Pass
* Blue = Insight
* Violet = Feature Request

* Qualitative vs. Quantitative Testing
  * The riskiness dictates which form and level of testing is needed (e.g., high risk = quantitative; low-risk = qualitative)

* Sacrificial Testing: the idea during the usability test where you introduce an idea not covered inside of the completed usability test that you can use to  introduce new ideas.

> [!NOTE]
> When doing testing, do not use the actual terminology used within your system to direct the user. The user will hunt for that key word rather than acting naturally... (e.g., use "how would you **access** the system vs how would you **log in** to the system.)