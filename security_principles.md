# Principles \n## Category Security\n
###Always consider the users
#### StatementAlways consider the users\n#### RationaleThe security stance of a software system is inextricably linked to what its users do with it. It is therefore very important that all security-related mechanisms are designed in a manner that makes it easy to deploy, configure, use, and update the system securely. Remember, security is not a feature that can simply be added to a software  system, but rather a property emerging from how the system was built and is operated.

The way each user interacts with software is dictated not only by the design and implementation decisions of its creators but also by the cognitive abilities and cultural background of its users.\n#### ImplicationsFailing to address this design principle can lead to a various problems, e.g.:
<ul>
	<li>When designers don’t “remember the user” in their software design, inadvertent disclosures by the user may take  place. If it is difficult to understand the authorization model, or difficult to understand the configuration for visibility  of data, then the user’s data are likely to be unintentionally disclosed.</li>
	<li>Designers sometimes fail to account for the fact that authenticated and properly authorized users can also be attackers! This design error is a failure to distrust the user, resulting in authorized users having opportunities to misuse the system.</li>
	<li>When security is too hard to set up for a large population of the system’s users, it will never be configured, or it will not be configured properly.</li>
</ul>\n
###Asset protection and resilience
#### StatementAsset protection and resilience\n#### RationaleConsumer data, and the assets storing or processing it, should be protected against physical tampering, loss, damage or seizure.\n#### ImplicationsIf this principle is not implemented, inappropriately protected consumer data could be compromised which may result in legal and regulatory sanction, or reputational damage. \n
###Assume that external systems are insecure
#### StatementAssume that external systems are insecure\n#### RationaleThe term information domain arises from the practice of partitioning information resources according to access control, need, and levels of protection required. Organizations implement specific measures to enforce this partitioning and to provide for the deliberate flow of authorized information between information domains. The boundary of an information domain represents the security perimeter for that domain.

An external domain is one that is not under your control. In general, external systems should be considered insecure.\n#### Implications\n
###Audit information provision to consumers
#### StatementAudit information provision to consumers\n#### RationaleConsumers should be provided with the audit records they need to monitor access to their service and the data held within it. 
If this principle is not implemented, consumers will not be able to detect and respond to inappropriate or malicious use of their service or data within reasonable timescales. \n#### Implications\n
###Authenticate users and processes to ensure appropriate access control decisions both within and across domains
#### StatementAuthenticate users and processes to ensure appropriate access control decisions both within and across domains\n#### RationaleAuthentication is the process where a system establishes the validity of a transmission, message, or a means of verifying the eligibility of an individual, process, or machine to carry out a desired action, thereby ensuring that security is not compromised by an untrusted source. It is essential that adequate authentication be achieved in order to implement security policies and achieve security goals.\n#### Implications\n
###Authorize after you authenticate
#### StatementAuthorize after you authenticate. \n#### RationaleAuthorization should be conducted as an explicit check, and as necessary even after an initial authentication has been completed. Authorization depends not only on the privileges associated with an authenticated user, but also on the context of the request. The time of the request and the location of the requesting user may both need to be taken into account.\n#### ImplicationsFor particularly sensitive operations, authorization may need to invoke authentication.

Although authorization begins only after authentication has occurred, this requirement is not circular. Authentication is not binary—users may be required to present minimal (such as a password) or more substantial (e.g. biometric or token-based) evidence of their identity, and authentication in most systems is not continuous—a user may authenticate, but walk away from the device or hand it to someone else.\n
###Avoid security by obscurity
#### StatementSecurity measurements should not be open and transparent.\n#### RationaleAssume attackers will have source code (also for closed source software).
Assume attackers will have complete design and network topologies.
Open security design promote cycle of improvement faster.\n#### ImplicationsSecurity should always be tested by experts (open or not)\n
###Check the return value of all non-void functions, and check the validity of all function parameters
#### StatementCheck the return value of all non-void functions, and check the validity of all function parameters.

The return value of non-void functions must be checked by each calling function, and the validity of parameters must be checked inside each function. \n#### RationaleThis is possibly the most frequently violated principle.In the strictest interpretation, this rule means that even the return value of printf statements and file close statements must be checked.
A case can be made, though, that if the response to an error would rightfully be no different than the response to success, there is no point in checking a return value. This is often the case with calls to printf and close. In cases like these, it can be acceptable to explicitly cast the function return value to (void) -- thereby indicating that the programmer explicitly and not accidentally decides to ignore a return value. The rule is then only violated if the cast is missing.
In more dubious cases, a comment should be present to explain why a return value is irrelevant.

In most cases, though, the return value of a function should not be ignored, especially if error return values must be propagated up the function call chain. Standard libraries famously violate this rule with potentially grave consequences. See, for instance, what happens if you accidentally execute

<tt>strlen(0)</tt>

, or

<tt>strcat(s1, s2, -1)</tt>

with the standard C string library. For this reason, most coding guidelines for safety critical software also forbid the use of all ansi standard headers like string.h, stdlib.h, stdio.h etc. If the function are needed, they should be written separately, and made compliant with safety critical use.

The enforcement of this principle make sure that exceptions are always explicitly justified (and justifiable), with mechanical checkers flagging violations.  Often, it will be easier to comply with the rule than to explain why non-compliance is acceptable.\n#### ImplicationsExtra testing and programming effort:Function parameters should normal be verified for validity before being used. This rule especially applies to pointers: before dereferencing a pointer that is passed as a parameter the pointer must be checked for null.\n
###Clearly delineate the physical and logical security boundaries governed by associated security policies.
#### StatementClearly delineate the physical and logical security boundaries governed by associated security policies.\n#### RationaleInformation technology exists in physical and logical locations, and boundaries exist between these locations. An understanding of what is to be protected from external factors can help ensure adequate protective measures are applied where they will be most effective. Sometimes a boundary is defined by people, information, and information technology associated with one physical location.\n#### Implications\n
###Compartmentalise
#### StatementSub-systems will be partitioned logically and isolated using physical devices and/or security controls \n#### RationaleIn accordance with the Minimise Attack Surface and Defence in Depth principles, the Compartmentalise principle keeps a sub-system, or logically grouped set of sub-systems, relatively self-contained such that compromise of one will not imply the compromise of another. \n#### Implications\n
###Compile with all warnings enabled
#### StatementCompile with all warnings enabled, in pedantic mode, and use one or more modern static source code analyzers.

All code must be compiled, from the first day of development, with all compiler warnings enabled at the compiler's most pedantic setting. All code must compile with these setting without warnings. All code must be checked on each build with at least one, but preferably more than one, state-of-the-art static source code analyzer and should pass the analyses with zero warnings. \n#### RationaleThere are several very effective static source code analyzers on the market today, and quite a few freeware tools as well. There is no excuse for any serious software development effort not to make use of this technology. It should be considered routine practice, especially for critical software development. The rule of zero warnings applies even in cases where the compiler or the static analyzer gives an erroneous warning: if the compiler or the static analyzer gets confused, the code causing the confusion should be rewritten so that it becomes more trivially valid. Many have been caught in the assumption that a warning was likely invalid, only to realize much later that the report was in fact valid for less obvious reasons.
Static analyzers originally had a bad reputation due to the limited capabilities of early versions (e.g., the early Unix tool <tt>lint</tt>). The early tools produced mostly invalid messages, but this is not the case for the current generation of commercial tools. The best static analyzers today are fast, and they produce selective and accurate messages.\n#### ImplicationsProvide awareness trainings of developers continuously.

&nbsp;\n
###Complete mediation
#### StatementComplete mediation\n#### RationaleAccess rights are completely validated every time an access occurs. Systems should rely as little as possible on access decisions retrieved from a cache. Again, file permissions tend to reflect this model: the operating system checks the user requesting access against the file’s ACL. The technique is less evident when applied to email, which must pass through separately applied packet filters, virus filters, and spam detectors.\n#### Implications\n
###Computer Security is Constrained by Societal Factors
#### StatementComputer Security is Constrained by Societal Factors\n#### RationaleThe ability of security to support the mission of an organization may be limited by various factors, such as social issues. For example, security and workplace privacy can conflict. 
Commonly, security is implemented on an IT system by identifying users and tracking their actions. However, expectations of privacy vary and can be violated by some security measures. 
(In some cases, privacy may be mandated by law.)\n#### Implications\n
###Computer Security Requires a Comprehensive and Integrated Approach
#### StatementComputer Security Requires a Comprehensive and Integrated Approach\n#### RationaleProviding effective computer security requires a comprehensive approach that considers a variety of areas both within and outside of the computer security field. This comprehensive approach extends throughout the entire information life cycle.
To work effectively, security controls often depend upon the proper functioning of other controls. Many such interdependencies exist. If appropriately chosen, managerial, operational,and technical controls can work together synergistically.\n#### ImplicationsThe effectiveness of security controls (also) depends on such factors as system management, legal issues, quality assurance, and internal and management controls. Computer security needs to work with traditional security disciplines including physical and personnel security.\n
###Computer Security Responsibilities and Accountability Should Be Made Explicit
#### StatementComputer Security Responsibilities and Accountability Should Be Made Explicit\n#### RationaleThe responsibility and accountability3 of owners, providers, and users of IT systems and other parties4 concerned with the security of IT systems should be explicit.5 The assignment of responsibilities may be internal to an organization or may extend across organizational boundaries.\n#### ImplicationsDepending on the size of the organization, the computer security program may be large or small, even a collateral duty of another management official. However, even small organizations can prepare a document that states organization policy and makes explicit computer security responsibilities.\n
###Computer Security Should Be Cost-Effective
#### StatementComputer Security Should Be Cost-Effective\n#### RationaleThe costs and benefits of security should be carefully examined in both monetary and nonmonetary terms to ensure that the cost of controls does not exceed expected benefits. Security should be appropriate and proportionate to the value of and degree of reliance on the IT systems and to the severity, probability, and extent of potential harm. Requirements for security vary, depending upon the particular IT system.\n#### Implications\n
###Computer Security Should Be Periodically Reassessed
#### StatementComputer Security Should Be Periodically Reassessed\n#### RationaleComputers and the environments in which they operate are dynamic. System technology and users, data and information in the systems, risks associated with the system, and security requirements are ever-changing. Many types of changes affect system security: technological developments (whether adopted by the system owner or available for use by others); connection to external networks; a change in the value or use of information; or the emergence of a new threat. In addition, security is never perfect when a system is implemented.\n#### Implications\n
###Computer Security Supports the Mission of the Organization
#### StatementComputer Security Supports the Mission of the Organization\n#### RationaleThe purpose of computer security is to protect an organization's valuable resources, such as information, hardware, and software. Through the selection and application of appropriate safeguards, security helps the organization's mission by protecting its physical and financial resources, reputation, legal position, employees, and other tangible and intangible assets.\n#### Implications\n
###Data in transit protection
#### StatementData in transit protection\n#### RationaleConsumer data transiting networks should be adequately protected against tampering and eavesdropping via a combination of network protection and encryption.\n#### ImplicationsIf this principle is not implemented, then the integrity or confidentiality of the data may be compromised whilst in transit. \n
###Data Security
#### StatementData is protected from unauthorized use and disclosure. In addition to the traditional aspects of data classification, this includes, but is not limited to, protection of per-decisional, sensitive, source selection-sensitive, and proprietary information.\n#### RationaleOpen sharing of information and the release of information via relevant legislation must be balanced against the need to restrict the availability of classified, proprietary, and sensitive information.

Existing laws and regulations require the safeguarding of security and the privacy of data, while permitting free and open access.\n#### ImplicationsAggregation of data, both classified and not, will create a large target requiring review and de-classification procedures to maintain appropriate control. 

Access to information based on a need-to-know policy will force regular reviews of the body of information.

Security needs must be identified and developed at the data level, not the application level.

Data security safeguards can be put in place to restrict access to "view only", or "never see".

Sensitivity labeling of data for access to pre-decisional, decisional, classified, sensitive, or proprietary information must be determined.

Security must be designed into data elements from the beginning; it cannot be added later.

Systems, data, and technologies must be protected from unauthorized access and manipulation. Headquarters information must be safeguarded against inadvertent or unauthorized alteration, sabotage, disaster, or disclosure.\n
###Declare data objects at the smallest possible level of scope
#### StatementDeclare data objects at the smallest possible level of scope. 
\n#### RationaleBasic principle of data-hiding. Clearly if an object is not in scope, its value cannot be referenced or corrupted. Similarly, if an erroneous value of an object has to be diagnosed, the fewer the number of statements where the value could have been assigned; the easier it is to diagnose the problem. The rule discourages the re-use of variables for multiple, incompatible purposes, which can complicate fault diagnosis. \n#### ImplicationsData should always be declared at the start of the scope in which it is used: for file scope, the declarations go at the top of the source file (never in a header file); for function scope, the declaration goes at the top of the function body; for block scope, at the start of the block. This means that declarations should not be placed at random places in the code, e.g., that the point of first use.
Data objects only used in one file should be declared file <i>static</i>. \n
###Defense in depth
#### StatementDefense in depth should be a key architecture and design principle.\n#### RationaleMulti-layered security controls and practices are better than single defense layer.\n#### ImplicationsDo not trust on security measurements from preceding functions.
Prepare for the worst possible scenario.
Implement multiple defense mechanism\n
###Design and implement audit mechanisms
#### StatementDesign and implement audit mechanisms to detect unauthorized use and to support incident investigations\n#### RationaleOrganizations should monitor, record, and periodically review audit logs to identify unauthorized use and to ensure system resources are functioning properly. In some cases, organizations may be required to disclose information obtained through auditing mechanisms to appropriate third parties.
\n#### Implications\n
###Design and operate an IT system to limit damage and to be resilient in response.
#### StatementDesign and operate an IT system to limit damage and to be resilient in response.\n#### RationaleInformation systems should be resistant to attack, should limit damage, and should recover rapidly when attacks do occur. The principle suggested here recognizes the need for adequate protection technologies at all levels to ensure that any potential cyber attack will be countered effectively.\n#### Implications\n
###Design for secure updates
#### StatementDesign for secure updates\n#### RationaleIt is easier to upgrade small pieces of a system than huge blobs. Doing so ensures that the security implications of the upgrade are well understood and controlled.\n#### ImplicationsVerify the integrity and provenance of upgrade packages; make use of code signing and signed manifests to ensure that the system only consumes patches and updates of trusted origin.

&nbsp;\n
###Design for security properties changing over time
#### StatementDesign for security properties changing over
time\n#### RationaleThe migration of previous users (and/or the correct coexistence of the local and remote users) would need to happen in a way that does not compromise security.\n#### ImplicationsMake security design modular and flexible from the start.\n
###Design security to allow for regular adoption of new technology
#### StatementDesign security to allow for regular adoption of new technology, including a secure and logical technology upgrade process.\n#### RationaleAs mission and business processes and the threat environment change, security requirements and technical protection methods must be updated. IT-related risks to the mission/business vary over time and undergo periodic assessment.\n#### Implications\n
###Develop and exercise contingency or disaster recovery procedures to ensure appropriate availability
#### StatementDevelop and exercise contingency or disaster recovery procedures to ensure appropriate availability\n#### RationaleContinuity of operations plans or disaster recovery procedures address continuance of an organization’s operation in the event of a disaster or prolonged service interruption that affects the organization’s mission.\n#### Implications\n
###Do not implement unnecessary security mechanisms.
#### StatementDo not implement unnecessary security mechanisms.\n#### RationaleEvery security mechanism should support a security service or set of services, and every security service should support one or more security goals. Extra measures should not be implemented if they do not support a recognized service or security goal. Such mechanisms could add unneeded complexity to the system and are potential sources of additional vulnerabilities.\n#### ImplicationsOnly implement security measurements when needed.
\n
###Don’t trust infrastructure
#### StatementUnderlaying infrastructure cannot be assumed safe.\n#### RationaleVulnerabilities are at hardware,firmwire, virtualization, middleware and application layers. 
To minimize data leakage risks trusting security of other objects should be prevented.\n#### ImplicationsSandbox model /Jericho model needed.
Layered defense easily possible\n
###Don’t trust services
#### StatementServices from other should never (ever) be trusted.\n#### RationaleSecurity design should protect against services use of other layers or applications (also SAAS services)\n#### ImplicationsEvery input/output and given by external services must be validated.
Authentication, authorization can be needed.
Measurements to maintain availability when using services (input or output) requires strict measurements implemented.\n
###Earn or give, but never assume or trust
#### StatementEarn or give, but never assume or trust\n#### RationaleOffloading security functions from server to client exposes those functions to a much less trustworthy environment, which is one of the most common causes of security failures predicated on misplaced trust.
Designs that place authorization, access control,enforcement of security policy, or embedded sensitive data in client software thinking that it won’t be discovered, modified, or exposed by clever users or malicious attackers are inherently weak. Such designs will often lead to compromises.\n#### Implications<ul>
	<li>Make sure all data received from an untrusted client are properly validated before processing.</li>
	<li>When designing your systems, be sure to consider the context where code will be executed, where data will go, and where data entering your system comes from.</li>
</ul>\n
###Economy of mechanism
#### StatementA simple design is easier to test and validate.\n#### RationaleKeep it simple to avoid risk. More is not always better. This means more components, more processes and more security measurements involved.

&nbsp;\n#### ImplicationsAvoid complexity\n
###Ensure proper security in the shutdown or disposal of a system
#### StatementEnsure proper security in the shutdown or disposal of a system\n#### RationaleAlthough a system may be powered down, critical information still resides on the system and could be retrieved by an unauthorized user or organization. Access to critical information systems must be controlled at all times.\n#### Implications<ul>
	<li>At the end of a system’s life-cycle, system designers should develop / design procedures to dispose of an information system’s assets in a proper and secure fashion.</li>
	<li>Procedures must be implemented to ensure system hard drives, volatile memory, and other media are purged to an acceptable level and do not retain residual information.</li>
</ul>\n
###Ensure that developers are trained in how to develop secure software.
#### StatementEnsure that developers are trained in how to develop secure software.\n#### RationaleIt is unwise to assume that developers know how to develop secure software. Therefore, ensure that developers are adequately trained in the development of secure software before developing the system. This includes application of engineering disciplines to design, development, configuration control, and integration and testing.
\n#### ImplicationsTraining cost (permanent) for all staff involved in maintaining the IT assets of a company. \n
###Establish a sound security policy as the “foundation” for design.
#### StatementEstablish a sound security policy as the “foundation” for design.\n#### RationaleA security policy is an important document to develop while designing an information system. The security policy begins with the organization’s basic commitment to information security formulated as a general policy statement. The policy is then applied to all aspects of the system design or security solution. The policy identifies security goals (e.g., confidentiality, integrity, availability, accountability, and assurance) the system should support, and these goals guide the procedures, standards and controls used in the IT security architecture design. The policy also should require definition of critical assets, the perceived threat, and security-related roles and responsibilities.\n#### Implications\n
###Establish secure defaults
#### StatementEstablish secure defaults when system goes in error or exception status, or at default startup.\n#### RationaleSecure defaults lower the risk of bad configurations.\n#### ImplicationsSecurity design principles and requirements must be implemented at first release.
Installation of software without safe defaults is not possible\n
###External interface protection
#### StatementExternal interface protection\n#### RationaleAll external or less trusted interfaces of the service should be identified and have appropriate protections to defend against attacks through them. 

If this principle is not implemented, interfaces could be subverted by attackers in order to gain access to the service or data within it. \n#### Implications\n
###Fail Safe Defaults
#### StatementFail Safe Defaults\n#### RationaleA mechanism that, in the event of failure, responds in a way that will cause no harm, or at least a minimum of harm, to other devices or danger to personnel.
\n#### Implications\n
###Fail-safe defaults
#### StatementFail-safe default settings for security and access. So in case of error security should not be compromised.\n#### RationaleIn computing systems, the save default is generally “no access” so that the system must specifically grant access to resources. Most file access permissions work this way, though Windows also provides a “deny” right. Windows access control list (ACL) settings may be inherited, and the “deny” right gives the user an easy way to revoke a right granted through inheritance. However, this also illustrates why “default deny” is easier to understand and implement, since it’s harder to interpret a mixture of “permit” and “deny” rights.\n#### Implications\n
###Formulate security measures to address multiple overlapping information domains
#### StatementFormulate security measures to address multiple overlapping information domains.\n#### RationaleAn information domain is a set of active entities (person, process, or devices) and their data objects. A single information domain may be subject to multiple security policies. A single security policy may span multiple information domains. An efficient and cost effective security capability should be able to enforce multiple security policies to protect multiple information domains without the need to separate (physically or logically) the information and respective information systems processing the data.\n#### Implications\n
###Governance framework
#### StatementA Governance framework is required for service providers of Cloud hosting.
\n#### RationaleThe service provider should have a security governance framework that coordinates and directs their overall approach to the management of the service and information within it.
If this principle is not implemented, any procedural, personnel, physical and technical controls in place will not remain effective when responding to changes in the service and to threat and technology developments. \n#### Implications\n
###HTTP header
#### StatementHTTP header information is not relied on to make security decisions.\n#### RationaleHTTP headers can be manipulated very easily.\n#### Implications\n
###Identify and prevent common errors and vulnerabilities
#### StatementIdentify and prevent common errors and vulnerabilities\n#### RationaleMany errors reoccur with disturbing regularity - errors such as buffer overflows, race conditions, format string errors, failing to check input for validity, and programs being given excessive privileges. Learning from the past will improve future results.\n#### ImplicationsUse OWASP top 10 checklist
Use proven security testtools that are regular updated.
\n
###Identify potential trade-offs between reducing risk and increased costs and decrease in other aspects of operational effectiveness.
#### StatementIdentify potential trade-offs between reducing risk and increased costs and decrease in other aspects of operational effectiveness.\n#### RationaleTo meet stated security requirements, a systems designer, architect, or security practitioner will need to identify and address all competing operational needs. It may be necessary to modify or adjust (i.e., trade-off) security goals due to other operational requirements. In modifying or adjusting security goals, an acceptance of greater risk and cost may be inevitable.\n#### Implications\n
###Identity and authentication
#### StatementIdentity and authentication\n#### RationaleAccess to all service interfaces (for consumers and providers) should be constrained to authenticated and authorised individuals.

If this principle is not implemented, unauthorised changes to a consumer’s service, theft or modification of data, or denial of service may occur.\n#### Implications\n
###Implement layered security (Ensure no single point of vulnerability).
#### StatementImplement layered security (Ensure no single point of vulnerability).\n#### RationaleSecurity designs should consider a layered approach to address or protect against a specific threat or to reduce vulnerability. For example, the use of a packet-filtering router in conjunction with an application gateway and an intrusion detection system combine to increase the work-factor an attacker must expend to successfully attack the system.\n#### Implications\n
###Implement least privilege
#### StatementImplement least privilege.\n#### RationaleThe concept of limiting access, or "least privilege," is simply to provide no more authorizations than necessary to perform required functions. This is perhaps most often applied in the administration of the system. Its goal is to reduce risk by limiting the number of people with access to critical system security controls; i.e., controlling who is allowed to enable or disable system security features or change the privileges of users or programs. Best practice suggests it is better to have several administrators with limited access to security resources rather than one person with "super user" permissions.\n#### Implications\n
###Implement tailored system security measures to meet organizational security goals.
#### StatementImplement tailored system security measures to meet organizational security goals.\n#### RationaleIn general, IT security measures are tailored according to an organization’s unique needs. While numerous factors, such as the overriding mission requirements, and guidance, are to be considered, the fundamental issue is the protection of the mission or business from IT security-related, negative impacts.\n#### Implications\n
###Isolate public access systems from mission critical resources
#### StatementIsolate public access systems from mission critical resources (e.g., data, processes, etc.).\n#### RationaleWhile the trend toward shared infrastructure has considerable merit in many cases, it is not universally applicable. In cases where the sensitivity or criticality of the information is high, organizations may want to limit the number of systems on which that data is stored and isolate them, either physically or logically. Physical isolation may include ensuring that no physical connection exists between an organization’s public access information resources and an organization’s critical information. When implementing logical isolation solutions, layers of security services and mechanisms should be established between public systems and secure systems responsible for protecting mission critical resources.\n#### ImplicationsIsolation measurements must be tested regularly.
An audit report from a third party is required (in case of cloud sourcing).

\n
###Least common mechanism
#### StatementLeast common mechanism\n#### RationaleUsers should not share system mechanisms except when absolutely necessary, because shared mechanisms may provide unintended communication paths or means of interference.\n#### Implications\n
###Least privilege
#### StatementLeast privilege\n#### RationaleEvery program and user should operate while invoking as few privileges as possible. This is the rationale behind Unix “sudo” and Windows User Account Control, both of which allow a user to apply administrative rights temporarily to perform a privileged task.\n#### ImplicationsThis principle has impact on the system, software components, but also on procedures used.

&nbsp;\n
###Limit the use of pointers
#### StatementLimit the use of pointers. Use no more than N levels of dereferencing (star operators) per expression. A strict value for N=1, but in some cases using N=2 can be justified.

Pointer dereference operations may not be hidden in macro definitions or inside typedef declarations. The use of function pointers should be restricted to simple cases. \n#### RationalePointers are easily misused, even by experienced programmers. They can make it hard to follow or analyze the flow of data in a program, especially by tool-based static analyzers. Function pointers, similarly, can seriously restrict the types of checks that can be performed by static analyzers and should only be used if there is a strong justification for their use, and ideally alternate means are provided to assist tool-based checkers determine flow of control and function call hierarchies. For instance, if function pointers are used, it can become impossible for a tool to prove absence of recursion, so alternate guarantees would have to be provided to make up for this loss in analytical capabilities. \n#### ImplicationsIt should be possible for a static analyzer to determine in all cases which function is being called, if the call is made through a function pointer. It may be acceptable to allow cases where the number of possible functions that may be called is larger than one, provided it does not affect the precision of the code analysis itself. This means that it can depend on the capabilities of a specific static analyzer what liberties can be taken with the use of function pointers.
Additionally, though, it is wise to keep function pointer use to a minimum, and to restrict to simple cases, to make sure that also humans can determine accurately and with modest effort which functions may be evoked.\n
###Limit the use of the preprocessor to file inclusion and simple macros
#### StatementLimit the use of the preprocessor to file inclusion and simple macros.

The use of the preprocessor must be limited to the inclusion of header files and simple macro definitions. Token pasting, variable argument lists (ellipses), and recursive macro calls are not permitted.
All macros must expand into complete syntactic units.
The use of conditional compilation directives should be restricted to the prevention of duplicate file inclusion in header files. \n#### RationaleThe C preprocessor is a powerful obfuscation tool that can destroy code clarity and befuddle many text based checkers. The effect of constructs in unrestricted preprocessor code can be extremely hard to decipher, even with a formal language definition in hand. In a new implementation of the C preprocessor, developers often have to resort to using earlier implementations as the referee for interpreting complex defining language in the C standard. The rationale for the caution against conditional compilation is equally important. Note that with just ten conditional compilation directives, there could be up to 2^10 (i.e., 1024) possible versions of the code, each of which would have to be tested -- causing a significant increase in the required test effort.\n#### ImplicationsMacros should only appear in header files, never in the source code itself. The #undef directive should not be used. Macros should never hide declarations, and they should not hide pointer dereference operations from the code. Macros should also never be used to redefine the language.

The restriction of macro definitions to the definition of complete syntactic units means that <i>all</i> macro bodies must be enclosed in either round or curly braces.

<b>Compiler directives</b> There should not be more #ifdef directives in a code base than there are headerfiles. Each use of compilation directives (other than the duplicate file inclusion prevention use) should be flagged by a tool-based checker and justified with a comment in the code.\n
###Logging secrets
#### StatementPrivate data (for example, passwords) is not logged.\n#### RationaleProtecting secure logs is expensive.\n#### ImplicationsA clear message level must be built in to notify exactly what the cause of error is.
Reduced risk profile on system logs. 
\n
###Minimize secrets
#### StatementMinimize secrets\n#### RationaleSecrets should be few and changeable, but they should also maximize entropy, and thus increase the attacker’s work factor. The simple principle is also true by itself, since each secret increases a system’s administrative burden.\n#### Implications\n
###Minimize the system elements to be trusted.
#### StatementMinimize the system elements to be trusted.\n#### RationaleSecurity measures include people, operations, and technology. Where technology is used, hardware, firmware, and software should be designed and implemented so that a minimum number of system elements need to be trusted in order to maintain protection.\n#### Implications\n
###Open design
#### StatementOpen design\n#### RationaleBaran (1964) argued persuasively in an unclassified RAND report that secure systems, including cryptographic systems, should have unclassified designs. This reflects recommendations by Kerckhoffs (1883) as well as Shannon’s maxim: “The enemy knows the system” (Shannon, 1948). Even the NSA, which resisted open crypto designs for decades, now uses the Advanced Encryption Standard to encrypt classified information.\n#### Implications\n
###Open Design
#### StatementOpen Design\n#### RationaleThe security of physical products, machines and systems should not depend on secrecy of the design and implementation.
\n#### ImplicationsThe security design should be open for improvement for everyone interested. Consider using an OSS solution.

&nbsp;\n
###Operational security
#### StatementOperational security\n#### RationaleThe service provider should have processes and procedures in place to ensure the operational security of the service.
processes and procedures in place to ensure the operational security of the service.

If this principle is not implemented, the service can’t be operated and managed securely in order to impede, detect or prevent attacks against it.\n#### Implications\n
###Personnel security
#### StatementPersonnel security\n#### RationaleService provider staff should be subject to personnel security screening and security education for their role.

If this principle is not implemented, the likelihood of accidental or malicious compromise of consumer data by service provider personnel is increased. \n#### Implications\n
###Protect information while being processed, in transit, and in storage.
#### StatementProtect information while being processed, in transit, and in storage.\n#### RationaleThe risk of unauthorized modification or destruction of data, disclosure of information, and denial of access to data while in transit should be considered along with the risks associated with data that is in storage or being processed. Therefore, system engineers, architects, and IT specialists should implement security measures to preserve, as needed, the integrity, confidentiality, and availability of data, including application software, while the information is being processed, in transit, and in storage.\n#### Implications\n
###Provide assurance that the system is, and continues to be, resilient in the face of expected threats.
#### StatementProvide assurance that the system is, and continues to be, resilient in the face of expected threats.\n#### RationaleAssurance is the grounds for confidence that a system meets its security expectations. These expectations can typically be summarized as providing sufficient resistance to both direct penetration and attempts to circumvent security controls. Good understanding of the threat environment, evaluation of requirement sets, hardware and software engineering disciplines, and product and system evaluations are primary measures used to achieve assurance. Additionally, the documentation of the specific and evolving threats is important in making timely adjustments in applied security and strategically supporting incremental security enhancements.\n#### ImplicationsSecurity testing must be planned and performed on regular basis.\n
###Psychological acceptability
#### StatementPsychological acceptability\n#### RationaleThis principle essentially requires the policy interface to reflect the user’s mental model of protection, and notes that users won’t specify protections correctly if the specification style doesn’t make sense to them.\n#### Implications\n
###Reduce risk to an acceptable level.
#### StatementReduce risk to an acceptable level.\n#### RationaleRisk is defined as the combination of (1) the likelihood that a particular threat source will exercise (intentionally exploit or unintentionally trigger) a particular information system vulnerability and (2) the resulting adverse impact on organizational operations, organizational assets, or individuals should this occur.\n#### Implications\n
###Risk Based Approach to Security
#### StatementEnsure that risks to confidentiality, integrity, and availability of information and technology systems are treated in a consistent and effective manner.\n#### RationaleRisk is the chance of something happening that will have an impact on company objectives and risk assessment is the overall process of risk identification, analysis, evaluation, and mitigation.
<ul>
	<li>Taking a risk based approach allows for the:
better identification of threats to our projects and initiatives,</li>
	<li>more effective allocation and use of resources to manage those risks,
and</li>
	<li>improved stakeholder confidence and trust as we better manage
information and business risk.</li>
</ul>\n#### ImplicationsThe level and cost of information security controls to manage confidentiality, integrity, and availability risk must be appropriate and proportionate to the value of the information assets and the potential severity, probability, and extent of harm.

Risks must identified so we are aware of what risks can occur, what existing controls are in place, the consequence and likelihood of the risk occurring, and a determination is made about how to treat those risks.
<ul>
	<li>Options for addressing information risk should be reviewed so that informed
and documented decisions are made about the treatment of risk. Risk
treatment involves choosing one or more options, which typically include:
Accepting risk (by an appropriate team member signing off that he/she
has accepted the risk and no further action is required)</li>
	<li>Avoiding risk (by an appropriate team member deciding not to pursue a
particular initiative)</li>
	<li>Transferring risk (by an appropriate team member to an external entity
such as insurance)</li>
	<li>Mitigating risk (by an appropriate team member by applying appropriate
information security measures, e.g., access controls, network
monitoring and incident management)</li>
</ul>\n
###Secure use of the service by the consumer
#### StatementSecure use of the service by the consumer\n#### RationaleConsumers have certain responsibilities when using a cloud service in order for this use to remain secure, and for their data to be adequately protected.

If this principle is not implemented, the security of cloud services and the data held within them can be undermined by poor use of the service by consumers. \n#### Implications\n
###Security by Design
#### StatementControls for the protection of confidentiality, integrity, and availability should be designed into all aspects of solutions from initiation, not as an afterthought. Security should also be designed into the business processes within which an IT system will be used.\n#### RationaleThe implementation of protections for confidentiality, availability and integrity within information and systems at the end of a project is more expensive than including the security protections within the initial design of the project. Controls implemented at the end of a project are often less efficient and less integrated than those integrated within the core of the project.

&nbsp;\n#### Implications<ul>
	<li>Security is designed in as an integrated part of the system architecture, not added as an afterthought.</li>
	<li>Security mechanisms must span all tiers of the architecture, and must be scalable.</li>
	<li>All solutions, custom or commercial, must be tested for security.</li>
	<li>Possible areas of control which could be addressed and integrated include (but are not limited to): asset management and information classification;
physical security; segregation of duties, protections against malicious code; backup; exchange of information; logging and monitoring; user access management; technical vulnerability management; compliance with legal requirements; and, information systems audit considerations.</li>
</ul>\n
###Sensitive Data
#### StatementSecrets are not stored in code.\n#### RationaleStoring secrets involves risk at all times.\n#### ImplicationsSoftware code must be scanned on secrets (e.g. configuration details, passwords)\n
###Sensitive data must be identified
#### StatementSensitive data must be identified and it should be defined how the data is handled.
\n#### RationaleData sets do not exist only at rest, but in transit between components within a single system and between organizations. As data sets transit between systems, they may cross multiple trust boundaries. Identifying these boundaries and rectifying them with data protection policies is an essential design activity. Trust is just as tricky as data sensitivity, and the notion of trust enclaves is likely to dominate security conversations in the next decade.\n#### ImplicationsPolicy requirements and data sensitivity can change over time as the business climate evolves, as regulatory regimes change, as systems become increasingly interconnected, and as new data sources are incorporated into a system. Regularly revisiting and revising data protection policies and their design implications is essential.\n
###Separation between consumers
#### StatementSeparation between consumers\n#### RationaleSeparation should exist between different consumers of the service to prevent one malicious or compromised consumer from affecting the service or data of another.If this principle is not implemented, service providers can not prevent a consumer of the service affecting the confidentiality or integrity of another consumer’s data or service. \n#### ImplicationsSharing services between customers by Cloud Service Providers (CSP's) requires strict separation within the security model. \n
###Separation of privilege
#### StatementSeparation of privilege\n#### RationaleA protection mechanism is more flexible if it requires two separate keys to unlock it, allowing for two-person control and similar techniques to prevent unilateral action by a subverted individual. The classic examples include dual keys for safety deposit boxes and the two-person control applied to nuclear weapons and Top Secret crypto materials. Figure 3 (courtesy of the Titan Missile Museum) shows how two separate padlocks were used to secure the launch codes for a Titan nuclear missile.Separation of privilege – A protection mechanism is more flexible if it requires two separate keys to unlock it, allowing for two-person control and similar techniques to prevent unilateral action by a subverted individual. The classic examples include dual keys for safety deposit boxes and the two-person control applied to nuclear weapons and Top Secret crypto materials.\n#### Implications\n
###Session lifetime
#### StatementSession lifetime is limited. Also for cookies.\n#### RationaleSecurity
System performance
\n#### ImplicationsAll transactions must be completed within max session time.
 \n
###Strive for operational ease of use.
#### StatementStrive for operational ease of use.\n#### RationaleThe more difficult it is to maintain and operate a security control, the less effective that control is likely to be. Therefore, security controls should be designed to be consistent with the concept of operations and with ease-of-use as an important consideration.\n#### Implications\n
###Strive for simplicity
#### StatementStrive for simplicity\n#### RationaleThe more complex the mechanism, the more likely it may possess exploitable flaws. Simple mechanisms tend to have fewer exploitable flaws and require less maintenance. Further, because configuration management issues are simplified, updating or replacing a simple mechanism becomes a less intensive process.\n#### Implications\n
###Supply chain security
#### StatementSupply chain security\n#### RationaleThe service provider should ensure that its supply chain satisfactorily supports all of the security principles that the service claims to implement.

If this principle is not implemented, it is possible that supply chain compromise can undermine the security of the service and affect the implementation of other security principles.\n#### Implications\n
###Systems Owners Have Security Responsibilities Outside Their Own Organizations
#### StatementSystems Owners Have Security Responsibilities Outside Their Own Organizations\n#### RationaleIf a system has external users, its owners have a responsibility to share appropriate knowledge about the existence and general extent of security measures so that other users can be confident that the system is adequately secure. This does not imply that all systems must meet any minimum level of security, but does imply that system owners should inform their clients or users about the nature of the security.\n#### ImplicationsManagers "should act in a timely, coordinated manner to prevent and to respond to breaches of security" to help prevent damage to others.2 However, taking such action should not jeopardize the security of systems.\n
###Treat security as an integral part of the overall system design.
#### StatementTreat security as an integral part of the overall system design.\n#### RationaleSecurity must be considered in information system design. Experience has shown it to be both difficult and costly to implement security measures properly and successfully after a system has been developed, so it should be integrated fully into the system life-cycle process. This includes establishing security policies, understanding the resulting security requirements, participating in the evaluation of security products, and finally in the engineering, design, implementation, and disposal of the system.\n#### Implications\n
###Use a authentication mechanism that cannot be bypassed
#### StatementUse a authentication mechanism taht cannot be bypassed or tampered with.\n#### RationaleThe ability to bypass an authentication mechanism can result in an unauthorized entity having access to a system or service that it shouldn’t.\n#### Implications<ul>
	<li>It’s preferable to have a single method, component, or system responsible for authenticating users. Such a single mechanism can serve as a logical “choke point” that cannot be bypassed.</li>
	<li>Much as in code reuse, once a single mechanism has been determined to be correct, it makes sense to leverage it for all authentication.</li>
</ul>\n
###Use only Secure Protocols
#### StatementOnly inherently secure protocols should be used.
The protocol should not encapsulate another insecure
protocol (IPSec / VPN etc.)
The protocol should be capable of authenticating itself\n#### RationaleInsecure protocols introduce security risks than can be easily avoided.\n#### ImplicationsInsecure Protocols (http for example)
Only used where interaction with non-trusted environment
essential.
 Protocol must be validated against application\n
###Use standard solutions
#### StatementExisting security controls should be given preference over custom solutions \n#### RationaleSecure software is hard. The largest, most experienced and deep pocketed software developers in the world, both commercial and open source, are constantly patching security vulnerabilities in software that has been in the wild and hardened over many years. It is arguably implausible for developers of a particular system to invent and deliver a security solution that is as good as or better than an off-the-shelf solution. Add to that the need to fully and clearly document how the custom security solution works for maintainers of the software and new developers to comprehend, maintain and extend the solution and the cost of training up those resources. \n#### Implications\n
###Use unique identities to ensure accountability
#### StatementUse unique identities to ensure accountability\n#### RationaleAn identity may represent an actual user or a process with its own identity, e.g., a program making a remote access. Unique identities are a required element in order to be able to:
<ul>
	<li>Maintain accountability and traceability of a user or process</li>
	<li>Assign specific rights to an individual user or process</li>
	<li>Provide for non-repudiation</li>
	<li>Enforce access control decisions</li>
	<li>Establish the identity of a peer in a secure communications path</li>
	<li>Prevent unauthorized users from masquerading as an authorized user.</li>
</ul>\n#### Implications\n
###Where possible, base security on open standards for portability and interoperability.
#### StatementWhere possible, base security on open standards for portability and interoperability.\n#### RationaleFor security capabilities to be effective security program designers should make every effort to incorporate interoperability and portability into all security measures, including hardware and software, and implementation practices.\n#### Implications\n