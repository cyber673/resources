# SahurCTF Writeups!

## Shadow Asset Discovery

#### Description

DevBytes has a small office network, but someone may have connected an unauthorized device. You need to find it!

Go to https://guac.cyber673.com/guacamole and login using:
Username: shadow_it
Password: io72YhkwTFTeVfITgJfl

Then select chall1 to login to the server.

Flag format: btctf{ip_address_of_rouge_device}

#### File(s)

None (accessed through Guacamole)

#### Solution

Run nmap to scan the network for devices.

```bash
nmap -sn 192.168.10.0/24
```

You will find the unauthorized device at 192.168.10.99.

#### Flag

btctf{192.168.10.99}

***

## Access Control Analysis

#### Description

Review the "Access_Matrix.csv" file containing user permissions across various systems. Based on the principles of least privilege, identify all users who have excessive permissions that violate our security policy.

Access matrix and security policy can be found attached.

Flag format: btctf{user1_user2_user3}

#### File(s)

- Access_Matrix.csv
- Security_Policy.txt

#### Solution

Review the access matrix and security policy to identify users with excessive permissions.

#### Flag

btctf{amir_superuser_contractor}

***

## Suspicious Login Detection

#### Description

DevBytes security monitoring has flagged some suspicious login attempts. Analyze the logs to determine the nature of the attack.

Download and analyze the authentication log file. Identify:

- What type of attack is occurring?
- Which IP address is the primary attacker?
- Which valid username was eventually compromised?

Flag format: btctf{attack-name_ip-address_valid-user}

#### File(s)

- auth.log 

#### Solution

When checking the logs, you will see that there are multiple failed login attempts from the same IP address. The attacker is bruteforcing the password for the several users and succeeded with the user "nurul".

#### Flag

btctf{bruteForce_185.142.236.43_nurul}

***

## Malware Identification

#### Description

A developer at DevBytes downloaded several utilities, but security monitoring flagged one as potentially malicious.

One of these utility files is malicious. Without executing them, determine which file contains malware.

#### File(s)

- check_files.zip (containing multiple files)

#### Solution

1. Analyze the files in the zip archive to identify the malicious one. 
2. You can use a tool like VirusTotal to scan the files for malware. 
3. The file "system_optimizer.exe" is flagged as malicious. 
4. It's a false positive, but for the purpose of this challenge, it's considered malware.

#### Flag

btctf{system_optimizer.exe}

***

## Vulnerability Assessment

#### Description

DevBytes has run a security scan on their web application. Analyze the results to prioritize security fixes.

Review the file containing security scan results. Based on DevBytes' risk tolerance statement from the workshop:

1. Identify and provide the vuln ID with the highest CVSS score
2. Determine which server has the most critical security issues
3. Identify the oldest unpatched vulnerability (by CVE year)

Flag format: btctf{VLN-XXX_affected-server_CVE-XXXX-XXXX}

#### File(s)

- vuln_scan.json

#### Solution

1. Review the scan results to identify the vulnerability with the highest CVSS score.
2. Identify the server with the most critical security issues.
3. Find the oldest unpatched vulnerability.

#### Flag

btctf{VLN-001_backend-api-server_CVE-2018-12345}

***

## Incident Response Plan Analysis

#### Description

DevBytes has experienced an incident. Review the incident timeline and response actions to identify gaps.

Review the "incident_report.md" file containing details about a recent security incident.

1. Calculate the total time from detection to containment (in minutes)
2. Identify the attack vector used for initial compromise
3. Determine what data was potentially exposed

Flag format: btctf{XXmins_attack-vector_exposed-data}

#### File(s)

- incident_report.md

#### Solution

1. Calculate the time from detection to containment.
2. Identify the attack vector. In this case, it was a phishing email.
3. Determine the potentially exposed data. In this case, it was addresses.

#### Flag

btctf{78mins_phishing_addresses}

***

# The First Strike

#### Description

Identify the time of the first brute-force attempt.

Flag format: btctf{HH:MM:SS} no space for the am or pm

Note: use the files for the rest of the challenges

#### File(s)

- Security.evtx

#### Solution

1. Open security.evtx file using Event Viewer (Windows) or a log viewer tool.
2. Filter Event ID 4625
3. Sort by date and time
4. Look for workspacers user first attempt

#### Flag

btctf{2:07:09PM}

***

## Intruder's Footprint

#### Description

Find the attacker's IP address and source port

Flag format: btctf{IP:PORT}

#### File(s)

- Security.evtx

#### Solution

1. Open security.evtx file using Event Viewer (Windows) or a log viewer tool.
2. Filter Event ID 4625
3. Sort the date and time
4. Look for workspacers user first attempt
5. View the NetworkInformation

#### Flag

btctf{192.168.220.128:49014}

***

## The Stolen Document

#### Description

Identify the full path of the accessed file

Flag format: btctf{x/x/x/x/}

#### File(s)

- Security.evtx

#### Solution

1. Open security.evtx file using Event Viewer (Windows) or a log viewer tool.
2. Filter Event ID 4663
3. View the ObjectName
4. Copy the full path

#### Flag

btctf{C:\Users\workspaceRS\Documents\Finance\quarterfinanceamount.txt}

***

## The Rogue Command

#### Description

Find out what PowerShell command was executed

Flag format: btctf{flag}

#### File(s)

- Operational.evtx

#### Solution

1. Open operational.evtx file using Event Viewer (Windows) or a log viewer tool.
2. Filter Event ID 4104
3. Under general tab
4. Look for the powershell command at the first sentence

#### Flag

btctf{Invoke-WebRequest}

***

## The Hidden Payload

#### Description

Identify the name of the downloaded file.

Flag format: btctf{filename}

#### File(s)

- Operational.evtx

#### Solution

1. Open operational.evtx file using Event Viewer (Windows) or a log viewer tool.
2. Filter Event ID 4104
3. Under general tab
4. Look for the name of the outfile at the very last sentence

#### Flag

btctf{malware.exe}

***

## SIEM-1 : Critical File Modification

#### Description

- Access the SIEM: [cyber673 SIEM](https://siem.n0juan.com)
- Username: SOC
- Password: BlueTeam123*

A critical configuration file was modified on the server at Mar 14, 2025 @ 15:23:09.015. What is the name of this file?

*add rule.groups:syscheck_file as filter

Flag format: btctf{file_name}

#### File(s)

None (access through SIEM)

#### Solution

1. Access SIEM
2. Click Menu (Top Left)
3. Go to Threat Intelligence
4. Click Threat Hunting
5. Once in Threat Hunting Page, Go to Events tab
6. Adjust time appropriately (from 1 year ago to now)
7. Click add filter (Field: rule.groups; Operator: is; Value: syscheck_file)
8. Look for the correct timestamp (Mar 14, 2025 @ 15:23:09.015)
9. Click the "Inspect document details" icon which is on the left of the timestamp
10. Look for the file name either from the full_log or syscheck.path 

#### Flag

btctf{config_backup_2023.txt}

***

## SIEM-2: External Admin Login

#### Description

- Access the SIEM: [cyber673 SIEM](https://siem.n0juan.com)
- Username: SOC
- Password: BlueTeam123*

An administrator logged in from an external IP address at Mar 14 07:51:49 (predecoder.timestamp). What is the IP Address?

*add location:/var/log/auth_simulated.log as filter

Flag format: btctf{IP_Address}

#### File(s)

None (access through SIEM)

#### Solution

1. Access SIEM
2. Click Menu (Top Left)
3. Go to Threat Intelligence
4. Click Threat Hunting
5. Once in Threat Hunting Page, Go to Events tab
6. Adjust time appropriately (from 1 year ago to now)
7. Click add filter (Field: location; Operator: is; Value: /var/log/auth_simulated.log)
8. As this is not "timestamp", click the "626 available fields" and toggle on for "predecoder.timestamp"
9. Look for the correct predecoder.timestamp (Mar 14 07:51:49)
10. Click the "Inspect document details" icon which is on the left of the timestamp
11. Look for the ip from data.srcip

#### Flag

btctf{203.0.113.1}

***

## SIEM-3: Attacker Port Scan Source

#### Description

- Access the SIEM: [cyber673 SIEM](https://siem.n0juan.com)
- Username: SOC
- Password: BlueTeam123*

An attacker performed a port scan on the server. What is the IP address of the attacker?

*add location:/var/log/eve_simulated.log as filter

Flag format: btctf{IP_Address}

#### File(s)

None (access through SIEM)

#### Solution

1. Access SIEM
2. Click Menu (Top Left)
3. Go to Threat Intelligence
4. Click Threat Hunting
5. Once in Threat Hunting Page, Go to Events tab
6. Adjust time appropriately (from 1 year ago to now)
7. Click add filter (Field: location; Operator: is; Value: /var/log/eve_simulated.log)
8. Look for for word "Suricata: Alert - Nmap TCP Scan" in rule.description field
9. Click the "Inspect document details" icon which is on the left of the timestamp
10. Look for the ip from data.src_ip

#### Flag

btctf{10.10.10.10}
