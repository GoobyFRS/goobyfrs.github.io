---
layout: default
title: GR_Core
nav_enabled: true
parent: Open Source Projects
nav_order: 4
---
# GR_Core

GoobyDesk Extended! Fully Featured ITSM Platform for Small Businesses

**Basic ITSM Ticket management (ITSM)**

- uuid
- NAME/USERNAME
- ticket_type
- ticket_subject
- ticket_body

**Employee & Access Management (HR)**

- uuid
- employee_id (EM<count>)
- employee_first_name
- employee_last_name
- employee_preferred_name
- employee_age
- employee_dob (year-month-day)
- employee_state
- employee_ingame_username
- employee_chat_userid
- employee_hire_date (year-month-day)
- employee_termination_date (Default:null)
- rehire_status (Default:yes)
- employee_role (Default:technician)
- employee_compensation (Default:null)
- salary_exempt (Default:no)
- is_bonus_eligible (Default:no)
- bonus_rate (Default:0)
- assigned_business_unit (Default:support)
- access_role (Default:technician)
- total_pto_available (Default:0)
- reports_to (Default:null)

**Customer Tracker (CRM)**

```/crm/dashboard/``` - 

- uuid
- customer_id (CID<count>)
- customer_first_name
- customer_last_name
- customer_prefered_name
- customer_ingame_username
- customer_voicechat_username
- customer_contact_email
- customer_account_created_date (year-month-day)
- customer_account_status (Default:active)
- customer_fraud_risk (Default:low)
- customer_vip_status (Default:no)
- customer_account_value
- customer_helpdesk_tickets
- is_content_creator (Default:no)
- vat_taxid (Default:null)

**Service Database**

- uuid
- service_id
- service_sku
- service_name
- service_status
- service_subdomain
- service_created_timestamp
- service_terminated_timestamp
- service_updated_timestamp
- service_provision_source
- service_rcon_port
- service_rcon_pwd

## Code Standards

### Development Setup

### Production Setup

Process not yet determined.
