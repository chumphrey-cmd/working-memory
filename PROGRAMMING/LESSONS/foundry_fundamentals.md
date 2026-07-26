# Ontology (Information Science)

* https://en.wikipedia.org/wiki/Ontology_(information_science)
**Ontology:** In information science, an ontology encompasses **a representation, formal naming, and definitions of the categories, properties, and relations between the concepts, data, or entities that pertain to one, many, or all domains of discourse**. More simply, an ontology is a way of showing the properties of a subject area and how they are related, by defining a set of terms and relational expressions that represent the entities in that subject area. 
* Effectively, it's a way to represent the relationships between objects and entities within a system. It's a way to create a controlled and shared vocabulary/terminology within a system that are easily understood by people internal and external to the domain (Thinking in Systems). 

# Ontology (Philosophy)

* https://en.wikipedia.org/wiki/Ontology
Ontology is the philosophical study of being. It is traditionally understood as the subdiscipline of metaphysics focused on the most general features of reality. As one of the most fundamental concepts, being encompasses all of reality and every entity within it. To articulate the basic structure of being, ontology examines the shared characteristics among all things and investigates their classification into basic types, such as the categories of particulars and universals.

# Architecture

> [!NOTE]
> The direct problem that it solves is making all non-normalized streaming content easily accessible, parse-able, and much more (very hard problem to solve)

### Outcome Layer (Top - North)
**WORKSHOP (NO-CODE PROTOTYPING PLAYGROUND)**
* Here we are effectively taking the normalized parsed and cleaned data to create visualization (e.g., the same way that Elastic Dashboards operate)

### Ontology Layer (Middle)
**ONTOLOGY MANAGER**
* Handles the class definitions of every object

* Creates the abstraction and extraction of similarities between objects (basically abstracted OOP [inheritance, polymorphism, abstraction, encapsulation, etc.], common entities across ingested data)
* Essentially, creating Entities/Representations of the raw data that you've created (Human, Student, Team, etc. based on the raw data that you've created).
  * Object Type
  * Action (Verbs)
  * Link: JOINs
  * Function (Pivot Tables in SQL) 
  * Automate: set of actions that (functions/cron) that run on the ingested data set as new data is uploaded.
    * This may also be where streaming comes in to ingest real time data into the application (IDK how this works, but I think that this is where that happens...)

### Data Layer (Bottom - South)
**PIPELINE BUILDER/MANUAL PARSING**

* Raw unparsed, non-normalized, free text, generally unstructured, manually uploads, etc.
    * Protocols and out of the box connectors for all data types (e.g., REST, JDBC, SFTP, file upload, etc.)
    * Include logic sources,

## General Vantage/Foundry Workflow
* Find problem that needs to be optimized
* Verify that the data is present inside of Vantage Data Marketplace
* Create Project
* Upload or find the data from within the Data Marketplace
* Clean and normalize data (Pipeline)
* Ontology Manager > Access the data that you just generated

## Artificial Intelligence Platform (AIP)
* AI FDE (customizable agent): 
  * The advantage here is the ability to customize and configure the system prompt and harness that the agent should operate. 
  * Used to build pipelines, create and edit objects, debug, etc.

### Agent Development Workflow

> [!IMPORTANT]
> Something that I realized is the importance of modifying "North of the Ontology". You want to grab the most fundamental building block (ontology) and then begin to modify and manipulate.

* **AIP FDE: the de-facto standard captures a lot of the functionality of the tools (generalist)**
* **AIP Logic: different session work internal to AI FDE**
* **AIP Evals: the testing for the agentic plane, use as a way to make the application deterministic**
* **AIP Analyst: useful for all things related to data analysis**
* AIP Machinery: essentially Miro and allows you to coordinate a reusable and component based tool.
* AIP Pilot: useful for quick prototypes
* AIP Assist: doc focused regarding the direct documentation provided from the Docs
* AIP Continue: basically cursor; will be discontinued

# Qs/Random Ideas
* How does the abstraction of the software that Palantir provides assist software developers?
* Is there a danger to a degradation of skill set and problem-solving?
* Who retains the normalized data that is ingested inside Palantir (probably Palantir)?
* If I wanted to scan or deploy a security agent to scan source code, is this possible within Foundry for Vantage/Foundry native applications?

> [!NOTE]
> Another random idea that I just thought of is that Technical Palantir Low-Level Platform Developers > Palantir FDE (work natively inside Foundry) > ASWF Devs > Army Soldiers
> Effectively, it's the attempt to get as close to the bare-metal/as close to the customers as possible.
> **Strategic inflection point:** if the product that you've made is potentially commercially viable, you will be unable to remove that application from the platform (massive vendor lock in)...
> Essentially, context engineering and orchestrating of the right kinds of data that are needed (chaining together logical steps) 