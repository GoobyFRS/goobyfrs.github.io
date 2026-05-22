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
- employee_email
- employee_phone
- employee_timezone
- employee_ingame_username
- employee_chat_userid
- employee_hire_date (year-month-day)
- employee_termination_date (Default:null)
- employment_status
- rehire_status (Default:yes)
- employee_role (Default:technician)
- compensation_type
- base_salary
- hourly_rate
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
- customer_discord_user_id
- customer_contact_email
- customer_account_created_date (year-month-day)
- customer_account_status (Default:active)
- customer_fraud_risk (Default:low)
- customer_vip_status (Default:no)
- customer_account_value
- is_content_creator (Default:no)
- vat_taxid (Default:null)
- customer_mfa_enabled
- customer_last_login
- password_last_changed
- customer_account_locked
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
- service_ip
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

```shell
cd /var/www/
git clone https://github.com/GoobyFRS/GoobyDesk.git
sudo chown caddy /var/www/GoobyDesk
sudo mkdir /var/www/GoobyDesk/my_data
cp example_dotenv .env
cp example_employee.json my_data/employee.json
cp example_tickets.json my_data/tickets.json
cp template_configuration.yml my_data/core_configuration.yml
touch /var/log/goobydesk.log
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
deactivate
```
### GUNICORN Setup

Create a systemd service for Gunicorn. By default Gunicorn will use port 8000.

```sudo touch /etc/systemd/system/goobydesk.service```

Add the following content.

```shell
[Unit]
Description=Gunicorn Instance serving GoobyDesk
After=network.target

[Service]
User=$USER
Group=www-data
WorkingDirectory=/var/www/GoobyDesk
Environment="PATH=/var/www/GoobyDesk/venv/bin"
ExecStart=/var/www/GoobyDesk/venv/bin/gunicorn -w 3 -b 127.0.0.1:8000 app:app

[Install]
WantedBy=multi-user.target
```

### Caddy Setup

Append the following to your Caddyfile.

```shell
subdomain.example.org {
        reverse_proxy 127.0.0.1:8000

        # Security headers
        header {
                # Remove server identification
                -Server

                # HSTS - Force HTTPS (Caddy handles this well at the edge)
                Strict-Transport-Security "max-age=86400; includeSubDomains; preload"

                # Prevent clickjacking
                X-Frame-Options "DENY"

                # Prevent MIME type sniffing
                X-Content-Type-Options "nosniff"

                # Enable browser XSS protection
                X-XSS-Protection "1; mode=block"

                # Control referrer information
                Referrer-Policy "strict-origin-when-cross-origin"
        }

        log {
                output file /var/log/caddy/access.log
                format json
        }
}
```

After creating the Caddyfile with logging, setup a log rotation config for the Caddy logs....

```shell
sudo nano /etc/logrotate.d/caddy
```

Append the following data to the Caddy log rotation config...

```txt
/var/log/caddy/access.log {
    size 10M
    rotate 12
    compress
    missingok
    notifempty
    copytruncate
}
```

### Troubleshooting

- ```sudo systemctl status goobydesk.service```
- ```sudo systemctl stop goobydesk.service```
- ```sudo systemctl start goobydesk.service```
- ```sudo systemctl restart goobydesk.service```
- ```tail -n 25 /var/log/goobydesk.log```
