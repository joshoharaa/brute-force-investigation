# Brute-Force Investigation 

## Executive Summary 
On **11 March 2026**, Microsoft Defender detected multiple **brute-force authentication attempts** targeting several user accounts on the host **mts-contractorpc1**. This activity indicates a likely attempt to gain **unauthorised access** through credential compromise. 

The attack originated from two external IP addresses, **94.26.68.20 (Poland)** and **84.8.107.159 (Saudi Arabia)**, and generated **782 failed authentication attempts** across multiple common account names. 

The attacker successfully authenticated to the **administrator** account **three times** during the attack window; however, the investigation found **no evidence of post-authentication malicious activity**. The activity aligns with **MITRE ATT&CK** - **T1110 (Brute Force)**. Containment and remediation recommendations were provided to reduce the likelihood of further authentication-based attacks. 
--- 
## Findings

### Time
- **TimeCollected_UTC_s:** 11 March 2026, 11:01:15 - 15:00:25

### Incident
- Multiple **brute-force authentication attempts** were made against user accounts on this device. This activity may indicate an attempt to gain **unauthorised access** through credential compromise.

### Affected Accounts 
- administrator

### Affected Host
- mts-contractorpc1

### Source IP Addresses
- 94.26.68.20
- 84.8.107.159

### Successful Logons 
- **administrator**
  -  11 March 2026 - 11:01
  -  11 March 2026 - 15:00
  -  11 March 2026 - 15:00
  -  11 March 2026 - 15:00

## Investigation Summary

Between 11:04 and 15:00 on 11 March 2026, several failed authentication attempts were detected, totalling 782 and three successful logons. The targeted account with successful logons was "administrator" on the host of mts-contractorpc1. No post-authentication malicious behaviour was identified during the investigation. 

## Timeline of Events

| Time | Event |
| --- | --- |
| 11:01 | First successful authentication to administrator account |
| 11:04 | Large volume of failed login attempts begins |
| 15:00 | Additional successful authentication events |
| 15:00 | Investigation initiated |

## Incident Overview 

### WHO: 

Users/Accounts involved: 

**Successful**
- administrator

**Unsuccessful**
- ADMIN
- USER
- PC
- HP
- SQL
- FTP

### WHAT:
An automated brute-force authentication attack targeting multiple user accounts was observed. 

### WHEN: 

11 March 2026: 11:01:15 - 15:00:25 

### WHERE: 

Host/System affected: mts-contractorpc1

### WHY: 

The activity demonstrates characteristics consistent with a brute-force attack specifically targeting privileged accounts. No evidence of post-authentication compromise was identified during the investigation. 

### HOW: 

The high volume of login attempts (782 failed attempts) indicates an automated brute-force attack, likely performed using a scripted authentication tool. 

Mapped MITRE ATT&CK Technique: Brute Force - T1110

## Verdict 

The alert corresponds to a brute-force authentication attack targeting privileged accounts on host mts-contractorpc1. 

The attacker successfully authenticated to the administrator account three times during the attack window. 

Post-authentication investigation found no evidence of malicious activity such as process execution, persistence mechanisms, or lateral movement. 

The incident is therefore classified as confirmed credential compromise with limited successful authentication with no confirmed system compromise. 

## Indicators of Compromise (IOCs) 

## Source IP Addresses 

- 94.26.68.20 - Associated with repeated authentication attacks
- 84.8.107.159 - Observed targeting multiple accounts during attack window

## Targeted Accounts 

- administrator
- ADMIN
- USER
- PC
- HP
- SQL
- FTP

## Recommendations 

- Immediately reset the password for the affected administrator account.
- Revoke all active session and authentication tokens for the account.
- Implement multi-factor authentication (MFA) for all privileged accounts.
- Configure account lockout policies to mitigate brute-force authentication attempts.
- Restrict administrative logins to trusted network locations.
- Monitor authentication logs for continued attempts from identified IP addresses.
- Block the identified malicious IP addresses at the firewall or conditional access policies.

## Supporting Evidence

The following evidence demonstrate the step-by-step investigation process conducted using Microsoft Defender Advanced Hunting.

### Detection and Initial Alert 

<img width="1917" height="991" alt="Screenshot 2026-03-11 at 19 43 59" src="https://github.com/user-attachments/assets/a87d1d45-5bd3-44c0-a494-cf1c03601f19" />

**Figure 1:** Microsoft Defender alert indicating suspicious authentication activity associated with potential brute-force login attempts against the host mts-contractorpc1. 

### Initial Investigation and Data Collection 

<img width="1920" height="1005" alt="Screenshot 2026-03-11 at 22 00 44" src="https://github.com/user-attachments/assets/94b63e1a-84be-4031-9738-5870f80e7971" />

**Figure 2:** Initial Advanced Hunting query executed to identify relevant authentication events and determine appropriate data fields for further investigation. 

<img width="1920" height="994" alt="Screenshot 2026-03-11 at 22 09 59" src="https://github.com/user-attachments/assets/420632fc-66b8-4d23-a714-bf6cba1a4659" />

### Authentication Failure Analysis

**Figure 3:** Query results displaying failed authentication attempts associated with the affected account, confirming a high volume of authentication failures during the attack timeframe. 

<img width="1920" height="994" alt="Screenshot 2026-03-11 at 22 09 59" src="https://github.com/user-attachments/assets/4c5d527b-ec2a-47b3-8b8a-1f86066494fb" />

### Attack Scope and Correlation

**Figure 4:** Aggregated query showing the number of failed authentication attempts per source IP address targeting the administrator account, helping to identify the primary origin of the attack. 

### Successful Authentication Analysis 

<img width="1919" height="994" alt="Screenshot 2026-03-11 at 22 22 06" src="https://github.com/user-attachments/assets/bbf608bb-aece-41d8-8603-d7794f732da0" />

**Figure 5:** Following analysis of failed authentication attempts within the SecurityEvent table, an additional query was executed to identify a more suitable Defender data source for investigating successful logons and potential post-authentication activity. 

<img width="1919" height="994" alt="Screenshot 2026-03-12 at 19 13 13" src="https://github.com/user-attachments/assets/fd85567b-708f-4786-a5c3-e2f009f5b8c0" />

**Figure 6:** Query results showing successful authentication events for the affected administrator account, including associated source IP addresses and timestamps. 


### Affected User Scope 

<img width="1640" height="943" alt="Screenshot 2026-03-12 at 20 53 37 (1)" src="https://github.com/user-attachments/assets/908feb23-cc71-4c4d-ae6f-4c9939292c9c" />

**Figure 7:** Aggregated query displaying failed authentication attempts across multiple accounts from the same source IP, confirming a brute-force authentication attack targeting multiple usernames. 

<img width="1641" height="944" alt="Screenshot 2026-03-12 at 20 55 10" src="https://github.com/user-attachments/assets/e0cea696-960b-493a-890c-ed860c5bb7d4" />

**Figure 8:** Query results summarising successful authentication events by account, confirming that only the administrator account experienced successful logins during the investigation window. 

### Post-Authentication Activity Analysis 

<img width="1919" height="994" alt="Screenshot 2026-03-12 at 19 13 13" src="https://github.com/user-attachments/assets/8f3959aa-d871-4268-a784-cd1321cfb912" />

**Figure 9:** Process activity query showing no suspicious executable activity following successful authentication, indicating no immediate post-compromise behaviour occurred. 

### Threat Intelligence Enrichment

<img width="1944" height="1108" alt="Screenshot 2026-03-12 at 20 58 03" src="https://github.com/user-attachments/assets/43cfc952-b7a7-4d55-b7d4-733a8e2e194c" />

<img width="1920" height="1080" alt="Screenshot 2026-03-12 at 20 59 55" src="https://github.com/user-attachments/assets/22bbd8d5-7344-4007-93d1-e10f6ab5b390" />

**Figure 10:** OSINT lookup for the first source IP address used in the attack, providing additional threat intelligence context for the external host. 

<img width="1920" height="1080" alt="Screenshot 2026-03-12 at 20 59 18" src="https://github.com/user-attachments/assets/09fa0d82-eb72-44a0-925a-8a982e775840" />

**Figure 11:** OSINT intelligence results for the second source IP address identified in the brute-force authentication attempts. 

<img width="1944" height="1108" alt="Screenshot 2026-03-12 at 21 01 53" src="https://github.com/user-attachments/assets/c34e194c-5d30-4f34-abad-e930b4effdf1" />

**Figure 12:** Threat intelligence lookup for the first observed execution file hash to determine whether the file is associated with known malicious activity. 

<img width="1920" height="1080" alt="Screenshot 2026-03-12 at 21 02 46" src="https://github.com/user-attachments/assets/c165fa24-d216-49f9-a057-6676104b421f" />

**Figure 13:** Threat intelligence lookup results for the second execution hash to verify whether the file has known malicious associations. 

<img width="1920" height="1080" alt="Screenshot 2026-03-12 at 21 02 46" src="https://github.com/user-attachments/assets/f277c8e3-cf35-493d-ba6d-b81dde4074e3" />

**Figure 14:** Threat intelligence lookup results for the third observed execution hash used to validate whether the file is benign or associated with malicious activity. 

### Geolocation Analysis

<img width="1632" height="993" alt="Screenshot 2026-03-13 at 18 48 21" src="https://github.com/user-attachments/assets/7f0b78a7-d3e1-4dba-8699-7b235374713c" />

**Figure 15:** Geolocation of IP address 94.26.68.20 (Poland). 

<img width="1627" height="994" alt="Screenshot 2026-03-13 at 18 49 10" src="https://github.com/user-attachments/assets/f48d056b-2c5b-40fa-a50d-daf571f560ad" />

**Figure 16:** Geolocation of IP address 84.8.107.159 (Saudi Arabia). 


