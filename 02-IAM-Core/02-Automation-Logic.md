# Automated Identity Provisioning

## 1. Automation Overview
**Objective:** Eliminate manual user creation to reduce human error and ensure standardization.
**Tool:** PowerShell Script `Onboard-Users.ps1`.
**Input:** CSV Data Feed mimicking an HR Information System (HRIS).

## 2. Script Logic Flow
The script follows this JML decision tree:
1.  **Import Data:** Reads `NewHires.csv`.
2.  **Generate ID:** Formats username as `firstname.lastname`.
3.  **Determine Scope:** Matches "Department" column to AD Organizational Unit (OU).
4.  **Provision:**
    * Creates AD Object.
    * Sets temporary password.
    * Enforces "Change on Next Logon".
5.  **Assign Access:** Adds user to the correct Department Security Group.

## 3. Execution Evidence
Executed the onboarding script for a batch of 5 new employees.

![PowerShell Script Output](./attachments/powershell-onboarding.png)

![AD Verification-Alice](./attachments/alice-users-created.png)
*(Screenshot of ADUC showing Alice in HR)*

![AD Verification-David](./attachments/david-users-created.png)
*(Screenshot of ADUC David in Contractors)*

## 4. "Failure Lab" Observation
**Incident:** User `Eve Evil` (Management Dept) was processed but not placed in a specific OU.
**Root Cause:** The script's `if/elseif` logic did not have a defined rule for "Management."
**System Behavior:** The script triggered the `else` "Safety Net" clause and dumped the user in the default container.
**Fix Required:** Update JML Logic Matrix to include Executive Management rules.
![AD Failure](./attachments/eve-users-created.png)

---
*Scripted by: Saad Charif | Date: Dec 2025*