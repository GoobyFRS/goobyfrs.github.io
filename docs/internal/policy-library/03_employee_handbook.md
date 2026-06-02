---
layout: minimal
title: Employee Handbook
nav_enabled: false
parent: Handbook
grand_parent: SMB Projects
nav_order: 3
---

# [MATTFAULKNER] Employee Handbook

## Welcome

Welcome to [MATTFAULKNER].

This handbook establishes the expectations, policies, and security standards that apply to all employees across [MATTFAULKNER] business units. Please read it carefully and refer to it whenever you have questions about workplace expectations or company policy.

Because employees may encounter payment card data or systems connected to payment processing, maintaining PCI-DSS compliance and strong cybersecurity practices is a **core responsibility** for all staff.

## People & Conduct

### Equal Employment Opportunity

[MATTFAULKNER] provides equal employment opportunities to all employees and applicants regardless of race, religion, color, sex, gender identity, sexual orientation, national origin, age, disability, veteran status, or any other protected status under applicable law.

Harassment, discrimination, retaliation, or hostile conduct of any kind will not be tolerated.

### Employment Classifications

Employees at [MATTFAULKNER] are classified as follows:

| Classification | Description |
|---|---|
| **Full-Time** | 40 hours/week; eligible for full benefits package |
| **Part-Time** | Regularly scheduled below 40 hours/week; benefits eligibility varies |
| **Seasonal** | Fixed-duration employment tied to a specific season or business period; limited benefits |
| **Contractor** | Independent engagement; not an employee; compensated per individual agreement |

Benefits, leave eligibility, and scheduling requirements vary by classification and are detailed in the Compensation & Benefits section. This handbook applies to all classifications unless a section explicitly states otherwise.

### Workplace Conduct

All employees are expected to:

- Behave professionally and respectfully in all interactions.
- Protect company and customer information.
- Follow all cybersecurity and PCI compliance policies.
- Use company systems responsibly and only for authorized purposes.
- Report suspicious or unsafe behavior promptly.
- Follow management instructions and guidelines.
- Maintain confidentiality of all business information.

**The following conduct is strictly prohibited:**

- Unauthorized access to systems or data.
- Sharing passwords or MFA tokens with anyone.
- Installing unauthorized software on company systems.
- Downloading illegal or malicious content.
- Harassment or threats toward any person.
- Theft or misuse of company property.
- Circumventing security controls.
- Storing PCI data outside approved systems.

Violations may result in disciplinary action up to and including termination.

### Conflicts of Interest

All employees must disclose any situation that could create a conflict of interest, including:

- Financial interest in client organizations.
- Personal relationships with clients or competitors.
- Outside employment or consulting work.
- Board positions or advisory roles involving competing interests.
- Any situation that could create the appearance of a conflict.

**Employees may not:**

- Use [MATTFAULKNER] resources or information for personal gain.
- Accept gifts valued over $100 from clients or vendors without prior disclosure.
- Perform unauthorized work for competitors.
- Share [MATTFAULKNER] confidential information with outside parties.
- Use their position to influence business decisions for personal benefit.

---

## Compensation & Benefits

### Compensation

Employees are paid on a **bi-weekly** basis. Direct deposit is available and encouraged. Pay rates are reviewed annually based on performance and company growth.

Contractors are compensated per the terms of their individual engagement agreement. Invoicing instructions and payment schedules will be established at the start of each engagement.

Overtime and work outside the agreed scope must be **pre-approved** by management.

### Benefits Eligibility

Benefits eligibility varies by employment classification:

| Benefit                  | Full-Time | Part-Time | Seasonal | Contractor |
|---|---|---|---|---|
| Health Insurance         | ✓ | Varies | — | — |
| Paid Time Off (PTO)      | ✓ | Varies | — | — |
| 401(k)                   | ✓ | Varies | — | — |
| Professional Development | ✓ | ✓      | — | — |

Health insurance is effective the first of the month following 60 days of employment for eligible employees.

### Paid Time Off (PTO)

Full-time employees accrue PTO based on length of service:

| Tenure | PTO Accrual |
|---|---|
| 0–2 years | 12 days per year |
| 3–5 years | 18 days per year |
| 6+ years | 24 days per year |

PTO requests should be submitted at least one week in advance when possible. Part-time and seasonal PTO eligibility will be defined at hire.

### Scheduling and Work Hours

Standard business hours are **Monday through Friday, 9:00 AM to 5:00 PM**. Some positions may require different schedules or on-call availability. Specific scheduling requirements will be communicated at hire or as business needs change.

### Performance Expectations

All employees are expected to:

- Maintain current knowledge of technologies and practices relevant to their role.
- Complete required training and certifications as assigned.
- Document work thoroughly in company-approved systems.
- Respond promptly and professionally to requests.
- Escalate issues and blockers proactively.

---

## Remote & Onsite Work

### Remote Work Policy

Remote work is permitted with management approval. Employees approved for remote work must:

- Maintain a dedicated, private workspace where sensitive information cannot be viewed by others.
- Ensure a reliable high-speed internet connection.
- Be available and responsive during core business hours.
- Attend virtual meetings as required.
- Use company-approved VPN and security tools at all times when accessing [MATTFAULKNER] systems.
- Lock devices when stepping away, even briefly.
- Use only approved communication platforms for business purposes.

**Remote employees may not:**

- Use public, shared, or library computers for [MATTFAULKNER] work.
- Disable endpoint protection or security software.
- Store PCI data locally unless explicitly authorized in writing.
- Share work devices with family members or anyone else.
- Access [MATTFAULKNER] systems from public Wi-Fi without VPN.

### Onsite Work Policy

Employees working onsite must:

- Wear a company-issued badge at all times in secured areas.
- Follow all visitor escort procedures.
- Secure sensitive paperwork when not in use.
- Keep workspaces clean and organized.
- Comply with all building access and physical security requirements.

Tailgating or allowing unauthorized individuals into secured areas is strictly prohibited.

### Clean Desk and Screen Policy

This policy applies to both remote and onsite employees. All employees must:

- Lock screens when stepping away from workstations, even briefly.
- Remove sensitive documents from visible areas when unattended.
- Properly shred or securely dispose of confidential printed materials.
- Secure laptops and mobile devices when not in use.

PCI-related information must never be left visible in public, shared, or unsecured environments.

---

## Information Security & PCI Compliance

> Any employee who handles payment card information, or has access to systems connected to payment processing, is subject to PCI-DSS requirements. Non-compliance may result in disciplinary action up to and including immediate termination.

### General Security Requirements

All employees must:

- Access only systems and data necessary for their specific job duties.
- Follow least-privilege access principles at all times.
- Immediately report suspected breaches, anomalies, or phishing attempts.
- Complete required security awareness training.
- Use only approved payment processing systems.
- Protect customer payment information at all times.

### PCI Data Restrictions

Employees working within the cardholder data environment may **never**:

- Write down cardholder data unless explicitly authorized and in approved systems.
- Store card numbers in spreadsheets, personal notes, or local files.
- Send PCI data over unencrypted email, chat, or messaging tools.
- Capture full card details in screenshots or screen recordings.
- Share customer payment information with any unauthorized personnel.

### Data Classification

| Classification | Examples | Handling |
|---|---|---|
| **Public** | Marketing materials, published docs | No restrictions |
| **Internal** | Procedures, org info | Internal channels only |
| **Confidential** | Client data, business strategy | Encrypted storage, need-to-know access |
| **Restricted** | PCI/cardholder data, credentials | Approved systems only; strict controls |

PCI data is always classified as **Restricted**.

Employees must store data only in approved locations, use encryption where required, and dispose of sensitive data securely. Sensitive documents must never be discarded in regular trash or recycling.

### Email and Communication Security

Employees must use [MATTFAULKNER]-approved communication tools for all business operations involving sensitive information.

Employees must not:

- Send sensitive, confidential, or PCI data through personal email accounts.
- Click suspicious links or open unexpected attachments.
- Share confidential data in public channels or group chats.

All suspected phishing attempts or suspicious messages must be reported immediately.

### Physical Security

Employees must:

- Protect all company-issued devices from loss, theft, or unauthorized access.
- Secure offices, workspaces, and any physical documents containing sensitive information.
- Never leave devices containing company information unattended in vehicles, hotels, or public places.

---

## Acceptable Use Policy

[MATTFAULKNER] systems and networks are provided for authorized business use. Limited personal use is permitted if it does not interfere with work duties, violate company policy, or introduce security risks.

**Employees may not use [MATTFAULKNER] resources to:**

- Access illegal or inappropriate content.
- Conduct unauthorized outside business activities.
- Download or distribute pirated software or media.
- Perform cryptocurrency mining.
- Introduce malware or malicious software.
- Bypass any security control.

> All activity on [MATTFAULKNER]-owned or managed systems may be monitored and logged.

### Password and MFA Requirements

| Requirement | Standard |
|---|---|
| **Minimum length** | 14 characters |
| **Recommended approach** | Strong passphrase |
| **Reuse** | Prohibited across systems |
| **Sharing** | Strictly prohibited |

Employees must enable MFA wherever available, use approved password managers when provided, and never share passwords or authentication tokens. Suspected account compromise must be reported immediately.

### Device and Endpoint Security

All [MATTFAULKNER]-issued devices must:

- Run approved, current anti-malware software.
- Maintain current operating system and application updates.
- Use full-disk encryption where supported.
- Be protected with screen locks.

Employees may not disable security software, jailbreak or root any device used for company work, or connect unauthorized USB storage to company systems.

Personally owned devices used for [MATTFAULKNER] work must meet the same security requirements as company-issued devices.

### VPN and Secure Remote Access

All remote access to [MATTFAULKNER] systems must occur through an approved secure access solution (VPN, ZTNA, or SD-WAN).

Employees must not:

- Expose internal [MATTFAULKNER] services directly to the internet.
- Use unauthorized remote desktop software to access company systems.
- Bypass network security controls under any circumstance.

All remote access sessions may be logged and monitored.

---

## Incident Reporting

All employees must **immediately** report any of the following:

- Lost or stolen devices (company-issued or personal devices used for work)
- Suspected malware infections or unusual system behavior
- Unauthorized access attempts to any system or account
- Phishing emails or social engineering attempts (whether acted on or not)
- Actual or suspected data breaches or data leaks
- Disclosure of PCI or restricted data to unauthorized parties
- Physical security incidents

> When in doubt, report it. There is no penalty for good-faith reporting. Prompt reporting minimizes risk and supports PCI-DSS compliance.

Report all incidents to [MATTFAULKNER] via:

| Contact | Use For |
|---|---|
| **[MATTFAULKNER] Primary Contact** | All incidents — first point of contact |
| **Email:** [Insert Security Contact Email] | Written incident documentation |
| **Emergency:** [Insert Emergency Contact] | Active breaches or device theft |

Do not attempt to investigate, remediate, or contain a suspected breach independently without direction from [MATTFAULKNER].

## Operations

### Attendance

Employees are expected to:

- Maintain their scheduled working hours
- Notify their supervisor promptly of any unplanned absences
- Attend required meetings and training sessions

Repeated or unaddressed attendance issues may result in disciplinary action.

### Timekeeping

Non-exempt employees must accurately record all hours worked. Falsification of time records is prohibited and grounds for immediate termination. Overtime must be approved in advance by management.

### Leave and Time Off

Eligible employees may receive the following leave types:

- Paid Time Off (PTO)
- Sick Leave
- Bereavement Leave
- Jury Duty Leave
- Military Leave

Leave eligibility varies by classification. Employees should follow [MATTFAULKNER] procedures for requesting leave and provide advance notice whenever possible.

## Disciplinary Action & Separation

### Disciplinary Action

Policy violations may result in the following, depending on severity:

| Step | Action |
|---|---|
| 1 | Verbal warning |
| 2 | Written warning with documented corrective expectations |
| 3 | Suspension or revocation of system access pending review |
| 4 | Termination |

Severe violations — including security breaches, PCI non-compliance, data theft, harassment, or falsification of records — may result in **immediate termination** without prior warning steps.

### Separation of Employment

Upon separation from [MATTFAULKNER], employees must:

- Return all company-issued equipment, devices, and physical materials
- Surrender all credentials, access badges, tokens, and keys
- Cease accessing [MATTFAULKNER] systems, data, and communications immediately
- Delete or return any [MATTFAULKNER] confidential data stored on personal devices

[MATTFAULKNER] reserves the right to revoke system access at any time without prior notice. Confidentiality obligations survive the end of employment.

---

## Employee Acknowledgment

By signing below, I acknowledge that I have received, read, and understood the [MATTFAULKNER] Employee Handbook.

> I understand that compliance with all policies in this handbook — including information security, PCI-DSS requirements, acceptable use, and conduct standards — is a **condition of my employment or engagement**. I understand this handbook is not a contract of employment and may be updated at any time with reasonable notice.

*Return a signed copy to [MATTFAULKNER] prior to your first day.*
