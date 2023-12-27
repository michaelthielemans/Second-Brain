#windows 
# Security Team colors

## Red Team = Attackers

- Penetration testing  
  Tries to probe and infiltrate a secured system.
- Social engineering
- Phishing

## Blue Team = Defensive
- Carrying out DNS assessments to ensure that there are no phishing activities in the network or any general issue with DNS transactions.
- Conducting a footprint analysis to ensure that there are no unidentified signatures in the network that may signal a breach.
- Managing firewall access controls and end-point security software on devices such as workstations.

## Purple team = Team with Red and Blue members
Consists of more of a dynamic party between red and blue teams
It’s usually not a fixed team but often consists of people from both teams meeting up. Its purpose is to maximize the results of Red Team engagements and improve Blue Team capability.

## Yellow Team = Developers

These are the teams that build and design software, systems, and integrations. Application developers, software engineers and architects fall into this category.

Their focus is usually on requirements, functionality, user experience and back-end performance. If we want to have applications, automations and processes designed and implemented securely, Red Team and Blue Team need to work with the Builders.
## Orange Team
 
>The purpose of the Orange dynamic party is to inspire Yellow Team to be more security conscious, increasing their security awareness by providing education to benefit software code and design implementation. There should be structured and ongoing engagements between Red and Yellow Team for the benefit of Yellow.
>Since Orange’s goal is to make developers think more like attackers, it will most likely start with certain Red Team members being available to Yellow Team. Working with developers to understand how attackers work will be the first step. A developer will then, in their brain, begin to internalise how to make their apps resistant to these types of attacks. Bringing in a Red or Orange Team member at the beginning of a software sprint allows for additional “Hacker Stories” and “Mis-use cases” to be developed alongside the team’s usual “User Stories” and “Use cases” that Yellow Team would typically rely upon to make features. This gives Yellow Team immediate feedback on areas they need to secure before they write a single line of code.

### Orange Sec. Awareness: OWASP Top 10 AppSec Risks

• The Open Web Application Security Project (OWASP) is a non- profit foundation dedicated to improving the security of software.

• OWASP Top 10 is an online document on OWASP’s website that provides ranking of the top 10 most critical web application security risks based on:

• the frequency of discovered security defects • the severity of the vulnerabilities  
• the magnitude of their potential impacts

• This is an Awareness document, which the naming reflects: A01, A02, A03, ... , A10


## Orange Sec. Awareness: OWASP Top 10 AppSec Risks

* The Open Web Application Security Project (OWASP) is a non- profit foundation dedicated to improving the security of software.
* OWASP Top 10 is an online document on OWASP’s website that provides ranking of the top 10 most critical web application security risks based on:
* The frequency of discovered security defects • the severity of the vulnerabilities  
* he magnitude of their potential impacts
* This is an Awareness document, which the naming reflects: A01, A02, A03, ... , A10


### 1. Broken Access Control

>Access control enforces policy such that users cannot act outside of their intended permissions. Failures typically lead to unauthorized information disclosure, modification, or destruction of all data or performing a business function outside the user's limits.

1. Broken  Access control
	* Make sure that access to content that should not be available is blocked even if the content is not easily to find.
2. Directory Traversal -> ../../../passwords
	* If a webserver shows you a filename or a path to a file in the address field, you can kind of line browse through the structure with 
3. Cross-site request forgery
	* Making use of the http get and post procedures. passing data from within the url.
	* The hacker creates (forges) a link, the links contains a url with the malicious payload (http://site.com/post?message=malicious+content).
	* When a victim clicks the link, the content is send to the server with the victims credentials.
### 2. Cryptographic Failures

>Many web applications and APIs do not properly protect sensitive data with strong encryption. Attackers may steal or modify such weakly protected data to conduct credit card fraud, identity theft, or other crimes. Sensitive data must be encryption at rest and in transit, using a modern (and correctly configured) encryption algorithm.

### 3. Injection

>Injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when untrusted data is sent to an interpreter as part of a command or query. The attacker’s hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.

1. Sql injections
	Passing special characters to the application so that this would alter the way the sql query is interpreted. for example ''or 1=1--'
2. Command line injections
	* Some webservers make use of OS functions or programs to process a request.
	* the name of the command is used in the http header, then a hacker can build his own http post header and can manipulate the outcome.
	* example dns lookup

### 4. Insecure Design

>Pre-coding activities are critical for the design of secure software. The design phase of you development lifecycle should gather security requirements and model threats, and development time should be budgeted to allow for these requirements to be met. As software changes, your team should test assumptions and conditions for expected and failure flows, ensuring they are still accurate and desirable. Failure to do so will let slip critical information to attackers, and fail to anticipate novel attack vectors.

1. Insecure design
2. Information leakage
	1. Gathering information about
		1. what server you are running
		2. which version of application
		3. How the http response headers look like
		4. urls that are showing webserver languages, like ending a url with .php , .asp
		5. cookies with visible session id's
		6.  Error pages that will show to much information
		7. make sure you sanitise the responses to the client side application, for example: do not pass the database record id's
		8. client side javascript with common libraries may contain vulnerabilities. If the attacker can find out which type and version you are running he can look for some know security flaws.
		9. If you allow users to be able to upload files, make sure to scrub the metadata of these files. ( locations, personal information,....)
		10. All the data send to client-side will be visible, masking data with client-applications is not enough.
	2. File upload vulnerabilities
		1. make sure to rename of change the extensions that are uploaded by clients. If the client is able to upload .php files, it is possible he can execute the script.

### 5. Security Misconfiguration

>Your software is only as secure as you configure it to be. Using ad hoc configuration standards can lead to default accounts being left in place, open cloud storage, misconfigured HTTP headers, and verbose error messages containing sensitive information. Not only must all operating systems, frameworks, libraries, and applications be securely configured, but they must be patched/upgraded in a timely fashion.

1. LAX security settings
	1. weak passwords, default passwords that are not changed
	2. faulty webserver filesystem directory permissions
### 6. Vulnerable and Outdated Components

>Components, such as libraries, frameworks, and other software modules, run with the same privileges as the application. If a vulnerable component is exploited, such an attack can facilitate serious data loss or server takeover. Applications and APIs using components with known vulnerabilities may undermine application defenses and enable various attacks and impacts.

### 7. Identification and Authentication Failures

>Application functions related to authentication and session management are often implemented incorrectly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users’ identities temporarily or permanently.

1. password management
	1. password complexity
	2. password reset procedure
	3. password storage, hashing and salting passwords
2. privilege escalation
3. 

### 8. Software and Data Integrity Failures

>Software and data integrity failures relate to code and infrastructure that does not protect against integrity violations. An example of this is where an application relies upon plugins, libraries, or modules from untrusted sources, repositories, and content delivery networks (CDNs). An insecure deployment pipeline can introduce the potential for unauthorized access, malicious code, or system compromise. Lastly, many applications now include auto-update functionality, where updates are downloaded without sufficient integrity verification and applied to the previously trusted application. Attackers could potentially upload their own updates to be distributed and run on all installations

### 9. Security Logging and Monitoring Failures

>Insufficient logging and monitoring, coupled with missing or ineffective integration with incident response, allows attackers to further attack systems, maintain persistence, pivot to more systems, and tamper, extract, or destroy data. Most breach studies show time to detect a breach is over 200 days, typically detected by external parties rather than internal processes or monitoring.

1. Logging and monitoring
	1. Log everything, log what happens with files on disk.
	2. record important events that happen
	3. ship log-files to a central log server

### 10. Server-Side Request Forgery

>Server-Side Request Forgery (SSRF) flaws occur whenever a web application fetches a remote resource without validating the user-supplied URL. It allows an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall, VPN, or another type of network access control list (ACL).



## Green Team

>Blue Team are not always aware of all the frameworks, libraries, third-party systems, network calls and functionality added by Yellow Team.
>Yellow Team may sometimes be barely aware of some of the dependencies behind their own code.
>In the event of an incident, Blue Team may not have the data needed to investigate or defend breached systems and no one wants to test or touch the production environment for fear of it breaking.
>Green Team is another dynamic party that consists of ongoing structured interactions between the Blue Team and members of the software team, the Yellow Team. The ultimate goal is to improve code-based and design-based defense capability for detection, incident response and data forensics.
>With Yellow Team working with Blue Team, catching an event before it becomes an incident, before it becomes a breach, is essential to the defense of any organization. In other words, pre-empting incidents.

## Green Sec. Pre-empting: OWASP Pro-Active Controls

• OWASP Top 10 Proactive Controls for Software Developers focusses more on defensive techniques and controls, as opposed to risks:

https://owasp.org/www-project-proactive-controls/

• This is a document with Controls, which the naming reflects: C01, C02, C03, ... , C10

“the most important control and control categories thateveryarchitectand developer should absolutely, 100% include in every project.”

### C1: Define Security Requirements
- What are the security requirements of our application and how do we get to them? For 
- Should the application apply to level1, level2, level3 security requirements.
	- for example a application for a bank has higher requirements that an application for a sportsclub.
- example:
    OWASP Application Security Verification Standard
- This is a “standard” = Extensive, elaborate document of
    requirements
- Standard = you can comply to level1, or level2, or level3
    
- Result:  
    • Secure Coding Guidelines for your team • Secure Test-Driven Development
    
    • Requirements can be tested via Automatic Security Tests, you can do more focused Penetration Testing, you can start a Bug Bounty program, ...

### C2: Leverage Security Frameworks and Libraries
- You have to implement a lot of security controls! Stand on the shoulders of Giants in the Dev-world!
- Use native secure features, before 3rd party libraries (Spring Security, ...)
- Or... use Open Source security libraries and frameworks that are well vetted
- Don’t forget to update!
== Use security frameworks in you dev pipeline ==

### C3: Secure Database Access

• Remember our example? SQL Injection?
A whole control dedicated to DB access  
• Looking at the practical sense... use Cheat Sheets
• Database Security Cheat Sheet  
• Query Parameterization Cheat Sheet

### C4: Encode and Escape Data & C5: Validate All Inputs

• Number one attack vector of XSS  
(see Cheat Sheets for Injection Problems)

• Use HTML Sanitizers & DOM Purify tools  
• Really hard to do. HTML is very tricky... (.innerHTML function)  
• Most Frameworks do auto-escaping  
• Use validation options of your framework, but be aware of flaws

• SAST and DAST security tools are very good at XSS discovery

### Dynamic & Static Application Security Testing

### C8: Protect Data Everywhere

• Data in Transit: Remember HTTPS?
• Data at Rest (in storage):
• Use standard well vetted crypto libraries (Lipsodium, Tink)
• Use a form of secrets management to protect application secrets and keys (vaultproject.io)
• Personal Hardware Security Module

### C9: Implement Security Logging and Monitoring