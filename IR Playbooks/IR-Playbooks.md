# IR Playbooks — Quick Answers

- **What is the name of the process that initiated this communication?**  
  `taskhsvc.exe`

- **Is this process malicious, as per VirusTotal? (y/n)**  
  `n`

- **What is the name of the parent process of this process?**  
  `@WanaDecryptor@.exe`

- **This process's parent was launched by another process, which is a notorious ransomware. Which ransomware is that?**  
  `Wannacry`

- **Which playbook should be followed to respond to this incident?**  
  `malware playbook`

- **Is this incident an FP (False Positive) or a TP (True Positive)?**  
  `TP`

- **In case the incident is a TP, what will be the next step in the IR process?**  
  `Containment`
