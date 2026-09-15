# Microsoft Intune Endpoint Management Lab

## Overview

This project demonstrates a hands-on Microsoft Intune endpoint management environment using Microsoft Entra ID, Microsoft Intune, Microsoft 365 Business Premium, and a Windows 11 Pro virtual machine running in Oracle VirtualBox.

The purpose of this lab was to simulate common tasks performed by IT Support, Help Desk, Desktop Support, Endpoint Administrators, and Junior System Administrators in a Microsoft cloud environment.

The lab includes:

- Microsoft Intune administration
- Microsoft Entra ID device enrollment
- Windows 11 endpoint management
- Device security groups
- Configuration policy deployment
- Compliance policy configuration
- Microsoft Defender compliance checks
- Application deployment
- Device synchronization
- Remote device actions
- Conditional Access configuration
- Microsoft Entra sign-in monitoring
- Microsoft Intune troubleshooting

---

## Lab Environment

| Component | Purpose |
|---|---|
| Microsoft Intune | Cloud endpoint management |
| Microsoft Entra ID | Identity and device management |
| Microsoft 365 Business Premium | Licensing for Intune and Microsoft cloud services |
| Windows 11 Pro | Managed client endpoint |
| Oracle VirtualBox | Virtualization platform |
| Microsoft Defender | Endpoint security and compliance |
| Company Portal | Intune-managed application |

### Lab Objects

| Object | Name |
|---|---|
| Windows Device | `VMPC` |
| Test User | `John Wick` |
| Device Security Group | `Intune-Lab-Devices` |
| Configuration Policy | `Windows Security Baseline - Lab` |
| Compliance Policy | `Windows Compliance Policy - Lab` |
| Conditional Access Policy | `Require Compliant Windows Device - Lab` |

> `John Wick` was created as a fictional test user for this lab.

---

# Lab Architecture

```text
Microsoft Entra ID
        |
        |
Microsoft Intune
        |
        |
Intune-Lab-Devices
        |
        |
Windows 11 VM - VMPC
        |
        +---- Configuration Policies
        |
        +---- Compliance Policies
        |
        +---- Application Deployment
        |
        +---- Remote Device Management
        |
        +---- Monitoring and Troubleshooting
```

---

# 1. Microsoft Intune Admin Center

The lab began by verifying access to the Microsoft Intune Admin Center.

The dashboard provides administrators with information about:

- Device compliance
- Configuration policy status
- Application installation failures
- Connector errors
- Service health
- Tenant account status

![Microsoft Intune Admin Center](Microsoft%20Intune/01-Intune-Admin-Center.png)

The tenant showed an active and healthy Intune environment.

---

# 2. Create an Intune Device Security Group

A Microsoft Entra security group named:

`Intune-Lab-Devices`

was created for this lab.

Configuration:

- Type: Security
- Membership type: Assigned
- Source: Cloud

![Intune Device Group](Microsoft%20Intune/02-Intune-Lab-Device-Group.png)

The group was used as the target for device configuration policies, compliance policies, and application deployment.

Using a dedicated security group allows administrators to test policies on selected devices instead of deploying them to an entire organization.

---

# 3. Configure Automatic MDM Enrollment

Automatic Microsoft Intune enrollment was configured.

The MDM user scope was set to:

`All`

![Automatic Enrollment](Microsoft%20Intune/03-Automatic-Enrollment.png)

This allows eligible users to automatically enroll supported Windows devices into Microsoft Intune when they connect them to the organization's Microsoft Entra environment.

---

# 4. Verify Microsoft Intune Licensing

The test user was assigned:

`Microsoft 365 Business Premium`

![Intune User License](Microsoft%20Intune/04-Intune-User-License.png)

Microsoft 365 Business Premium provides access to Microsoft Intune and other Microsoft cloud management capabilities required for this lab.

---

# 5. Join Windows 11 to Microsoft Entra ID

A Windows 11 Pro virtual machine was created using Oracle VirtualBox.

The organizational test account was used to connect the Windows device to Microsoft Entra ID.

The connection was verified under:

`Settings > Accounts > Access work or school`

![Windows Work Account Connected](Microsoft%20Intune/05-Windows-Work-Account-Connected.png)

Windows confirmed that the device was connected to the organization's Microsoft Entra ID environment.

---

# 6. Verify Intune Device Enrollment

After joining Microsoft Entra ID, the Windows 11 VM appeared in the managed device inventory.

Device name:

`VMPC`

The device showed:

- Operating system: Windows
- Device action: Managed
- Management type: Fully managed

![Intune Enrolled Device](Microsoft%20Intune/06-Intune-Enrolled-Device.png)

This confirmed that the Windows endpoint had successfully enrolled into device management.

---

# 7. Verify Fully Managed Device Status

The VMPC device details were reviewed to verify that Microsoft Intune was managing the endpoint.

The device showed:

- Windows operating system
- Fully managed status
- Successful Intune management
- Organizational ownership

![Fully Managed Device](Microsoft%20Intune/07-Fully-Managed-Device-Details.png)

A fully managed endpoint allows administrators to centrally deploy security settings, applications, compliance requirements, and remote management actions.

---

# 8. Add VMPC to the Intune Device Group

The Windows device was added to:

`Intune-Lab-Devices`

The device properties confirmed:

- Join type: Microsoft Entra joined
- MDM: Microsoft Intune
- Security settings management: Microsoft Intune
- Compliance: Yes
- Group: Intune-Lab-Devices

![Device Group Membership](Microsoft%20Intune/08-Device-Group-Membership.png)

This group was later used to target the endpoint with Intune policies and applications.

---

# 9. Create a Windows Security Configuration Policy

A Windows configuration profile was created using the Microsoft Intune Settings Catalog.

Policy name:

`Windows Security Baseline - Lab`

The following setting was configured:

`Interactive Logon Machine Inactivity Limit = 900`

The value `900` represents:

`900 seconds = 15 minutes`

This setting automatically locks the Windows session after 15 minutes of inactivity.

The configuration policy was assigned to:

`Intune-Lab-Devices`

This demonstrated centralized Windows security configuration using Microsoft Intune.

---

# 10. Force a Device Synchronization

A manual synchronization was triggered from the Microsoft Intune Admin Center.

The synchronization completed successfully.

The sync processed:

- Device notification
- Policies
- Applications

![Device Sync Successful](Microsoft%20Intune/10-Device-Sync-Successful.png)

Manual synchronization is useful when administrators need a managed endpoint to retrieve newly assigned settings without waiting for the normal device check-in cycle.

---

# 11. Verify Configuration Policy Deployment

The device configuration report was reviewed after synchronization.

The policy:

`Windows Security Baseline - Lab`

reported:

`Succeeded`

for both the logged-in user context and the system account context.

![Security Policy Applied](Microsoft%20Intune/11-Security-Policy-Applied.png)

This confirmed that the Windows security configuration was successfully delivered to the VMPC endpoint.

---

# 12. Create a Windows Compliance Policy

A Windows compliance policy was created.

Policy name:

`Windows Compliance Policy - Lab`

The following security requirements were configured:

| Security Setting | Requirement |
|---|---|
| Firewall | Required |
| Antivirus | Required |
| Antispyware | Required |
| Microsoft Defender Antimalware | Required |
| Real-time protection | Required |

The policy was assigned to:

`Intune-Lab-Devices`

The action for noncompliance was configured to mark a device noncompliant immediately if it failed the configured requirements.

After synchronization and evaluation, Intune reported:

- Compliant: 1
- Noncompliant: 0
- Total: 1

![Compliance Policy Applied](Microsoft%20Intune/12-Compliance-Policy-Applied.png)

This demonstrated how Microsoft Intune can continuously evaluate the security posture of managed endpoints.

---

# 13. Deploy Company Portal Using Microsoft Intune

Microsoft Company Portal was deployed using:

`Microsoft Store app (new)`

The application was configured with:

- Application: Company Portal
- Install behavior: System
- Assignment type: Required
- Target group: Intune-Lab-Devices

After synchronization, Intune offered the application to the managed Windows device.

![Company Portal Deployment](Microsoft%20Intune/13-Company-Portal-Deployed.png)

This demonstrated centralized application deployment without manually installing the application on the endpoint.

---

# 14. Verify Company Portal Installation

The managed applications report was reviewed after deployment.

Company Portal showed:

- Resolved intent: Required install
- Installation status: Installed

![Company Portal Installed](Microsoft%20Intune/14-Company-Portal-Installed.png)

This confirmed that Microsoft Intune successfully deployed the application to the Windows 11 endpoint.

---

# 15. Perform a Remote Device Restart

Microsoft Intune provides administrators with remote management capabilities for enrolled devices.

A remote restart command was issued to:

`VMPC`

The Microsoft Intune notification center confirmed:

`Restart initiated`

![Remote Restart Successful](Microsoft%20Intune/15-Remote-Restart-Successful.png)

This demonstrates how administrators can remotely manage endpoints without requiring physical access to the computer.

Other remote actions available in Microsoft Intune include:

- Sync
- Restart
- Collect diagnostics
- Retire
- Remove company data
- Wipe

Destructive actions such as Wipe and Remove company data were intentionally not executed in this lab.

---

# 16. Conditional Access

A Microsoft Entra Conditional Access policy was configured.

Policy name:

`Require Compliant Windows Device - Lab`

The policy was designed to evaluate:

- The test user
- Windows devices
- Device compliance status
- Access to organizational resources

The Grant control was configured to:

`Require device to be marked as compliant`

The Conditional Access policy was kept in:

`Report-only`

mode.

Report-only mode allows an administrator to test how a Conditional Access policy would behave without actually blocking user access.

The policy was intentionally not enabled for enforcement during this lab to avoid accidentally locking the test account out of the tenant.

---

# 17. Microsoft Entra Sign-In Monitoring

Microsoft Entra Sign-In Logs were used to monitor authentication activity.

The logs provide information such as:

- User
- Application
- Sign-in status
- Error code
- Conditional Access status
- Authentication activity

![Microsoft Entra Sign-In Logs](Microsoft%20Intune/17-Sign-In-Logs.png)

Sign-In Logs are useful for troubleshooting authentication failures and investigating account activity.

During the lab, access to Sign-In Logs initially required additional reporting permissions.

The built-in:

`Reports Reader`

role was assigned to the administrative account.

After signing out and signing back into Microsoft Entra, the sign-in activity became visible.

This provided hands-on experience with Microsoft Entra role-based access control and monitoring permissions.

---

# 18. Microsoft Intune Troubleshooting

The Microsoft Intune:

`Troubleshooting + support`

interface was used to investigate the managed user and endpoint.

![Intune Troubleshooting](Microsoft%20Intune/18-Intune-Troubleshooting.png)

The troubleshooting dashboard showed:

## Policy Status

- Compliant: 2
- Error: 0
- Noncompliant: 0
- Conflict: 0
- Pending: 0

## Compliance Status

- Compliant: 2
- Error: 0
- Noncompliant: 0
- Conflict: 0
- Pending: 0

## Application Status

- Installed: 1
- Failed: 0
- Waiting for install status: 0

## Device Status

- Enrolled: 1
- Disabled: 0
- Offline: 0
- Noncompliant: 0
- Enrollment failures: 0

This dashboard provides IT support technicians with a centralized location for investigating user, policy, compliance, application, and enrollment problems.

---

# Device Offboarding

Microsoft Intune provides several options for removing organizational management from a device.

These include:

- Retire
- Remove company data
- Wipe
- Delete

The offboarding features were reviewed but intentionally not executed because the goal was to preserve the working Intune lab environment.

Before considering destructive actions, a VirtualBox snapshot was created.

Snapshot name:

`Intune-Lab-Before-Offboarding`

This allows the fully configured virtual machine to be restored if required.

---

# Troubleshooting Performed During the Lab

## Device Group Membership

During the initial group configuration, a Microsoft 365 group interface was opened instead of the Microsoft Entra security group interface.

The correct Microsoft Entra security group was then located.

The Windows device was successfully added to:

`Intune-Lab-Devices`

This demonstrated the difference between user-focused Microsoft 365 groups and security groups used for device targeting.

---

## Compliance Policy Reporting Delay

After the compliance policy was created, the report initially showed:

`0 devices`

The endpoint was manually synchronized and given time to process the new compliance assignment.

After Intune completed the evaluation, the report updated to:

`Compliant: 1`

This demonstrated that Microsoft Intune reporting and policy evaluation are not always immediate.

---

## Microsoft Entra Sign-In Log Permissions

Microsoft Entra Audit Logs were available, but Sign-In Logs initially did not display authentication activity.

The administrative account was assigned the built-in:

`Reports Reader`

role.

After signing out and signing back into Microsoft Entra, Sign-In Logs became visible.

This demonstrated the importance of Microsoft Entra role-based access control when accessing monitoring and reporting information.

---

# Security and Privacy

Before publishing the project to GitHub, sensitive or unnecessary identifiers were removed from screenshots.

The following information was hidden where applicable:

- Email addresses
- User principal names
- Public IP addresses
- Geographic sign-in information
- Device IDs
- Object IDs
- Device serial numbers
- Other unnecessary tenant-specific identifiers

No passwords, authentication tokens, BitLocker recovery keys, API keys, secrets, or other credentials are included in this repository.

---

# Skills Demonstrated

This project demonstrates practical experience with:

### Microsoft Intune

- Intune Admin Center
- Windows device enrollment
- Device management
- Device synchronization
- Configuration profiles
- Settings Catalog
- Compliance policies
- Application deployment
- Managed applications
- Remote device actions
- Troubleshooting and support

### Microsoft Entra ID

- Microsoft Entra Join
- Users
- Security groups
- Device objects
- Group membership
- Conditional Access
- Sign-In Logs
- Administrative roles
- Role-based access control

### Windows Administration

- Windows 11 Pro
- Work or school account connection
- Cloud device enrollment
- Security policy deployment
- Microsoft Defender compliance
- Remote device management

### Microsoft 365

- Microsoft 365 Business Premium licensing
- Cloud identity
- Endpoint management integration

### Virtualization

- Oracle VirtualBox
- Windows 11 VM
- Virtual machine snapshots
- Lab environment recovery

---

# Real-World Scenario

This lab simulates an organization issuing a new Windows laptop to an employee.

A typical endpoint management workflow can include:

1. Create the employee identity in Microsoft Entra ID.
2. Assign the required Microsoft 365 license.
3. Join the Windows computer to Microsoft Entra ID.
4. Automatically enroll the endpoint into Microsoft Intune.
5. Add the device to the appropriate security group.
6. Deploy company security configuration.
7. Evaluate the endpoint using compliance policies.
8. Automatically deploy required applications.
9. Monitor the device remotely.
10. Perform remote support actions when required.
11. Investigate authentication activity using Sign-In Logs.
12. Troubleshoot device, policy, application, and compliance issues.
13. Retire or wipe the device when it is no longer required.

This allows organizations to centrally manage Windows endpoints without requiring direct physical access to every computer.

---

# Project Results

The completed lab successfully demonstrated a cloud-managed Windows endpoint environment.

The Windows 11 VM was successfully:

- Joined to Microsoft Entra ID
- Enrolled into Microsoft Intune
- Registered as a fully managed corporate device
- Added to a Microsoft Entra security group
- Assigned a Windows configuration policy
- Successfully synchronized with Intune
- Configured with an inactivity security policy
- Evaluated with a compliance policy
- Reported as compliant
- Assigned Microsoft Company Portal
- Successfully installed Company Portal remotely
- Restarted using a remote Intune action
- Monitored using Microsoft Entra Sign-In Logs
- Reviewed using Microsoft Intune Troubleshooting + Support

The project provided practical experience with modern cloud-based endpoint administration and troubleshooting.

---

# Technologies Used

- Microsoft Intune
- Microsoft Entra ID
- Microsoft 365 Business Premium
- Windows 11 Pro
- Microsoft Defender
- Microsoft Company Portal
- Microsoft Entra Conditional Access
- Microsoft Entra Sign-In Logs
- Oracle VirtualBox

---

# Key Takeaways

This lab provided hands-on experience with the complete lifecycle of a cloud-managed Windows endpoint.

Important concepts practiced include:

- Device enrollment
- Identity-based device management
- Security group targeting
- Centralized configuration
- Compliance enforcement
- Software deployment
- Remote support
- Conditional Access
- Authentication monitoring
- Role-based access control
- Endpoint troubleshooting

These technologies and workflows are commonly used in modern enterprise IT environments.

---

# Author

**Gurveer Singh**

Computer Information Systems / IT

Areas of interest:

- IT Support
- Help Desk
- Desktop Support
- Microsoft 365 Administration
- Microsoft Intune
- Microsoft Entra ID
- Windows Administration
- Networking
- System Administration
