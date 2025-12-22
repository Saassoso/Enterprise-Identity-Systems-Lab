# Day 8: Identity Lifecycle (JML) Design

## 1. Project Overview
**Objective:** standardize the creation and removal of identities to prepare for automation.

**Scope:** Automated provisioning for Employees and Contractors.

## 2. Naming Convention Standards
To ensure consistency, all scripts must follow this format:

| Attribute | Format / Rule | Example |
| :--- | :--- | :--- |
| **SamAccountName** | `FirstInitial.LastName` | `j.doe` |
| **DisplayName** | `FirstName LastName` | `John Doe` |
| **UPN (Email)** | `FirstInitial.LastName@lab.local` | `j.doe@lab.local` |
| **Password** | Random 12-char or Default (ChangeMe123!) | `Start123!` |

## 3. Provisioning Logic (The "Joiner" Matrix)
The automation script will check the "Department" and "Type" to decide access.

| Role Type | Department | Target OU | Primary Groups | Home Drive |
| :--- | :--- | :--- | :--- | :--- |
| **Employee** | **HR** | `_CORP\HR` | `GG_HR_Staff` | `\\DC01\Homes\HR\%username%` |
| **Employee** | **Finance** | `_CORP\Finance` | `GG_Finance_Staff` | `\\DC01\Homes\Fin\%username%` |
| **Employee** | **IT** | `_CORP\IT` | `GG_IT_Team` | `\\DC01\Homes\IT\%username%` |
| **Contractor** | *(Any)* | `_CORP\Contractors` | `GG_Contractors` | *(None - Cloud Only)* |

## 4. De-Provisioning Logic (The "Leaver" Workflow)
When a user is marked "Terminated" in the source (CSV):
1.  **Disable** the Active Directory account immediately.
2.  **Move** the object to `_CORP\Terminated_Users` OU.
3.  **Clear** the "Description" and add: `Terminated [Date]`.
4.  **Remove** from all Security Groups to prevent "Ghost Access."

## 5. Automation Strategy
**Tool:** PowerShell (Active Directory Module).

**Input Source:** `NewHires.csv` (Simulating an HR Data Feed).

**Schedule:** Daily at 06:00 AM (Simulated).
