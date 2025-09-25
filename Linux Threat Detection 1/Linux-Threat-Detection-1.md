# TryHackMe — Initial Access on Linux — Writeup

## Task 1 — Introduction (mini résumé)
Avec l'essor de l'IA, du cloud et de l'IoT, les systèmes Linux sont de plus en plus exposés. Pourtant, la plupart des compromissions Linux commencent par des techniques d'accès initial bien connues (SSH brute force, exploitation de services exposés, compromise de la chaîne d'approvisionnement, etc.). Cette room vise à montrer comment détecter ces techniques en s'appuyant sur les sources de logs étudiées dans la room *Linux Logging for SOC*, utiliser l'analyse d'arbre de processus pour retracer l'origine d'une attaque et s'exercer sur des scénarios réalistes.

**Objectifs d'apprentissage**
- Comprendre le rôle et le risque de SSH dans les environnements Linux  
- Identifier comment des services exposés mènent à des compromissions  
- Utiliser l'analyse d'arbre de processus pour trouver l'origine de l'attaque  
- Pratiquer la détection d'Initial Access via des labs réalistes

---

## Task 2 — Lab Access

- **Q : When did the ubuntu user log in via SSH for the first time?**  
  **Réponse :** `2024-10-22`  
  *Méthode courte :* inspection des logs SSH (ex : `auth.log` / logs SIEM) pour trouver le premier `sshd` accept login pour user `ubuntu`.

- **Q : Did the ubuntu user use SSH keys instead of a password for the above found date? (Yea/Nay)**  
  **Réponse :** `Yea`  
  *Méthode courte :* vérification des lignes `Accepted publickey for ubuntu` vs `Accepted password for ubuntu` dans les logs.

---

## Task 3 — SSH Brute Force

- **Q : When did the SSH password brute force start?**  
  **Réponse :** `2025-08-21`  
  *Méthode courte :* repérer le début d’une série de tentatives `Failed password` dans les logs (`auth.log` / SIEM`) et prendre la première date.

- **Q : Which four users did the botnet attempt to breach?**  
  **Réponse :** `root, roy, sol, user`  
  *Méthode courte :* extraire la liste des usernames ciblés par les événements `Failed password` et trier alphabétiquement.

- **Q : Finally, which IP managed to breach the root user?**  
  **Réponse :** `91.224.92.79`  
  *Méthode courte :* trouver la première occurrence `Accepted password for root` ou similaire et lire l’IP source associée.

---

## Task 4 — File access

- **Q : What is the path to the Python file the attacker attempted to open?**  
  **Réponse :** `/opt/trypingme/main.py`  
  *Méthode courte :* analyser logs d’accès fichiers / processus (auditd, proc accounting) ou les commandes enregistrées dans l’arbre de processus.

- **Q : Looking inside the opened file, what's the flag you see there?**  
  **Réponse :** `THM{i_am_vulnerable!}`  
  *Méthode courte :* récupérer le contenu du fichier (via l’image disque, ou logs montrant `cat`/`less`/`python` invocation) et lire la chaîne flag.

---

## Task 5 — Process tree analysis

- **Q : What is the PPID of the suspicious whoami command?**  
  **Réponse :** `1018`  
  *Méthode courte :* repérer le processus `whoami` dans l’arbre de processus et lire son PPID.

- **Q : Moving up the tree, what is the PID of the TryPingMe app?**  
  **Réponse :** `577`  
  *Méthode courte :* remonter l’arbre parent → parent jusqu’à trouver le PID du processus applicatif `TryPingMe`.

- **Q : Which program did the attacker use to open a reverse shell?**  
  **Réponse :** `Python`  
  *Méthode courte :* analyser la commande lancée (ex : `python -c '...socket...'`) ou vérifier les arguments du processus de reverse shell.

---

## Task 6 — Detections & Mitigations

- **Q : Which Initial Access technique is likely used if a trusted app suddenly runs malicious commands?**  
  **Réponse :** `Supply Chain Compromise`  
  *Méthode courte :* contexte d’un binaire/trusted app qui exécute actions malveillantes → suspecter compromission via chaîne d’approvisionnement ou mise à jour corrompue.

- **Q : Which detection method can you use to detect a variety of Initial Access techniques?**  
  **Réponse :** `Process Tree Analysis`  
  *Méthode courte :* utiliser l’analyse d’arbre de processus pour relier commandes suspectes à processus parents, repérer persistance, exécution inhabituelle et pivots.

---

## Conclusion rapide
Ce lab montre l'importance de corréler logs SSH, logs système et arbre de processus pour détecter l'accès initial : détection précoce (brute force), vérification des méthodes d'authentification (clé vs mot de passe), enquête sur les processus suspects, et identification de patterns d'Initial Access comme Supply Chain Compromise. L'analyse d'arbre de processus est un outil central pour tracer l'origine des commandes malveillantes et construire une réponse IR appropriée.

