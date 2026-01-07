![700](images/SDLC.jpg.webp)

## What is SDLC
Software Development Life Cycle (SDLC) is a process used by the software industry to design, develop and test high quality software with **cost-effective** and **time-efficient**. SDLC aims to provide a **structured** and **systematic** approach to the development of software systems.

In the above, we define SDLC as a _process_. This leads to questions like, “How does SDLC work?” and “Are there distinct phases or steps within the SDLC process?”. We will discuss and analyse these questions later, but for now, I’d like to provide you with a summary of the information.

In SDLC we have **7 phase** (“Some articles state that there are six phases in the SDLC. Don't worry, they combine the ‘analysis’ and ‘defining requirements’ phases into a single phase) and each phase has vital role on the process. Let’s take a look at these phases.

![600](images/SDLCPhases.png)

- Planning(Requirement Analysis)  
	- **Roles**: Product Owner, Product Manager, Business Analyst, CEO…
- Define Requirements  
	- **Roles**: Business Analyst, Project Manager, System Architect, Developers, QA professionals…
- Design  
	- **Roles**: System Architect, UI/UX Designer, Software Designers, Database Designers, QA professionals, Network Architects…
- Development  
	- **Roles**: Front-End Developers, Back-End Developers, Database Administrators…
- Testing  
	- **Roles**: QA Testers, Automation Test Engineers, User Acceptance Testers, Test Analysts…
- Deployment  
	- **Roles**: Release Managers, Deployment Engineers, System Administrators, Operations and Support Teams, Backup and Recovery Specialists…
- Maintenance  
	- **Roles**: Support and Help Desk Teams, QA Teams…
	

> ! These roles may vary depending on the size and needs of the company !
> Business Analysts and QA professionals can join entire phases.

## How SDLC works?
SDLC divides the entire Software application development process into seven phases. Let's take a look.

![600](images/planningSdlc.webp)

### STEP 1 : Planning and Requirement Analysis

As you can see, Requirement Analysis is the first activity in SDLC. In this phase, the focus is on understanding the **project’s objectives**, identifying **stakeholder needs**, and setting the **project’s direction.**

Requirement Analysis can be examined in 3 step

**1- Requirement gathering**
It is often referred to as _elicitation._ In this section, you must gather clear, concise, and correct customer requirements. Let the customer define their needs adequately, and the business analyst collects them as the customer/stakeholders wants.

Taking notes of the requirements in a clear and understandable way in this section will prevent errors that may occur later in the process.

**2- Analysing**
This process is essential for ensuring that the software development project is well-defined and that the resulting software product will meet the needs and expectations of the end users. In this section, concepts such as _Requirements Validation_, _Categorization_, _Prioritization_ are answered in detail.

**3- Documentation**
It involves creating detailed records and reports to capture essential information and decisions related to the project. This step creates a summary for the next step.


### STEP 2: Defining Requirements

Research shows that 68% of IT projects fail, and one of the main reasons for this is the poor initial definition of requirements. Before proceeding with defining requirements, it’s essential to _review_ and _validate_ the requirements gathered in the previous phase. This involves confirming that the requirements are clear, complete, and aligned with the project’s objectives. Any inconsistencies or ambiguities should be addressed.

The main focus of the Defining Requirements phase in the Software Development Life Cycle (SDLC) is to precisely and comprehensively specify what the software **must accomplish**. This phase aims to create a _clear_ and _unambiguous_ understanding of the project’s requirements, including both functional and non-functional aspects.

Separating requirements into functional and non-functional categories during the defining phase enhances developer performance. This improved performance contributes to achieving **better results**.

Let’s categorize the requirements into functional and non-functional.

#### Functional Requirements
Functional requirements are specific criteria and descriptions that define the functions or features that a software system, application, or product must perform. They describe what the software is expected to do to meet the needs of users and stakeholders.

Here some examples..

1. User Authentication: A functional requirement for a web application might specify that users must be able to register for an account, log in with their credentials, and reset their password if forgotten. It would also describe the rules and criteria for password creation, login attempts, and user account management.
2. Online Shopping Cart: For an e-commerce website, a functional requirement might state that users should be able to add products to their shopping cart, update quantities, remove items, and proceed to the checkout process. It would detail the steps and interactions required to make a purchase.
3. Search Functionality: A functional requirement for a search engine might outline the ability to enter search queries, perform searches across a database of indexed content, display search results, and allow users to refine their searches with filters or sorting options. It would specify the behavior and functionality of the search feature.

#### Non-Functional Requirements
Non-functional requirements, often referred to as quality attributes or performance requirements, specify how a software system should perform rather than what it should do. These requirements address characteristics related to system behavior, user experience, and performance.

- Performance
- Security
- Scalability
- Usability
- Reliability

Non-functional requirements are crucial because they ensure that the software not only functions correctly but also meets user expectations for performance, security, and overall quality. These requirements help guide design, development, and testing activities to deliver a software system that performs well and provides a positive user experience.


## STEP 3: Design
We have completed the requirements in the previous phases, now we need to design them and move them to the development phase. Its primary purpose is to transform all the requirements into complete, detailed system design specifications.

#### Technical-Architect, Tech-Designer, Design Team
They design the system architecture, software components, etc., along with the design walk-through.

#### Developer/ Construction Team
They assist in finalizing the data conversion strategy. Plus, also reviewing the architecture and the software components.

#### Testing Team/ Tester
They assist with identifying and finalizing the testing strategy. Plus, reviewing the architecture and software components.

#### Database Team
The database team assists with architecture design and data conversion strategy.

#### UI/UX designers
Have key responsibilities during this phase to ensure that the software is not only functional but also user-friendly and visually appealing.


## STEP 4: Development
The Development Phase’s primary purpose is to convert the system design prototyped in the Design Phase into a working information system that addresses all the documented system requirements. In the end, the operating system enters the Testing Phase.

> It’s a critical phase where the software goes from the design on paper to a working product.

Here some responsibilities of the development team:
- Coding
- Modular Development
- Code Review
- Unit Testing
- API Development
- Error Handling and Logging
- Adherence to Coding Standards…

## STEP 5: Testing
Testing starts as soon as programming is finished and the components are made accessible for testing. During this step, the software is thoroughly assessed, and any defects are given to engineers to fix.

Until the software satisfies customer requirements, additional testing and bug fixing are conducted. Testers refer to the software requirements specifications to make sure the software complies with the client’s criteria.

Test Planning, Test Case Design, Test Data Preparation, Test Environment Setup, Manual Testing, Automated Testing. These are some test step operations.

## STEP 6: Deployment
Depending on the customer’s expectations, the product may first undergo UAT (User Acceptance Testing) before being released into the manufacturing process.

When using UAT, a copy of the production environment is made, and the client and programmers test the software together. The consumer must provide their approval for the app to go online if they find it to be what they expected.


## STEP 7: Maintenance
After a product has been deployed in a manufacturing process, the developers are responsible for maintaining the product, taking care of any issues that need to be resolved or enhancements that need to be made.

---
*To be continued, as we explore the next phase in the journey of software development.*  
*Stay tuned for my upcoming article, where we will delve into the key modules and methodologies of the Software Development Life Cycle (SDLC).*