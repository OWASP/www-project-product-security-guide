---

layout: col-sidebar
title: OWASP Product Security Guide
tags: example-tag
level: 2
type: 
pitch: The OWASP Product Security Guide project educates developers and organizations on security considerations for various products, offering a curated list of vulnerabilities and promoting awareness and solutions within the development community.

---

<img src="Asset/OWASP Product Security Guide Logo.png" width="500" height ="300">

This page is the OWASP product security guide. It has two parts:  
1. [How products are being attacked/exploited](#how-products-are-being-attacked/exploited)  
2. [How to secure products](#how-to-secure-products)
3. [Role of AI/LLM in product security](#role-of-AI/LLM-product-security)  
  
Application security focuses on code-level vulnerabilities, while product security addresses broader aspects like design flaws and supply chain risks. Rising concerns in privacy and security stem from AI/LLMs, posing threats like data breaches, biased algorithms, and manipulation of personal information. This guide serves as a document offering insights on designing, creating, testing, and procuring secure and privacy-preserving products.

See also [this useful recording](https://youtu.be/ol-z_ShulCc?si=xmPFkpjrwrxNYQSX) or [the slides](https://github.com/OWASP/www-project-ai-security-and-privacy-guide/blob/main/assets/images/20230215-Rob-AIsecurity-Appsec-ForSharing.pdf?raw=true) from [Rob van der Veer's talk](https://sched.co/1F9DT) at the OWASP Global appsec event in Dublin on February 15 2023. And check out the Appsec Podcast episode on this guide ([audio](https://www.buzzsprout.com/1730684/12313155-rob-van-der-veer-owasp-ai-security-privacy-guide),[video](https://www.youtube.com/watch?v=SLdn3AwlCAk&)), or the [September 2023 MLSecops Podcast](https://mlsecops.com/podcast/a-holistic-approach-to-understanding-the-ai-lifecycle-and-securing-ml-systems-protecting-ai-through-people-processes-technology). If you want the short story, check out [the 5 minute product security quick-talk](https://youtu.be/D6YRQYHVHao?si=Ua_TG5tqy_YiYaVG).

<p align="left"><a href="https://youtu.be/D6YRQYHVHao?si=cMom_KcEa4sIVt6k" target="_blank" rel="noopener noreferrer"><img src="Asset/talkvideo.jpeg" width="160" height="160" border="1"/> </a></p>


Please provide your input through pull requests / submitting issues (see [repo](https://owasp.org/www-project-product-security-guide/#)) or emailing the project lead, and let's make this guide better and better. Many thanks to [Scott Bauer](https://www.linkedin.com/in/scott-bauer-90a55531/overlay/about-this-profile/), lead product security at Qualcomm, for his great contributions.

# How products are being attacked/exploited  
SDLC and [supply chain vulnerabilities](https://www.fortinet.com/resources/cyberglossary/supply-chain-attacks) are exploited through various methods. In the [SDLC](https://mediasmarts.ca/digital-media-literacy/digital-issues/cyber-security/cyber-security-software-threats), attackers leverage weaknesses in development, testing, or deployment phases, injecting malicious code or compromising tools and libraries. Supply chain attacks involve infiltrating trusted vendors or third-party components to distribute malware or tamper with updates, compromising downstream systems. Techniques like code injection, dependency confusion, or hijacking exploit authentication, authorization, or distribution weaknesses, leading to breaches, data theft, or system compromise. These highlight the [critical need for robust security measures](https://jfrog.com/blog/the-importance-of-prioritizing-product-security/) across the software development and distribution lifecycle. Products confront diverse attack vectors, including malware injection, phishing, and supply chain compromises, underscoring the need for comprehensive security measures throughout their lifecycle.

#  How to secure products

## Phase 1: Requirements

During this initial stage, new feature requirements are gathered from different stakeholders. It is crucial to recognize any security considerations associated with the functional requirements being gathered for the upcoming release.

**Sample functional requirement:** user needs the ability to verify their contact information before they are able to renew their membership.

**Sample security consideration:** users should be able to see only their own contact information and no one else’s.

## Phase 2: Design

This stage converts in-scope requirements into a plan for how the actual application should appear. Functional requirements outline actions to take place, while security requirements concentrate on actions to avoid.

**Sample functional design:** page should retrieve the user’s name, email, phone, and address from CUSTOMER_INFO table in the database and display it on screen.

**Sample security concern:** we must verify that the user has a valid session token before retrieving information from the database. If absent, the user should be redirected to the login page.

## Phase 3: Development

When it's time to implement the design, ensuring code quality from a security perspective becomes the focus. Established secure coding guidelines and code reviews verify adherence to these standards, which can be manual or automated using technologies like [static application security testing (SAST)](https://en.wikipedia.org/wiki/Static_application_security_testing). Modern application developers must consider not only their own code but also rely on existing functionality, typically from free open source components, to expedite feature delivery. Over 90% of modern deployed applications utilize such components, which are assessed using [Software Composition Analysis (SCA)](https://www.g2.com/categories/software-composition-analysis) tools.

Secure coding guidelines, in this case, may include:  
- Using parameterized, read-only SQL queries to read data from the database and minimize chances that anyone can ever commandeer these queries for nefarious purposes  
- Validating user inputs before processing data contained in them  
- Sanitizing any data that’s being sent back out to the user from the database  
- Checking open source libraries for vulnerabilities before using them

## Phase 4: Verification

The Verification phase involves a testing cycle to ensure applications meet the original design and requirements. It's a place to introduce automated security testing using various technologies. The application is not deployed unless these tests pass. This phase often includes automated tools like CI/CD pipelines to control verification and release.

Verification at this phase may include:  
- Automated tests that express the critical paths of your application  
- Automated execution of application unit tests that verify the correctness of the underlying application  
- Automated deployment tools that dynamically swap in application secrets to be used in a production environment

## Phase 5: Maintenance and Evolution

The narrative continues beyond the application release. Vulnerabilities, initially overlooked, may surface long after the release. These issues may exist in the code developers crafted but are increasingly detected in the foundational open-source components comprising the application. This results in a rise in [zero-days](https://en.wikipedia.org/wiki/Zero-day_(computing))—previously unknown vulnerabilities identified in production by the application’s maintainers.

The development team must then patch these vulnerabilities, a process that might necessitate substantial rewrites of application functionality. Vulnerabilities at this stage can also originate from external penetration tests by ethical hackers or submissions through **bug bounty** programs. Addressing such production issues requires careful planning and inclusion in future releases.

## AI/LLMs in SDLC and Supply Chain Attacks: A Double-Edged Sword

**Benefits of AI/LLMs in SDLC and Supply Chain:**

- **Automated Testing:** `LLMs can analyze code for potential issues, identifying bugs and vulnerabilities faster than manual testing.`  
- **Code Generation:** `AI can automate repetitive tasks like generating boilerplate code, freeing developers for more complex work.`  
- **Threat Detection:** `AI can analyze vast amounts of data to identify suspicious activity and potential supply chain attacks.`  
- **Security Hardening:** `AI can suggest security best practices and help developers write more secure code.`

**Risks and Challenges:**

- **AI Bias:** `Biases in training data can lead to biased AI models, potentially introducing vulnerabilities or discriminatory practices.`  
- **Poisoning Attacks:** `Malicious actors can manipulate training data or models to inject harmful code or misinformation.`  
- **Black Box Problem:** `The complex nature of AI makes it difficult to understand how decisions are made, hindering root cause analysis and security audits.`  
- **Dependency Management:** `Managing dependencies on external AI models and libraries introduces additional security risks.`

**Mitigating the Risks:**

- **Data Quality:** `Invest in high-quality, unbiased training data for AI models.`  
- **Security Awareness:** `Train developers and security teams on AI security risks and best practices.`  
- **Model Testing & Auditing:** `Regularly test and audit AI models for bias, vulnerabilities, and unintended consequences.`  
- **Dependency Management:** `Implement secure practices for managing and updating external AI dependencies.`  
- **Transparency & Explainability:** `Advocate for the development of more transparent and explainable AI models.`

**Additional Resources:**

- **Retrieval vs. poison — Fighting AI supply chain attacks:** [Link](https://www.elastic.co/security-labs/elastic-users-protected-from-suddenicon-supply-chain-attack)  
- **Detecting Poisoned AI Models:** [Link](https://arxiv.org/pdf/2204.00032)  
- **Secure the AI Software Supply Chain:** [Link](https://www.linuxfoundation.org/resources/publications/open-source-software-supply-chain-security)
