## ITIL = IT Infrastructure library

## Basis begrippen:

**Business**: activiteit van het bedrijf
**Core Business:** Kern activiteit van het bedrijf
**Business Case**: analyse om te beslissen om het te doen of niet te doen. bekijken wat zijn de kosten en wat brengt het mij op.
**ICT business enabler:** -> ondersteunende dienst voor de business

**RoI**: Return on investment
**KPI:** Key Performance Indicators
#### SLA
Service level agreement
#### XLA
Experience Level Agreement
#### P&L
Profit and Los - Is an indicator hoeveel de geleverde service kost and wat de klant betaald voor het contract.
#### Prioriteit = Impact x Urgentie

#### CMDB = configuration Management Database
CI = configuration Item = Asset

## Hoe kunnen we service deliveren?
We gebruiken het ITIL framework om onze service organisatie in te richten.
### IT service framework with 4P's

In order to organise you ITSM you need to take 4 pillars into account.

#### Process
Define how work flows, who does what, and in what order.
#### People
Make sure you have the right skilled workforce, good communicators, tech, skills, interaction with customers.
#### Partner
Suppliers, vendors, distributors, resellers, and other third-party service providers.
#### Product
Make use of the right tools and infrastructure

A strong **Process** relies on competent **People** using effective **Products** and leveraging valuable **Partners** to consistently deliver high-quality services that meet customer needs and drive business value.


### SPOC
Single Point Of Contact -> centrale helpdesk

Different types of incoming service demands:
- Call center -> phone focus, dispatching , inbound, outbound (surveys)
	- inbound -> helpdesk
	- outbound -> mensen opbellen
	- Alle inkomende incidents doorsturen , niets zelf oplossen- inbound -> helpdesk
- Helpdesk -> try to help the customer with procedures + dispatching to other teams
- Service Desk -> delivering a service, zoveel mogelijk zelf oplossen.
- Skilled service Desk -> maximaal problemen trachten op te lossen.
	- maximize shift to the left:
		- zoveel mogelijk problemen trachten op te lossen bij het eerste klanten contact

#### Types of escalation
##### Functional escalation:
-> hogerop gaan in de hierarchie

##### Horizontal escalation:
-> naar een andere lijn 1ste lijn naar 2de lijn naar 3de lijn.
bijvoorbeeld een ticket wordt doorgeschoven van een andere IT specialist, kan ook binnen dezelfde lijn eventueel.

## ITIL Practices

### **1. Incident Management**

- **Purpose:** To restore normal service operation as quickly as possible and minimize the adverse impact on business operations, thus ensuring the best possible levels of service quality and availability.
#### What is an incident:
- eenmalig probleem
- verstoring van de service
	- volledig weg of degradatie van de qualiteit
#### Option to solve the incident:
--> zo snel mogelijk oplossen
- workaround - een alternative bieden om het incident op te lossen.
- permanente / structurele oplossing
    
- **Key Activities:**
    - **Incident Identification & Logging:** Detecting incidents (e.g., system down, slow performance) and recording all relevant details.
    - **Categorization & Prioritization:** Classifying the incident (e.g., by service, impact, urgency) to determine its severity and who should address it.
    - **Diagnosis & Resolution:** Investigating the root cause of the incident and applying a workaround or permanent fix.
    - **Closure:** Verifying with the user that the service has been restored and formally closing the incident record.
    - **Escalation:** Raising an incident to a higher level of support or management if it cannot be resolved within agreed-upon timeframes or requires additional resources.

### **2. Problem Management**

- **Purpose:** To reduce the likelihood and impact of incidents by identifying and analyzing the root causes of recurring incidents and preventing future incidents.
#### What
- Wederkerig soortgelijk service verstoring
- Een problem kan ook komen pro-active zoals een bug gerapporteerd van de vendor
#### How
- RCA - Root cause analysis -> de oorzaak vinden is nodig om de juiste oplossing te vinden.
	- structurele oplossing zoeken :5 why methodology kan gebruikt worden om de root cause te vinden.
	- Known error - gekend probleem, known errors blijven open staan. indien er een nieuw incident wordt gemeld moet dit dan aan de known error gekoppeld worden.
		- kosten baten
		- we kennen de oorzaak nog niet

- **Key Activities:**
    - **Problem Identification:** Detecting problems, often by analyzing incident records, major incidents, or through proactive trend analysis.
    - **Problem Categorization & Prioritization:** Classifying the problem to determine its severity and potential impact.
    - **Root Cause Analysis:** Investigating the underlying reason for incidents (e.g., using techniques like 5 Whys, Fishbone diagrams).
    - **Workaround Documentation:** Developing temporary solutions to restore service quickly while a permanent fix is being found.
    - **Error Control:** Managing the lifecycle of known errors and ensuring that permanent solutions are implemented.
    - **Problem Resolution & Review:** Implementing permanent solutions and reviewing their effectiveness.

### **3. Service Request Management**

- **Purpose:** To support the agreed quality of a service by handling all pre-defined user-initiated service requests in an effective and user-friendly manner. These are typically standard, low-risk, and frequently occurring requests (e.g., password reset, software installation).

#### Types of requests
Standard
- RFI request for information "best effort" bepaald door de scope, voor welke vragen kan je binnen bellen
security
- alle aanvragen aangaande rechten, security
Klachten
- klanten tevredenheid
- aangaande
#### Key Activities:
- Service Request Logging: Receiving and recording requests from users, often through a self-service portal.
- Fulfillment: Carrying out the requested service, which may involve automated processes or manual tasks.
- Monitoring: Tracking the progress of the service request.
- Communication: Keeping the user informed about the status of their request.
- Closure: Confirming with the user that the request has been fulfilled.
### **4. Change Management**

- **Purpose:** To maximize the number of successful service and product changes by ensuring that risks have been properly assessed, authorizing changes, and managing a change schedule. It aims to minimize the negative impact of changes on services.
#### What
- Aanpassing aan service, product, process of procedure
- Add, edit, delete
#### Types
- Standaard change - er is een procedure beschreven om deze aanpassing te doen, dit is een laag risico en/of gekend. er is een fallback beschikbaar. vaak is deze change geautomatiseerd.
- Normal change - volgt de normale afhandeling.
- emergency change -> zelfde process als een normal change maar met dringendheid uit te voeren. de beslissing zal snel genomen worden.
#### C.A.B : Change advisory board
Team specialisten geleid door een CM (change manager) die zal bepalen of de change mag uitgevoerd worden en hoe dit zal gebeuren.

Change assignment wordt vervolgens aan de juiste specialist of team gegeven.
- planning opmaken wanneer de change kan worden uitgevoerd.
- communiceren wanneer de change kan worden uitgevoerd

#### **Key Activities:**
- **Change Request Submission:** Proposing and documenting a change (e.g., system upgrade, new software deployment).
- **Change Assessment & Justification:** Evaluating the necessity, benefits, and risks of the proposed change.
- **Change Authorization:** Obtaining approval from relevant stakeholders (e.g., Change Advisory Board - CAB).
- **Change Planning & Implementation:** Developing a plan for the change, including testing, communication, and rollback procedures, and then executing it.
- **Change Review & Closure:** Assessing the success of the change and ensuring it achieved its objectives without adverse effects.

##### OTAP
In the context of **service management** and specifically software development and IT operations, **OTAP** is a widely used acronym that refers to a standard sequence of environments for deploying and managing software applications. It stands for:

- **O**ntwikkeling (Development)
- **T**esten (Test)
- **A**cceptatie (Acceptance)
- **P**roductie (Production)

(You might also see it referred to as **DTAP** in English-speaking contexts, standing for Development, Test, Acceptance, Production).

This model ensures a structured and controlled progression of software changes from initial development through to the live, operational environment. Each environment serves a specific purpose:

1. **Ontwikkeling (Development) Environment:**
    - **Purpose:** This is where software engineers and developers write, debug, and initially test new code, features, or bug fixes. It's often a local environment on a developer's workstation or a shared development server.
    - **Characteristics:** Highly flexible, allows for rapid iteration and experimentation. Data is typically test data or dummy data. Changes are frequent and often individual.
2. **Testen (Test) Environment:**
    - **Purpose:** Once individual components or features are developed, they are integrated and deployed to the test environment. Here, automated tests (unit, integration, system tests) are run, and often functional testing is performed by a dedicated testing team.
    - **Characteristics:** Aims to mirror the production environment as closely as possible in terms of hardware, software, and data. It's used to identify defects, performance issues, and integration problems before they impact end-users.
3. **Acceptatie (Acceptance) Environment:**
    - **Purpose:** This is where the software is presented to the business users or stakeholders for User Acceptance Testing (UAT). The goal is to verify that the system meets the defined business requirements and that users can perform their tasks effectively. It's the final validation before going live.
    - **Characteristics:** Should be a near-exact replica of the production environment, including realistic data (often a masked copy of production data for privacy reasons). Non-technical users are actively involved in testing. Approval from business stakeholders is crucial here.
4. **Productie (Production) Environment:**
    - **Purpose:** This is the live, operational environment where the software or service is used by actual end-users or customers.
    - **Characteristics:** Designed for stability, performance, security, and reliability. Changes to this environment are highly controlled and typically follow strict change management processes. Data is live and real.

**Why is OTAP important in Service Management?**

The OTAP model is fundamental to effective service management because it:
- **Minimizes Risk:** By moving changes through a series of increasingly rigorous environments, it helps catch defects and issues early, preventing them from reaching the live production environment and causing service disruptions or incidents.
- **Ensures Quality:** Each stage has specific testing and validation criteria, contributing to the overall quality and reliability of the delivered service.
- **Facilitates Control:** It provides a structured process for managing changes, ensuring that only thoroughly tested and approved software is deployed to production. This aligns directly with ITIL's Change Management and Release Management practices.
- **Supports Collaboration:** It defines clear responsibilities and handoff points between development, testing, business, and operations teams.
- **Improves Predictability:** By following a repeatable process, the outcome of deployments becomes more predictable.

In essence, OTAP is a cornerstone of a robust IT service delivery pipeline, contributing significantly to service quality, availability, and overall customer satisfaction.

### **5. Monitoring and Event Management**

- **Purpose:** To systematically observe services and service components, and record and report selected changes of state identified as events. It identifies and prioritizes infrastructure, services, business processes, and information security events.

#### Event types:
- Informational: no action needed = GREEN LIGHT
- Warnings: als er potentieel een service incident kan gebeuren = ORANGE Light
- Exception: service is verstoord, incident creation mandatory = RED Light

- **Key Activities:**
    - **Monitoring Setup:** Configuring tools to track the performance, availability, and security of IT services and infrastructure.
    - **Event Detection:** Capturing real-time data from monitoring tools.
    - **Event Filtering & Correlation:** Distinguishing between normal operational events, informational events, and events that indicate an issue or potential incident.
    - **Event Classification & Response:** Determining the significance of an event and triggering appropriate actions (e.g., creating an incident, alerting a team, running an automated script).
    - **Reporting:** Providing insights into system performance and potential problems.

### **6. Release Management**

- **Purpose:** To make new and changed services and features available for use. It ensures that new or changed services are deployed successfully and that all necessary components (e.g., documentation, training) are in place.

- Release is de beschikbare versies van een product of programma
- nieuwe versie
- bug fix
- update
deployment is een bepaalde versie in productie nemen.
- deployment kan manueel of automatisch

- **Key Activities:**
    - **Release Planning:** Defining the scope and content of a release, including what changes will be deployed together.
    - **Release Building & Testing:** Assembling the release components and thoroughly testing them to ensure they function as expected and meet quality standards.
    - **Release Deployment:** Moving the release into the live environment.
    - **Validation & Verification:** Confirming that the deployed release works correctly in the operational environment.
    - **Support Handover:** Ensuring operations and support teams are ready to manage the new or changed service.

### **7. IT Asset Management (ITAM)**

- **Purpose:** To plan and manage the full lifecycle of all IT assets (hardware, software, licenses, cloud resources) to maximize value, control costs, manage risks, and support decision-making about purchase, reuse, and disposal.
    
- **Key Activities:**
    - **Asset Identification & Discovery:** Identifying and tracking all IT assets within the organization.
    - **Asset Tracking & Inventory:** Maintaining an accurate and up-to-date record of asset details (location, status, user, configuration).
    - **License Management:** Ensuring compliance with software licenses and optimizing license usage.
    - **Financial Management Integration:** Connecting asset data with financial information for budgeting and cost control.
    - **Lifecycle Management:** Managing assets from procurement to disposal, including maintenance and upgrades.

### **8. Financial Management of Services**

- **Purpose:** To support the organization's strategic and tactical decisions by providing financial data related to IT services. This includes budgeting, accounting, and charging for IT services to ensure cost-effectiveness and value for money.
    
- **Key Activities:**
    - **Budgeting:** Planning and controlling the financial resources required to provide services.
    - **IT Accounting:** Tracking and reporting on all IT expenditure and income.
    - **Charging/Showback:** Developing a clear model for charging business units or customers for IT services, or at least showing them the cost of the services they consume (showback).
    - **Cost Optimization:** Identifying opportunities to reduce IT costs without compromising service quality.
    - **Value Assessment:** Demonstrating the financial value of IT services to the business.

### 9. Continual Improvement
- 5WHY
- **PDCA Cycle:** The Plan-Do-Check-Act (PDCA) cycle is often used as a foundational model for driving continuous improvement within CSI
#### PDCA Circle
The **PDCA Cycle**, also known as the **Deming Cycle**, is an iterative management method used for the control and continuous improvement of processes and products. It's a fundamental concept in quality management and is heavily leveraged within ITIL's Continual Service Improvement.

1. **P - Plan:**
    - **What to do:** Identify an opportunity for improvement and plan a change. This involves understanding the current situation, defining the problem or opportunity, setting goals, and developing a specific plan for how to achieve the improvement.
    - **Questions to ask:** What's the problem? What's our objective? How will we achieve it? What resources do we need? What are our success metrics?
        
2. **D - Do:**
    - **What to do:** Implement the planned change on a small scale or in a controlled environment (e.g., a pilot project). This stage involves executing the plan, collecting data, and observing the results.
    - **Key here:** Execute the plan, monitor its progress, and collect data without making further changes at this point.
        
3. **C - Check (or Study/Analyze):**
    - **What to do:** Analyze the results of the "Do" phase. Compare the outcomes against the goals set in the "Plan" phase. Identify what worked, what didn't, and why.
    - **Questions to ask:** Did the change achieve the desired results? What were the deviations? What did we learn?
        
4. **A - Act (or Adjust):**
    - **What to do:** Based on the insights from the "Check" phase, take action.
        - If the change was successful, standardize it, implement it more broadly, and integrate it into standard operating procedures.
        - If it wasn't successful, discard it or refine the plan and go through the cycle again. This stage also identifies new opportunities for further improvement, starting a new cycle.
    - **Key here:** Institutionalize successful changes or learn from failures to refine the next iteration of the cycle.

The PDCA cycle is _continual_ because once the "Act" phase is completed, the process is revisited to identify new areas for improvement, starting a new "Plan" phase. This iterative nature drives ongoing optimization and refinement.
### CRM Customer Relationship Management
Customer Relationship Management (CRM) is a broader business strategy and set of technologies focused on managing and analyzing customer interactions and data throughout the customer lifecycle. Its primary goal is to improve business relationships with customers, assist in customer retention, and drive sales growth. CRM systems typically handle sales, marketing, and customer service functions.

Within the context of ITIL, CRM itself is not one of the core ITIL practices like Incident Management or Change Management. However, ITIL practices significantly _contribute_ to and interact with aspects of customer relationship management, particularly in the realm of customer service and satisfaction.

Here's how ITIL practices relate to customer relationships:

- **Service Request Management:** This practice directly handles standard customer requests, providing a structured and efficient way to fulfill them, which positively impacts customer satisfaction.
- **Incident Management:** By quickly restoring services after disruptions, Incident Management minimizes negative customer impact and maintains trust in IT services.
- **Problem Management:** By identifying and resolving the root causes of recurring incidents, Problem Management proactively prevents future issues, leading to a more stable and reliable service experience for customers.
- **Relationship Management (in ITIL 4):** While not precisely "CRM," ITIL 4 introduces a dedicated "Relationship Management" practice. This practice focuses on establishing and nurturing links between the service provider and all its stakeholders (including customers, users, partners, and suppliers) at strategic and tactical levels. Its purpose is to ensure that services meet or exceed expectations and to foster collaboration and value co-creation. This is the closest ITIL comes to a direct "customer relationship" focus.

In summary, while CRM is a distinct business discipline, ITIL practices provide the operational framework and processes that underpin a positive customer experience, making IT an effective partner in overall customer relationship management.
## Other
#### One-way tickets
- ping-pong van de ticket vermijden
#### Warm transfer
- wanneer er een ticket wordt geescalleerd (horizontal or vertical) moet er een duidelijke uitleg en documentatie bij zijn. extra informatie meegeven.
- de klant dient maar 1 keer zijn uitleg te doen, dit om klantgericht te worden
#### Prioriteit matrix verbeteren
- sommige klanten hebben voorrang (VIP)
- urgency x impact
#### Capacity en Availability

- capacity = hoeveelheid er in totaal er is
- availability = de effectieve beschikbaarheid van die capaciteit
