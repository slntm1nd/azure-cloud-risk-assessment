# Cloud Security Risk Assessment & GRC Simulation (Azure)

## 📌 Project Overview
This project simulates a comprehensive Governance, Risk, and Compliance (GRC) assessment for a small cloud workload hosted on Microsoft Azure. The primary objective was to define the assessment scope, identify high-risk assets, map threat scenarios, detect infrastructure vulnerabilities, and quantify risks using a standardized repeatable scoring model ($Risk = Likelihood \times Impact$).

---

## 🛠️ Environment & Scope
- **Target Asset:** Azure Virtual Machine (`GRC-WIN-VM01`) running Windows Server 2022.
- **Infrastructure Setup:** Virtual Network (VNet), Network Security Group (NSG), Public IP enabled.
- **Baseline Configuration:** Default OS configuration with standard Windows Defender and Firewall settings (no initial CIS Benchmarks applied).

---

## 🔍 Phase 1: Asset, Threat, & Vulnerability Identification

### 1. Identified Assets
| Asset Category | Asset | Security Significance |
| :--- | :--- | :--- |
| **Compute** | Azure VM (Windows Server 2022) | Hosts core data & application services. |
| **Identity** | Local Admin Account (`azureadmin`) | Provides full administrative and system control. |
| **Network** | Public IP & RDP Port (TCP 3389) | Direct external entry point from the internet. |
| **Cloud Control** | Azure Subscription | Grants management, configuration, and billing access. |

### 2. Threat Modeling & Vulnerabilities
- **Threat Scenario:** External internet brute-force attacks via automated bots targeting the exposed RDP port.
- **Vulnerability Detected:** Network Security Group (NSG) allowed inbound RDP traffic (Port 3389) from **'Any' / 'Internet'** source.
- **Identity Vulnerability:** Lack of Multi-Factor Authentication (MFA) for the local administrator account, increasing password compromise risk.
- **Monitoring Gap:** Relied heavily on default OS-level Event Viewer logging without centralized SIEM/Log Analytics workspace integration.

---

## 📊 Phase 2: Risk Scoring Matrix
Using a standard GRC qualitative-quantitative matrix (Scale 1-5):

| Risk Description | Likelihood (1-5) | Impact (1-5) | Risk Score ($L \times I$) | Criticality |
| :--- | :---: | :---: | :---: | :--- |
| Internet Brute-Force via exposed RDP | 5 | 4 | **20** | **CRITICAL** |
| Local Admin credential stuffing (No MFA) | 4 | 5 | **20** | **CRITICAL** |
| Delayed Incident Detection (Default logs) | 3 | 3 | **9** | **MEDIUM** |

---

## 🎯 Key Takeaways & GRC Competencies Demonstrated
- **Attack Surface Reduction:** Documented the severe risks of leaving default RDP ports open to the entire internet.
- **Risk Communication:** Translated technical misconfigurations (NSG rules, missing MFA) into a structured risk register easily understood by executive leadership.
- **Cloud Hygiene:** Demonstrated practical knowledge of Azure Portal navigation, asset inventorying, and security group auditing.
