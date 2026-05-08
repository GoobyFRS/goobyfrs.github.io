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
- ticket_number
- ticket_status (Default:new)
- requestor_name
- requestor_username
- ticket_type
- ticket_subject
- ticket_body
- ticket_impact (Default:low)
- ticket_urgency (Default:low)
- escalation_level (Default:0)
- assigned_queue (Default:support)
- assigned_technician (Default:none)
- ticket_worknotes
- ticket_created_timestamp (year-month-day-24:00)
- ticket_escalation_timestamp (year-month-day-24:00)
- ticket_closed_timestamp (year-month-day-24:00)
- ticket_acknowledged_timestamp
- requestor_vip_status (Default:false)
- ticket_overdue (Default:false)

**Employee & Access Management (HR)**

- uuid
- employee_id (EM<count>)
- employee_first_name
- employee_last_name
- employee_preferred_name
- employee_dob (year-month-day)
- employee_state
- employee_ingame_username
- employee_chat_userid
- employee_hire_date (year-month-day)
- employee_termination_date (Default:null)
- employment_status
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
- mfa_enabled
- last_login
- password_last_changed
- account_locked (Default: true)
- failed_login_attempts
- has_freshrss_access
- has_jellyfin_access
- has_nextcloud_access
- has_tailnet_access
- has_gitea_access
- has_discord_access
- has_slack_access

**Customer Tracker (CRM)**

```/crm/dashboard/``` - Table displaying CID, Full Name, 

- uuid
- customer_id (CID<count>)
- customer_first_name
- customer_last_name
- customer_preferred_name
- customer_ingame_username
- customer_voicechat_username
- customer_contact_email
- customer_account_created_date (year-month-day)
- customer_account_status (Default:active)
- customer_fraud_risk (Default:low)
- customer_vip_status (Default:no)
- customer_account_value
- is_content_creator (Default:no)
- vat_taxid (Default:null)
- mfa_enabled
- last_login
- password_last_changed
- account_locked
- customer_last_login
- customer_last_order_date
- customer_last_payment_date
- customer_total_lifetime_value
- customer_status_reason
- preferred_contact_method
- marketing_opt_in
- maintenance_notifications_enabled
- has_freshrss_access
- has_jellyfin_access
- has_nextcloud_access

**Service Database**

- uuid
- service_id
- service_sku
- service_type
- service_name
- service_status
- provisioning_status
- service_subdomain
- service_created_timestamp
- service_terminated_timestamp
- service_updated_timestamp
- service_provision_source
- customer_uuid
- customer_id
- service_rcon_port
- service_rcon_pwd
- node_id
- cluster_id
- region
- allocated_ram_mb
- allocated_disk_gb
- allocated_cpu_cores
- allocated_ports
- minecraft_version
- server_type
- modpack_name
- player_limit

## Code Standards

### Development Setup

### Production Setup

Process not yet determined.
