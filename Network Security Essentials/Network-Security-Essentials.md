# Network Incident — Writeup (Concise Answers)

## Part 1 — Logs (Firewall / WAF / VPN)

- **Examine the firewall logs. Which IP address is performing the port scan?**  
  **Answer:** `203.0.113.10`

- **In the WAF Logs, which single source IP is responsible for all the blocked web attacks?**  
  **Answer:** `198.51.100.12`

- **In the VPN logs, how many brute-force attempts failed?**  
  **Answer:** `90`

- **Which suspicious IP address was found attempting the brute-force attack against the VPN gateway?**  
  **Answer:** `45.137.22.13`

---

## Part 2 — Investigation via SIEM (Splunk)

- **Examine the firewall logs. What external IP performed the most reconnaissance?**  
  **Answer:** `203.0.113.45`

- **In the firewall log, Which internal host was targeted by scans?**  
  **Answer:** `10.0.0.20`

- **Which username was targeted in VPN logs?**  
  **Answer:** `svc_backup`

- **What internal IP was assigned after successful VPN login?**  
  **Answer:** `10.8.0.23`

- **Which port was used for lateral SMB attempts?**  
  **Answer:** `445`

- **In the IDS logs, which host beaconed to the C2?**  
  **Answer:** `10.0.0.60`

- **During the investigation, which IP was observed to be associated with C2?**  
  **Answer:** `198.51.100.77`

- **Which host showed the exfiltration attempts?**  
  **Answer:** `10.0.0.51`
