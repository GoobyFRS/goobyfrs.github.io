---
layout: minimal
title: BYOD Policy
nav_enabled: false
parent: Handbook
grand_parent: SMB Project
nav_order: 1
---
# Bring Your Own Device (BYOD) Policy

## Purpose

This Bring Your Own Device (BYOD) Policy establishes the minimum security and operational requirements for employees and contractors who access company systems, applications, or data using personally owned devices while working remotely or in a hybrid environment.

The purpose of this policy is to protect company information, reduce cybersecurity risk, and ensure secure connectivity to internal resources.

## Scope

This policy applies to all employees, contractors, vendors, and temporary staff who use personally owned devices to access company resources, including but not limited to:

- Email systems
- Internal web applications
- File shares and cloud platforms
- Administrative systems
- SD-WAN or remote access environments
- Communication platforms

Covered device types include:

- Windows laptops/desktops
- macOS devices
- Linux workstations
- Mobile phones and tablets

## Approved Remote Access Methods

All remote access to company systems must use approved secure connectivity platforms.

### Current Approved Technologies

- Tailscale (required) for secure SD-WAN and private network access
- MFA (Multi-Factor Authentication) must be enabled where supported

### Optional / Future Security Controls

The company may require additional endpoint security services such as:

- Cloudflare WARP
- DNS filtering
- Zero Trust Network Access (ZTNA)
- Secure Web Gateway (SWG) solutions

At this time, Tailscale provides encrypted connectivity and device identity management, but it does **not** replace endpoint protection or anti-malware requirements.

## Device Security Requirements

All personal devices used for work purposes must meet the following minimum requirements:

### Operating System

Devices must:

- Run a supported and actively maintained operating system
- Have automatic security updates enabled
- Be fully patched with current security updates

Unsupported or end-of-life operating systems are prohibited.

### Anti-Malware Protection

All devices must have active anti-malware or endpoint protection software installed and running.

Minimum requirements:

- Real-time protection enabled
- Automatic signature updates enabled
- Regular system scans configured

Examples of acceptable solutions include:

- Microsoft Defender
- Malwarebytes
- SentinelOne
- CrowdStrike
- Bitdefender
- Sophos Home

The company reserves the right to deny access to devices without adequate protection.

### Local Device Security

Devices must also:

- Use full-disk encryption where supported
  - BitLocker
  - FileVault
  - LUKS
- Require a password, PIN, or biometric authentication
- Automatically lock after a period of inactivity
- Not be shared with unauthorized individuals while connected to company systems

## Acceptable Use

Users agree to:

- Use company resources for authorized business purposes only
- Avoid downloading or storing unauthorized software related to company work
- Report suspected malware infections or security incidents immediately
- Disconnect compromised devices from company resources until remediated

Users must not:

- Disable security software
- Circumvent VPN or security controls
- Share company credentials
- Store sensitive company data on unencrypted removable media

## Monitoring and Privacy

The company respects employee privacy regarding personal devices. However:

- Network access logs may be collected for security and operational purposes
- Devices connected through Tailscale may be subject to access control policies
- The company will not intentionally access personal files unrelated to business operations

The company reserves the right to restrict or revoke access for devices deemed insecure or non-compliant.

## Incident Response

If a BYOD device is suspected of being compromised:

1. The user must immediately disconnect from company systems
2. The user must notify IT or management
3. Access may be temporarily suspended
4. The device must be remediated before reconnecting

## Compliance

Failure to comply with this policy may result in:

- Revocation of remote access privileges
- Disciplinary action
- Additional security review requirements

## Employee Acknowledgement

By accessing company systems using a personal device, users acknowledge that they:

- Have read and understood this BYOD Policy
- Agree to comply with all security requirements
- Understand that access may be revoked for non-compliance

## Policy Review

This policy may be updated periodically to address changes in technology, security requirements, or business operations.