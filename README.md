# DevOps-Monitoring-Project
This project demonstrates a full monitoring and alerting setup using Prometheus, Node Exporter, Blackbox Exporter, and Alertmanager across two virtual machines. It also includes real-time alert notifications via email.

🔧 Tools Used
Prometheus: Monitoring system to collect and store metrics.

Node Exporter: Exposes hardware and OS metrics.

Blackbox Exporter: Monitors the health of endpoints via HTTP, TCP, etc.

Alertmanager: Handles alerts sent by Prometheus and manages silencing, inhibition, and notification.

Email Notifications: Sends alert emails using SMTP.

Nginx (optional): For hosting a simple website on the second VM.

Ubuntu (or any Linux VM): For deploying all tools.

🛠️ Setup Steps
✅ 1. VM Creation
Provision 2 VMs using your cloud provider or virtualization tool (AWS, VirtualBox, etc.)

VM 1: Prometheus, Alertmanager, Blackbox Exporter

VM 2: Node Exporter, Static Website

✅ 2. Tool Installation
Install Prometheus, Node Exporter, Blackbox Exporter, and Alertmanager on the respective VMs.

Use wget or curl to download binaries, and configure services with .yml files.

✅ 3. Website & Node Exporter Setup (VM 2)
Host a sample static HTML site using Nginx or Apache.

Run Node Exporter to expose metrics on port 9100.

✅ 4. Alerting Setup
Create alert rules in Prometheus (e.g., high CPU, HTTP probe failure).

Example alert rule:

yaml
Copy
Edit
groups:
- name: Instance Down
  rules:
  - alert: InstanceDown
    expr: up == 0
    for: 1m
    labels:
      severity: critical
    annotations:
      description: "{{ $labels.instance }} is down"
✅ 5. Integration
Connect:

Prometheus to Node Exporter

Prometheus to Blackbox Exporter

Prometheus to Alertmanager

✅ 6. Configure Email Alerts
Update alertmanager.yml:

yaml
Copy
Edit
route:
  receiver: 'email-notifications'
receivers:
- name: 'email-notifications'
  email_configs:
  - to: your_email@example.com
    from: alertmanager@example.com
    smarthost: smtp.gmail.com:587
    auth_username: your_email@example.com
    auth_identity: your_email@example.com
    auth_password: your_app_password
📊 Final Outcome
Prometheus scrapes metrics from Node & Blackbox Exporters.

Alertmanager sends real-time alert notifications via email.

Monitoring dashboard confirms uptime/latency of endpoints.

Demonstrates proactive DevOps monitoring with alert-based workflows.

✅ Cleanup
Stop services or destroy VMs to free resources.

Uninstall tools or delete configs for cleanup.

