# TryHackMe — Mnemonic — Writeup

## TL;DR
Lab Mnemonic — découverte de services, accès via FTP/SSH, récupération d’un fichier secret (`backups.zip`) puis escalade vers root. Flags trouvés : `user.txt` et `root.txt`.

---

## Task 1 — Découverte & fichiers
- **How many open ports?**  
  **Answer:** `3`

- **What is the SSH port number?**  
  **Answer:** `1337`

- **What is the name of the secret file?**  
  **Answer:** `backups.zip`

**Méthode courte :** scan rapide (`nmap -sC -sV -p-`) → identifier ports ouverts, se connecter au FTP anonyme/authentifié, repérer le fichier `backups.zip` sur le serveur.

---

## Task 2 — Accès initial (FTP / SSH / mots de passe)
- **FTP user name?**  
  **Answer:** `ftpuser`

- **FTP password?**  
  **Answer:** `love4ever`

- **What is the SSH username?**  
  **Answer:** `james`

- **What is the SSH password?**  
  **Answer:** `bluelove`

- **What is the condor password?**  
  **Answer:** `pasificbell1981`

**Méthode courte :** connexion FTP avec les creds fournies, téléchargement de `backups.zip` → extraction (mot de passe `pasificbell1981` trouvé dans le backup ou via énumération) → récupérer creds pour SSH (`james:bluelove`) et se connecter sur le port `1337`.

Commandes fréquemment utilisées :
```bash
nmap -sC -sV -p- TARGET
ftp TARGET
# login ftpuser:love4ever
get backups.zip
unzip backups.zip          # ou use password: pasificbell1981
ssh -p 1337 james@TARGET



Task 3 — Flags

user.txt
Answer: THM{a5f82a00e2feee3465249b855be71c01}

root.txt
Answer: THM{2a4825f50b0c16636984b448669b0586}
