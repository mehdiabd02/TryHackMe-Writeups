# TryHackMe — Invite Only Writeup

## Question 1
**Question:**  
What is the name of the file identified with the flagged SHA256 hash?

**Method used:**  
- I uploaded the SHA256 hash to **TryDetecteThis 2.0** (similar to VirusTotal).  
- The tool returned the file name associated with the hash.

**Answer:**  
syshelpers.exe

---

## Question 2
**Question:**  
What is the file type associated with the flagged SHA256 hash?

**Method used:**  
- I used **TryDetecteThis 2.0** to check the SHA256 hash.  
- The tool returned the file type.

**Answer:**  
Win32 EXE

---

## Question 3
**Question:**  
What are the execution parents of the flagged hash? List the names chronologically, using a comma as a separator. Note down the hashes for later use.

**Method used:**  
- I navigated to the **Execution Parents** tab in **TryDetecteThis 2.0**.  
- Reviewed the scanned results and detections, noting the parent file names and hashes.

**Answer:**  
361GJX7J, installer.exe

---

## Question 4
**Question:**  
What is the name of the file being dropped? Note down the hash value for later use.

**Method used:**  
- I checked the **Dropped Files** tab in **TryDetecteThis 2.0**.  
- Reviewed the scanned results to identify the file name and noted the hash.

**Answer:**  
AClient.exe

---

## Question 5
**Question:**  
Research the second hash in question 3 and list the four malicious dropped files in the order they appear (from top to bottom), separated by commas.

**Method used:**  
- I used **TryDetecteThis 2.0** to search the **second hash from Question 3**.  
- Checked the **Dropped Files** tab for this hash and noted the four malicious files in order.

**Answer:**  
searchhost.exe, syshelpers.exe, nat.vbs, runsys.vbs

---

## Question 6
**Question:**  
Analyse the files related to the flagged IP. What is the malware family that links these files?

**Method used:**  
- Retrieved the flagged IP from previous steps.  
- Searched the related files on TryDetecteThis/VirusTotal.  
- Checked the AV detection names and classifications.  
- Multiple detections (Microsoft, Avast, Kaspersky) consistently tagged the files as **AsyncRAT**.

**Answer:**  
AsyncRAT

---

## Question 7
**Question:**  
What is the title of the original report where these flagged indicators are mentioned? Use Google to find the report.

**Method used:**  
- Used Google with IoCs (hashes, filenames, IP) + keywords such as “Discord invite malware report”.  
- Found a published analysis that matched the indicators.

**Answer:**  
From Trust to Threat: Hijacked Discord Invites Used for Multi-Stage Malware Delivery

---

## Question 8
**Question:**  
Which tool did the attackers use to steal cookies from the Google Chrome browser?

**Method used:**  
- Searched the original report (from Q7) for details about the theft of browser cookies and the tooling used by the adversary.

**Answer:**  
ChromeKatz

---

## Question 9
**Question:**  
Which phishing technique did the attackers use? Use the report to answer the question.

**Method used:**  
- Checked the original report for details on the phishing/social-engineering technique.  

**Answer:**  
ClickFix

---

## Question 10
**Question:**  
What is the name of the platform that was used to redirect a user to malicious servers?

**Method used:**  
- Reviewed the attack chain in the report.  
- Found that Discord was used as the redirection platform.

**Answer:**  
Discord

---

## Conclusion
In this room, I practiced analyzing malicious files and IoCs using TryDetecteThis and external research reports.  
Key takeaways:  
- Investigating execution parents and dropped files.  
- Identifying malware families through AV detections.  
- Linking IoCs to real-world threat intelligence reports.  
- Understanding attacker techniques such as phishing, cookie theft, and multi-stage delivery.
