# Designing-a-Multi-Platform-SIEM-SOC-Architecture-for-Healthcare-Data-Protection
Designing a Cloud Security SIEM SOC platform architecture for Healthcare Data protection Using Microsoft Cloud Defender, Sentinel and Splunk
Focus: Azure Cloud Security • Healthcare Data Protection • SIEM • SOC • Network Security • SQL Security Auditing • Threat Detection • Microsoft Defender for Cloud • Microsoft Sentinel • Splunk Enterprise.

# Project Overview

This capstone project designs and implements a cloud-based Security Operations Center (SOC) architecture in Microsoft Azure for protecting sensitive healthcare and patient information.

The environment combines Microsoft Defender for Cloud, Microsoft Sentinel, Azure Monitor/Log Analytics, Azure Firewall, Network Security Groups (NSGs), Azure SQL Database, Entra ID, and Splunk Enterprise to create a multi-layer security monitoring and detection architecture.

The project focuses on detecting and investigating:

Unauthorized access to healthcare databases
Failed authentication attempts
Privilege and permission violations
Suspicious SQL activity
Potential SQL injection patterns
Patient Personally Identifiable Information (PII) access
Database modification and deletion
Network traffic and blocked connections
Suspicious activity involving TCP port 1433
Security events across Azure infrastructure
Potential patient-data exfiltration scenarios
Security telemetry requiring centralized SIEM analysis
The architecture is designed around Defense in Depth, Zero Trust principles, the CIA Triad, centralized logging, security monitoring, and incident detection

# Architecture Overview

High-Level Architecture

<img width="804" height="842" alt="image" src="https://github.com/user-attachments/assets/92bceb31-c64a-4855-b259-ae1195bb1a0b" />



# Integration with Azure Zero Trust Security Ecosystem 


<img width="948" height="528" alt="image" src="https://github.com/user-attachments/assets/9e9920d4-5702-4880-a6c5-aa97f43fa247" />

<img width="1302" height="724" alt="image" src="https://github.com/user-attachments/assets/213e7129-8a15-4eaa-a060-7925d2885541" />

# Final Dashboard for SOC Analytics

<img width="1731" height="967" alt="image" src="https://github.com/user-attachments/assets/464372b0-2b90-4999-be06-e648649ccac2" />


# Architecture Data Flow



                         ┌─────────────────────────┐
                         │       Security SOC       │
                         │                         │
                         │  Microsoft Sentinel     │
                         │  Splunk Enterprise      │
                         │  Security Dashboards    │
                         └────────────┬────────────┘
                                      │
                              Centralized Logs
                                      │
              ┌───────────────────────┼───────────────────────┐
              │                       │                       │
              ▼                       ▼                       ▼
      ┌───────────────┐      ┌────────────────┐      ┌─────────────────┐
      │ Defender for  │      │ Azure Monitor  │      │ Microsoft       │
      │ Cloud         │      │ / Log Analytics│      │ Entra ID        │
      └───────┬───────┘      └───────┬────────┘      └─────────────────┘
              │                       │
              └───────────────┬───────┘
                              │
                       Security Telemetry
                              │
                    ┌─────────▼─────────┐
                    │   Azure Network   │
                    │                   │
                    │ Azure Firewall    │
                    │ NSGs              │
                    │ VNet / Subnets    │
                    └─────────┬─────────┘
                              │
                  ┌───────────┴───────────┐
                  │                       │
                  ▼                       ▼
        ┌──────────────────┐    ┌──────────────────┐
        │ Azure SQL        │    │ Splunk Enterprise │
        │ Database         │    │ Azure VM         │
        │                  │    │                  │
        │ Patient Data     │    │ SIEM / Analytics │
        │ SQL Audit Logs   │    │ Dashboards       │
        └──────────────────┘    └──────────────────┘

# Security data Workflow

Azure Resources
      │
      ├── Azure SQL Audit Logs
      ├── Azure Firewall Logs
      ├── NSG / Network Logs
      ├── Entra ID Logs
      ├── Defender Alerts
      └── Azure Diagnostic Logs
              │
              ▼
      Log Analytics Workspace
              │
              ├───────────────► Microsoft Sentinel
              │                       │
              │                       ├── Analytics Rules
              │                       ├── Incidents
              │                       ├── Workbooks
              │                       └── Investigations
              │
              └───────────────► Splunk Enterprise
                                      │
                                      ├── Indexes
                                      ├── Searches
                                      ├── Dashboards
                                      └── Security Alerts


# Azure service Used for implementation


 | Azure Service | Key Feature | Security Purpose |
| --- | --- | --- |
| **Azure SQL Database** | Managed relational database | Hosts healthcare/patient data |
| **Azure Virtual Machine** | Compute infrastructure | Hosts Splunk Enterprise |
| **Azure Virtual Network (VNet)** | Network isolation | Segments cloud infrastructure |
| **Network Security Groups (NSG)** | Stateful traffic filtering | Controls inbound/outbound network traffic |
| **Azure Firewall** | Managed network security | Network filtering, monitoring and threat protection |
| **Microsoft Defender for Cloud** | CSPM/CWPP capabilities | Cloud security posture and workload protection |
| **Microsoft Sentinel** | Cloud-native SIEM/SOAR | Centralized security analytics and incident detection |
| **Log Analytics Workspace** | Centralized telemetry repository | Stores and queries Azure logs |
| **Azure Monitor** | Monitoring and diagnostics | Infrastructure and application observability |
| **Azure Diagnostic Settings** | Resource log collection | Sends Azure resource logs to Log Analytics |
| **Microsoft Entra ID** | Identity and access management | Authentication and authorization |
| **Data Collection Rules (DCR)** | Configurable telemetry collection | Controls collection and routing of monitoring data |
| **Azure SQL Auditing** | Database activity auditing | Records SQL security and data-access events |
| **Azure SQL Diagnostic Logs** | SQL telemetry | Provides database security and operational visibility |

 ### External / Third-Party Security Platform

 | Platform | Role |
| --- | --- |
| **Splunk Enterprise** | Independent SIEM platform for log ingestion, correlation, investigation and visualization |

# 1. Project Purpose : 

Problem Statement
Healthcare organizations operate highly sensitive information systems containing patient identities, medical information, insurance information, and other regulated data.

Modern healthcare environments face several cybersecurity challenges.

Advanced Cyber Threats
Attackers increasingly use sophisticated techniques including:

Credential compromise
Privilege escalation
SQL injection
API exploitation
Data exfiltration
Lateral movement
Identity-based attacks
AI-assisted attacks
Prompt injection against AI-enabled healthcare applications
Increasing Vulnerabilities in AI-Based Healthcare Systems
The integration of Agentic AI and AI-powered healthcare applications introduces additional attack surfaces.

Potential risks include:

Prompt injection
Unauthorized AI-agent access to patient information
Abuse of healthcare APIs
Excessive AI-agent privileges
Sensitive-data leakage
Manipulation of AI workflows
Unauthorized access to EHR/EMR systems
Expanded Attack Surface and Limited Visibility
Modern healthcare infrastructure can span

Users
   ↓
Applications
   ↓
APIs
   ↓
AI Agents
   ↓
Cloud Infrastructure
   ↓
Databases
   ↓
External Services

This creates a requirement for centralized security visibility across identity, network, application, database, and cloud infrastructure.

Regulatory and Compliance Requirements
Healthcare organizations must protect sensitive information and demonstrate appropriate security controls.

This project therefore emphasizes:

Confidentiality
Integrity
Availability
Identity and access management
Auditability
Security monitoring
Incident detection
Centralized logging
Security investigation


# 2. Project Objectives

This project objectives are:

Design and implement a Cloud SOC architecture in Azure
Protect sensitive healthcare and patient data
Implement layered network and database security
Centralize security telemetry using Microsoft Sentinel and Splunk
Deploy Microsoft Defender for Cloud for cloud security posture and threat detection
Monitor Azure SQL Database security events
Detect suspicious access to patient information
Monitor network traffic and security events
Investigate database access and modification activity
Develop KQL-based security detections
Demonstrate SIEM dashboards and security investigations
Establish a foundation for Zero Trust and AAA security controls

# 3. Healthcare Database Design
A dedicated Azure SQL Database was created:
SQL Server:
healthcare-data-server

Database:
HealthCare-DataBase

Patient Data Schema
The demonstration database contains a Patients table representing healthcare information.


Column	Description
PatientID	Unique patient identifier
FirstName	Patient first name
LastName	Patient last name
DOB	Date of birth
Gender	Patient gender
SSN	Social Security Number / sensitive identifier
InsuranceNumber	Insurance identifier
Email	Patient email
Phone	Patient telephone
Address	Street address
City	Patient city
Province	Patient province/state
PostalCode	Postal/ZIP code
EmergencyContact	Emergency contact
EmergencyPhone	Emergency contact phone
CreatedAt	Record creation timestamp

# Implementation Phase 

# Step 1 — Create the Azure SQL Database
The healthcare database infrastructure was provisioned in Azure.
Azure
 └── Resource Group
      └── SQL Server
           └── HealthCare-DataBase
                └── Patients

Security controls included:

SQL authentication / Entra-based identity considerations
Network access controls
SQL auditing
Diagnostic logging
Database monitoring


<img width="1296" height="513" alt="image" src="https://github.com/user-attachments/assets/d3a664c6-d144-4100-b993-2a0d9a89c8a8" />




# Step 2 — Configure the Healthcare Database Schema
The Patients table was created to simulate a healthcare data repository containing sensitive information.

The dataset was intentionally structured to support security monitoring scenarios involving:

Patient lookup
Patient creation
Patient modification
Patient deletion
Unauthorized access
PII access
Suspicious SQL statements

# Step 3 Deploy Splunk Enterprise
A dedicated Azure Virtual Machine was created for the Splunk deployment.
Azure VM
│
└── Splunk Enterprise
      │
      ├── Indexes
      ├── Searches
      ├── Alerts
      └── Security Dashboards
      
Splunk was configured as an additional SIEM platform to provide an independent security analytics layer.


Splunk Indexes:
patient_pii
patient_access
network_security
azure_sql
azure_audit
azure-sql-db-logs
patient_sql_audit
security_alerts
telemetry

Splunk Index Configuration

The following indexes were created to separate security telemetry by use case.

azure-SQL-db-logs
security_alerts
network_security
patient_access
patient_pii

# Step 4 🛡️ Microsoft Defender for Cloud
Microsoft Defender for Cloud was deployed to provide cloud security posture and workload protection capabilities.

The implementation focused on:

Security recommendations
Secure configuration
Security posture visibility
Vulnerability assessment
Threat detection
Security alerts
Cloud workload monitoring
The Defender telemetry contributes to the overall SOC monitoring architecture.

# Step 5  Azure SQL Auditing
Azure SQL auditing was configured to monitor database activity.

The audit data provides visibility into:

Authentication failures
SQL statements
Database operations
User accounts
Client IP addresses
Application names
Host information
Success/failure status
Affected rows
Security-relevant SQL operations

# Step 6:  Log Analytics Workspace
A centralized Log Analytics Workspace was created to collect Azure security and operational telemetry.

Telemetry sources:

Azure SQL
   │
   ├── SQLSecurityAuditEvents
   ├── Errors
   └── DatabaseWaitStatistics
         │
         ▼
Log Analytics Workspace
         │
         ├── Microsoft Sentinel
         └── Splunk


# Step 7: Verify Azure Log Collection
Azure diagnostic logging was validated by generating and querying activity within the healthcare database.

The validation process included:

Generate database activity
Verify diagnostic settings
Confirm logs arrive in Log Analytics
Query AzureDiagnostics
Validate timestamps
Validate database name
Validate SQL statement
Validate user identity
Validate source IP
Forward relevant telemetry to SIEM platforms

 # Step 8 : Configure Microsoft Entra ID for Splunk
Microsoft Entra ID was incorporated into the architecture to provide identity-centric security monitoring.

The integration supports monitoring of:

Identity
   │
   ├── Authentication
   ├── Authorization
   ├── Account activity
   └── Suspicious access
            │
            ▼
      Security Analytics

This contributes to the AAA security model:

Authentication
Authorization
Accounting

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::



---


 # 8\. Deploy Splunk Enterprise

 A dedicated Azure Virtual Machine was created for the Splunk deployment.

```
Azure VM
│
└── Splunk Enterprise
      │
      ├── Indexes
      ├── Searches
      ├── Alerts
      └── Security Dashboards
```

 Splunk was configured as an additional SIEM platform to provide an independent security analytics layer.


<img width="1296" height="521" alt="image" src="https://github.com/user-attachments/assets/3968be64-39d2-4165-af83-9d4894601729" />



<img width="1296" height="559" alt="image" src="https://github.com/user-attachments/assets/0a1469a5-69a3-48e1-a174-3c6c690c3d5f" />

 ### Example Splunk indexes

```
patient_pii
patient_access
network_security
azure_sql
azure_audit
azure-sql-db-logs
patient_sql_audit
security_alerts
telemetry
```

Install Splunk in Azure VM 

<img width="1296" height="523" alt="image" src="https://github.com/user-attachments/assets/391284c7-cf70-4547-a33c-b3b3efd6fbcf" />


---

 # 9\. Splunk Index Configuration

 The following indexes were created to separate security telemetry by use case.

```
azure-SQL-db-logs
security_alerts
network_security
patient_access
patient_pii
```

 Example Splunk configuration:

```
[azure-SQL-db-logs]
homePath   = $SPLUNK_DB/azure-SQL-db-logs/db
coldPath   = $SPLUNK_DB/azure-SQL-db-logs/colddb
thawedPath = $SPLUNK_DB/azure-SQL-db-logs/thaweddb
datatype   = event
maxTotalDataSizeMB = 512000
enableDataIntegrityControl = 1

[security_alerts]
homePath   = $SPLUNK_DB/security_alerts/db
coldPath   = $SPLUNK_DB/security_alerts/colddb
thawedPath = $SPLUNK_DB/security_alerts/thaweddb
datatype   = event
maxTotalDataSizeMB = 512000
enableDataIntegrityControl = 1
```

---

 # 10\. Deployed Microsoft Defender for Cloud

 Microsoft Defender for Cloud was deployed to provide cloud security posture and workload protection capabilities.

 The implementation focused on:

 - Security recommendations
- Secure configuration
- Security posture visibility
- Vulnerability assessment
- Threat detection
- Security alerts
- Cloud workload monitoring

 The Defender telemetry contributes to the overall SOC monitoring architecture.


<img width="1120" height="897" alt="image" src="https://github.com/user-attachments/assets/9a5ce605-3611-415a-ad87-2a0892a44ee7" />

---

 # 11\. Azure SQL Logging and Auditing

 Azure SQL auditing was configured to monitor database activity.

 The audit data provides visibility into:

 - Authentication failures
- SQL statements
- Database operations
- User accounts
- Client IP addresses
- Application names
- Host information
- Success/failure status
- Affected rows
- Security-relevant SQL operations


<img width="1296" height="539" alt="image" src="https://github.com/user-attachments/assets/844c77ac-7508-4cf0-9125-d5b84be6c21c" />


---

 # 12\. Log Analytics Workspace

 A centralized **Log Analytics Workspace** was created to collect Azure security and operational telemetry.

 Example telemetry sources:

```
Azure SQL
   │
   ├── SQLSecurityAuditEvents
   ├── Errors
   └── DatabaseWaitStatistics
         │
         ▼
Log Analytics Workspace
         │
         ├── Microsoft Sentinel
         └── Splunk
```

<img width="1296" height="438" alt="image" src="https://github.com/user-attachments/assets/4f74591c-7afc-4ec4-87b8-30c5db9992cd" />


<img width="1239" height="438" alt="image" src="https://github.com/user-attachments/assets/cc75312b-252e-468c-856c-6cefa445a664" />

---

 # 13\. Verify Azure Log Collection

 Azure diagnostic logging was validated by generating and querying activity within the healthcare database.

 The validation process included:

 1. Generate database activity
2. Verify diagnostic settings
3. Confirm logs arrive in Log Analytics
4. Query `AzureDiagnostics`
5. Validate timestamps
6. Validate database name
7. Validate SQL statement
8. Validate user identity
9. Validate source IP
10. Forward relevant telemetry to SIEM platforms


<img width="1120" height="1026" alt="image" src="https://github.com/user-attachments/assets/a81da0d0-56a2-4a08-8aa6-03f910a53e95" />



---

 # 14\. Configure Microsoft Entra ID for Splunk

 Microsoft Entra ID was incorporated into the architecture to provide identity-centric security monitoring.

 The integration supports monitoring of:

```
Identity
   │
   ├── Authentication
   ├── Authorization
   ├── Account activity
   └── Suspicious access
            │
            ▼
      Security Analytics
```

 This contributes to the **AAA security model**:

- **Authentication**
- **Authorization**
- **Accounting**

<img width="1239" height="525" alt="image" src="https://github.com/user-attachments/assets/aeddffea-6488-4be1-b1ae-27ff4844ae5e" />



---

 # 15\.  Data Collection Rule

 A Data Collection Rule (DCR) was configured to control telemetry collection and routing.

 The conceptual workflow is:

```
Azure Resource
      │
      ▼
Diagnostic / Monitoring Data
      │
      ▼
Data Collection Rule
      │
      ▼
Log Analytics Workspace
      │
      ├── Sentinel
      └── Splunk
```

<img width="1143" height="968" alt="image" src="https://github.com/user-attachments/assets/a7603933-78c4-4f1b-971b-0fb28ceb2713" />



---

Forwarded Database Logs to Workspace

<img width="1308" height="931" alt="image" src="https://github.com/user-attachments/assets/cb3f0cb8-7862-480a-a0de-2a29b00bbbc3" />


Create Input for Azure Log Analytic

<img width="1239" height="344" alt="image" src="https://github.com/user-attachments/assets/2b683cef-5dc8-4356-8a0b-9e3bf38a2dcd" />


 # 16\. Healthcare Database Security Detection

 One of the primary detection objectives was identifying suspicious activity against the `Patients` table.

 The following KQL query searches for potentially sensitive database operations:

```
AzureDiagnostics
| where TimeGenerated >= ago(15m)
| where Category == "SQLSecurityAuditEvents"
| where ResourceProvider == "MICROSOFT.SQL"
| where Resource has "HEALTHCARE-DATABASE"
| where statement_s has "Patients"
| where statement_s has_any (
    "INSERT",
    "UPDATE",
    "DELETE"
)
| project
    TimeGenerated,
    ResourceId,
    Category,
    DatabaseName = database_name_s,
    Action = action_id_s,
    SQLStatement = statement_s,
    User = server_principal_name_s,
    ClientIP = client_ip_s,
    Application = application_name_s,
    Host = host_name_s,
    Success = succeeded_s,
    AffectedRows = affected_rows_d
```

 ### Detection objective

 This query provides visibility into:

```
WHO?
  ↓
User / Principal

WHAT?
  ↓
INSERT / UPDATE / DELETE

WHERE?
  ↓
Patients table

FROM WHERE?
  ↓
Client IP

WHEN?
  ↓
Timestamp

RESULT?
  ↓
Success / Failure

IMPACT?
  ↓
Affected rows
```

---

 # 17\. Patient PII Access Detection

 A second detection searches for database activity involving sensitive patient information.

```
AzureDiagnostics
| where TimeGenerated >= ago(15m)
| where ResourceId =~ "/SUBSCRIPTIONS/<SUBSCRIPTION-ID>/RESOURCEGROUPS/<RESOURCE-GROUP>/PROVIDERS/MICROSOFT.SQL/SERVERS/healthcare-data-server/DATABASES/HealthCare-DataBase"
| where Category == "SQLSecurityAuditEvents"
| where statement_s has "Patients"
| where statement_s has_any (
    "INSERT",
    "DELETE",
    "UPDATE"
)
or statement_s has_any (
    "FirstName",
    "LastName",
    "SSN",
    "InsuranceNumber",
    "Email",
    "Phone",
    "Address"
)
| project
    TimeGenerated,
    ResourceId,
    Category,
    statement_s,
    session_server_principal_name_s,
    client_ip_s,
    affected_rows_d
```

 ### Security use case

 This detection helps identify potential:

 - Unauthorized PII access
- Patient-record modification
- Patient-record deletion
- Suspicious bulk operations
- Insider-threat indicators
- Compromised credentials

---

 # 18\. Advanced SQL Security Detection

 The following KQL detection combines multiple indicators of suspicious database activity.

```
AzureDiagnostics
| where TimeGenerated >= ago(15m)
| where ResourceId =~ "/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>/providers/Microsoft.Sql/servers/healthcare-data-server/databases/HealthCare-DataBase"
| where Category in~ (
    "SQLSecurityAuditEvents",
    "DatabaseWaitStatistics",
    "Errors"
)
| extend
    IsFailedLogin =
        (action_id_s == "LGIF" or status_s == "FAILED"),

    IsPermissionDenied =
        (action_id_s == "GDB"
         or error_code_d in (916, 229, 262)),

    IsLongRunning =
        (duration_d > 5000
         or duration_s > 5000),

    StatementUpper =
        toupper(statement_s)
| where
    IsFailedLogin
    or IsPermissionDenied
    or IsLongRunning
    or StatementUpper has_any (
        "SELECT",
        "INSERT",
        "UPDATE",
        "DELETE",
        "ALTER TABLE",
        "DROP TABLE",
        "BULK INSERT"
    )
    or StatementUpper has_any (
        "UNION SELECT",
        "' OR 1=1",
        "WAITFOR DELAY",
        "XP_CMDLOGON"
    )
| project
    TimeGenerated,
    database_name_s =
        case(
            isnotempty(database_name_s),
            database_name_s,
            "HealthCare-DataBase"
        ),
    user = session_server_principal_name_s,
    statement = statement_s,
    duration = duration_d,
    clientIP = client_ip_s,
    status = status_s,
    error_code = error_code_d,
    Category
```

 ### Detection categories

 | Detection | Security Meaning |
| --- | --- |
| Failed login | Potential credential attack |
| Permission denied | Possible unauthorized access |
| Long-running query | Potential resource abuse |
| DROP TABLE | Potential destructive activity |
| BULK INSERT | Potential data ingestion abuse |
| UNION SELECT | Potential SQL injection |
| `OR 1=1` | SQL injection indicator |
| WAITFOR DELAY | SQL injection/time-delay indicator |
| Patient-table modification | Potential unauthorized data manipulation |

 > These patterns are **indicators for investigation**, not proof that an attack occurred. Detection rules should be tuned against legitimate application behavior before being used for production alerting.

---

 # 19\.  Network Security Monitoring

 Network security is an additional monitoring layer.

 The architecture monitors:

 - Source IP
- Destination IP
- Destination port
- Network flow
- VNet
- Subnet
- NSG decisions
- Azure Firewall events
- Blocked connections
- Allowed connections
- Database connectivity

 A key security scenario is monitoring traffic targeting SQL Server on:

```
TCP/1433
```

---

 # 20\. Azure Firewall & NSG Monitoring

 The network-security use case is designed around:

```
Internet
   │
   ▼
Azure Firewall
   │
   ▼
VNet
   │
   ├── Application Subnet
   │
   ├── Database Subnet
   │
   └── Splunk/Security Subnet
          │
          ▼
       Azure SQL
```

 Security controls include:

 - Network segmentation
- NSG rules
- Firewall rules
- Restricted database access
- Logging of allowed/blocked traffic
- Monitoring of TCP/1433 connections

---

 # 21\.  KQL — Network Security / Port 1433 Monitoring

 The following query can be adapted for a Log Analytics workspace containing Azure Firewall and/or NSG-related network telemetry.

```
AzureDiagnostics
| where TimeGenerated >= ago(15m)
| where Category has_any (
    "AzureFirewallNetworkRule",
    "AzureFirewallApplicationRule",
    "NetworkSecurityGroupEvent",
    "NetworkSecurityGroupRuleCounter"
)
| extend
    SourceIP = coalesce(
        tostring(msg_s),
        tostring(src_ip_s),
        tostring(SourceIP)
    )
| where
    tostring(msg_s) has "1433"
    or tostring(dst_port_s) == "1433"
    or tostring(DestinationPort) == "1433"
| project
    TimeGenerated,
    ResourceId,
    Category,
    SourceIP,
    DestinationIP = coalesce(
        tostring(dst_ip_s),
        tostring(DestinationIP)
    ),
    DestinationPort = coalesce(
        tostring(dst_port_s),
        tostring(DestinationPort)
    ),
    Action = coalesce(
        tostring(action_s),
        tostring(Action)
    ),
    Message = msg_s
| order by TimeGenerated desc
```

 ### Important implementation note

 Azure Firewall and NSG telemetry can use different schemas depending on the diagnostic configuration and log-generation mechanism.

 Therefore, the final production query should be validated against the actual tables in the workspace.

 For environments using modern **Azure Resource-Specific tables**, query the corresponding Firewall/NSG tables rather than assuming all network events are stored in `AzureDiagnostics`.

---

 # 22\.  Network Investigation Workflow

 A security analyst can investigate suspicious database access using:

```
Suspicious Source IP
        │
        ▼
Network Flow
        │
        ▼
Firewall / NSG Decision
        │
        ▼
Destination Port
        │
        ▼
TCP/1433
        │
        ▼
Azure SQL Server
        │
        ▼
SQL Audit Event
        │
        ▼
User / Principal
        │
        ▼
SQL Statement
        │
        ▼
Patient Data Access
        │
        ▼
Security Incident
```

 This provides an end-to-end investigation path from:

 **Network → Identity → Database → Data Access**

---

 # 23\. Security Dashboards

 The project includes dashboards designed around the major security use cases.


# Create the Dashboard for Logs analytics

<img width="1731" height="967" alt="image" src="https://github.com/user-attachments/assets/464372b0-2b90-4999-be06-e648649ccac2" />





 ## Dashboard 1 — Healthcare Database Security

 Metrics:

 - SQL activity
- Failed logins
- Permission denied events
- Patient-table activity
- Database errors
- Long-running queries
- Source IPs
- Database users

---

 ## Dashboard 2 — Patient PII Access

 Visualizations:

 - Number of PII access events
- Users accessing patient records
- Source IP addresses
- SQL operations
- Affected rows
- INSERT / UPDATE / DELETE activity
- Activity over time

---

 ## Dashboard 3 — Network Security

 Visualizations:

 - Allowed connections
- Blocked connections
- Top source IPs
- Destination IPs
- Destination ports
- TCP/1433 activity
- Firewall actions
- NSG actions

---

 ## Dashboard 4 — Security Alerts

 Metrics:

```
Critical Alerts
High Alerts
Medium Alerts
Low Alerts
```

 Potential security detections:

 - Failed authentication
- Permission violations
- Suspicious SQL statements
- Patient PII modification
- Network scanning
- Unauthorized port access
- Firewall blocks

---

 # 24\.  Multi-Platform SIEM Integration

 The project demonstrates how multiple security platforms can coexist.

```
                         SECURITY TELEMETRY
                                │
          ┌─────────────────────┼─────────────────────┐
          │                     │                     │
          ▼                     ▼                     ▼
     Azure SQL             Azure Network          Entra ID
          │                     │                     │
          └─────────────────────┼─────────────────────┘
                                │
                                ▼
                       Log Analytics
                                │
                ┌───────────────┴───────────────┐
                │                               │
                ▼                               ▼
       Microsoft Sentinel                Splunk Enterprise
                │                               │
                ▼                               ▼
          Detection / SOC                 SIEM Analytics
                │                               │
                └───────────────┬───────────────┘
                                ▼
                        Security Investigation
```

 This architecture provides **defense in depth at the monitoring layer**, allowing security teams to analyze the same security domain through complementary platforms.

---

 # 25\. Security Architecture Principles

 The project follows several core cybersecurity principles.

 ### Defense in Depth

 Multiple security layers are deployed:

```
Identity
   ↓
Network
   ↓
Firewall
   ↓
NSG
   ↓
Database
   ↓
Audit Logging
   ↓
SIEM
   ↓
Detection
   ↓
Investigation
```

 ### Zero Trust

 The architecture assumes:

 > **Never trust implicitly. Always verify.**

 Security decisions should consider:

 - Identity
- Device/context
- Network location
- Resource
- Application
- Permissions
- Data sensitivity

 ### CIA Triad

 | Principle | Implementation |
| --- | --- |
| Confidentiality | IAM, network restrictions, database controls |
| Integrity | SQL auditing, monitoring, security alerts |
| Availability | Azure infrastructure and monitoring |

---

 # 26\.  Future Agentic-AI Security Extension

 The proposed architecture can be extended to protect AI-enabled healthcare systems.

 Future architecture:

```
Patient
   │
   ▼
Healthcare Application
   │
   ▼
AI Agent
   │
   ├── Authentication
   ├── Authorization
   ├── Prompt Validation
   ├── API Security
   └── Data Access Policy
            │
            ▼
       Healthcare APIs
            │
            ▼
       Patient Database
            │
            ▼
       Security Telemetry
            │
            ▼
     Sentinel + Splunk
```

 Potential future detections include:

 - Prompt injection
- Excessive AI-agent permissions
- Abnormal API calls
- Unauthorized patient-data retrieval
- Large-volume patient-data queries
- AI-agent credential abuse
- Cross-tenant access attempts
- Sensitive data leakage

---

 # 27\. Penetration Testing / Validation Scenarios

 The security architecture can be validated using controlled security scenarios.

 | Scenario | Expected Security Control |
| --- | --- |
| Failed SQL authentication | SQL Audit + SIEM |
| Unauthorized database access | SQL Audit + Defender |
| Attempted access to TCP/1433 | NSG / Firewall |
| Blocked network connection | Firewall / NSG logs |
| Patient record modification | SQL Audit |
| Patient record deletion | SQL Audit |
| Suspicious SQL syntax | KQL detection |
| Permission violation | SQL Audit |
| High-volume database activity | SIEM analytics |
| Suspicious source IP | Network + SIEM correlation |

 All penetration testing should be conducted only against systems for which authorization has been explicitly granted.

---

 # 28\. End-to-End Implementation Workflow

```
1. Define healthcare security requirements
             ↓
2. Create Azure Resource Group
             ↓
3. Design VNet and subnets
             ↓
4. Configure NSGs
             ↓
5. Deploy Azure Firewall
             ↓
6. Create Azure SQL Server
             ↓
7. Create HealthCare-DataBase
             ↓
8. Create Patients table
             ↓
9. Configure SQL auditing
             ↓
10. Deploy Log Analytics Workspace
             ↓
11. Configure Diagnostic Settings
             ↓
12. Verify Azure telemetry
             ↓
13. Deploy Defender for Cloud
             ↓
14. Configure Microsoft Entra ID
             ↓
15. Create Data Collection Rules
             ↓
16. Deploy Splunk Enterprise VM
             ↓
17. Configure Splunk indexes
             ↓
18. Forward Azure telemetry
             ↓
19. Develop KQL detections
             ↓
20. Develop Splunk searches
             ↓
21. Create security dashboards
             ↓
22. Generate controlled security events
             ↓
23. Validate detections
             ↓
24. Investigate alerts
             ↓
25. Document findings
```

---

 # 29\.  Project Outcomes

 The project demonstrates the ability to:

 - Design a cloud-based SOC architecture
- Deploy security infrastructure in Azure
- Secure a healthcare database environment
- Implement Azure SQL auditing
- Centralize security telemetry
- Configure Log Analytics
- Implement cloud security monitoring
- Deploy Microsoft Defender for Cloud
- Configure Microsoft Sentinel
- Deploy Splunk Enterprise
- Design SIEM indexes
- Develop KQL detection rules
- Monitor network security
- Investigate TCP/1433 activity
- Detect suspicious SQL operations
- Monitor patient PII access
- Correlate network and database events
- Build security dashboards
- Apply Defense-in-Depth principles
- Apply Zero Trust concepts
- Design healthcare-focused security use cases

---

 # 30\.  Key Security Capabilities Demonstrated

 | Capability | Implementation |
| --- | --- |
| Cloud Security | Azure + Defender for Cloud |
| SIEM | Sentinel + Splunk |
| Network Security | Azure Firewall + NSGs |
| Database Security | Azure SQL + Auditing |
| Identity Security | Microsoft Entra ID |
| Log Management | Log Analytics |
| Detection Engineering | KQL |
| Threat Monitoring | Sentinel / Defender / Splunk |
| PII Monitoring | Patient-table activity detection |
| Network Monitoring | Firewall / NSG telemetry |
| Security Analytics | Splunk + Sentinel |
| SOC Operations | Alerts, dashboards and investigation |
| Compliance Support | Auditability and centralized monitoring |

---

 # 31\.Security  Area covered: 

 ### Cloud Security

 - Microsoft Azure
- Azure networking
- Azure SQL
- Azure Firewall
- NSGs
- Defender for Cloud

 ### SIEM / SOC

 - Microsoft Sentinel
- Splunk Enterprise
- Log Analytics
- Security dashboards
- Security alerting
- Log ingestion

 ### Detection Engineering

 - Kusto Query Language (KQL)
- SQL security monitoring
- Network security analytics
- PII access detection
- Authentication monitoring
- Threat hunting

 ### Identity & Access

 - Microsoft Entra ID
- Authentication
- Authorization
- AAA security model
- Zero Trust concepts

 ### Security Architecture

 - Defense in Depth
- CIA Triad
- Cloud SOC design
- Security telemetry architecture
- Healthcare security
- Incident investigation


 # 33\. Security & Privacy Notice

 This repository should contain **synthetic healthcare data only**.

 Do not commit:

 - Real patient information
- Real SSNs
- Real insurance numbers
- Real credentials
- API keys
- Passwords
- Azure secrets
- Private certificates
- Production IP addresses
- Connection strings
- Splunk tokens


 # 34\.  Conclusion

 This capstone project demonstrates the design and implementation of a **multi-platform cloud SOC architecture for healthcare data protection**.

 By combining:

```
Azure
+
Azure SQL
+
Azure Firewall
+
NSGs
+
Entra ID
+
Defender for Cloud
+
Log Analytics
+
Microsoft Sentinel
+
Splunk Enterprise
```

 the project establishes a layered security architecture capable of collecting, analyzing, detecting, and investigating security events across **identity, network, database, and cloud infrastructure**.

 The project demonstrates how security telemetry can be transformed into actionable detections for healthcare-specific threats such as unauthorized patient-data access, suspicious SQL activity, network attacks, authentication failures, and potential data-exfiltration scenarios.

 The architecture also establishes a foundation for future integration of **Agentic AI security controls**, including AI-agent authorization, healthcare API monitoring, prompt-injection detection, and AI-driven patient-data protection.


 ## Highlights

 **Cloud:** Microsoft Azure\
 **Security:** Defender for Cloud, Azure Firewall, NSG\
 **SIEM:** Microsoft Sentinel, Splunk Enterprise\
 **Database:** Azure SQL Database\
 **Identity:** Microsoft Entra ID\
 **Monitoring:** Azure Monitor, Log Analytics\
 **Detection:** KQL, SQL Audit Analytics\
 **Security Domains:** Cloud Security, Network Security, Database Security, IAM, SIEM, SOC, Threat Detection, Healthcare Security

---

 ### Author

 **David R. Gnimpieba Z.**

 **Cybersecurity Program — Capstone Project**

 **Project:**Cloud SOC Architecture & Healthcare Data Protection

