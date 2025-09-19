# 📝 Writeup – TryHackMe: Detecting Web DDoS

## Task 1 – Introduction
Les attaques **DoS/DDoS** visent à perturber ou bloquer l’accès à un site ou service.  
Dans cette room, on apprend à :  
- Comprendre le fonctionnement des attaques DoS/DDoS.  
- Identifier leurs motivations.  
- Détecter leurs traces dans les logs.  
- Utiliser un SIEM (Splunk) pour analyser les attaques.  
- Découvrir des méthodes de défense comme **CDN** et **WAF**.  

✅ Objectif : être capable de détecter et mitiger ces menaces.

---

## Task 2 – DoS and DDoS Attacks
- Classe d’attaque visant la disponibilité → **Denial-of-Service**  
- Réseau de machines zombies utilisé pour lancer un DDoS → **Botnet**  

✅ Réponses :  
- **Denial-of-Service**  
- **Botnet**

---

## Task 3 – Attack Motives
Les motivations derrière les attaques :  
- **Reputational Damage** → faire perdre confiance aux clients.  
- **Hacktivism** → attaque motivée par des raisons idéologiques ou politiques.  

✅ Réponses :  
- **Reputational Damage**  
- **Hacktivism** (exemple : attaque DDoS de 2023 contre Microsoft)

---

## Task 4 – Log Analysis
À travers l’analyse des logs, on identifie :  
- L’IP attaquante : **203.12.23.195**  
- La page ciblée : **/login**  
- Les utilisateurs légitimes reçoivent un code : **503**  

✅ Réponses :  
- **203.12.23.195**  
- **/login**  
- **503**

---

## Task 5 – Leveraging SIEMs
Avec Splunk, on peut visualiser et investiguer :  
- URI le plus ciblé : **/search**  
- Première requête vers la cible par : **203.0.113.12**  
- Nombre d’IP du botnet : **60**  
- User-Agent des attaquants : **Java/1.8.0_181**  
- Pic de requêtes par seconde : **207**  
- Première IP légitime à recevoir un **503** : **10.10.0.27**  

✅ Réponses :  
- **/search**  
- **203.0.113.12**  
- **60**  
- **Java/1.8.0_181**  
- **207**  
- **10.10.0.27**

---

## Task 6 – Defense
Les défenses contre DoS/DDoS se répartissent en plusieurs niveaux :  

### Application Level
- Validation des entrées pour éviter abus.  
- **CAPTCHA / JS challenges** pour filtrer les bots.  

### Network & Infrastructure
- **CDN** → mise en cache, load-balancing, absorption du trafic.  
- **WAF** → filtrage et blocage basé sur règles, ex. **rate limiting**.  

### Large-scale mitigation
- Exemples : Google et Cloudflare absorbant des attaques massives.  

⚠️ Techniques de contournement : paramètres aléatoires dans les URLs, user-agents falsifiés, géo-distribution des requêtes.  

✅ Réponses :  
- Challenge bloquant les bots → **CAPTCHA**  
- Fonction du CDN qui répartit le trafic → **Load-balancing**

---

## Task 7 – Conclusion
Dans cette room, tu as appris :  
- Les différents types d’attaques **DoS/DDoS** et leurs motivations.  
- Comment analyser des logs web pour y détecter des attaques.  
- L’usage d’un **SIEM (Splunk)** pour investiguer des attaques à grande échelle.  
- Des méthodes de défense modernes comme **CDN** et **WAF**.  

👉 Leçons clés :  
- Les logs sont essentiels pour identifier les patterns anormaux.  
- Les SIEM permettent de gérer et corréler de gros volumes de données.  
- La défense repose sur une combinaison de bonnes pratiques (app, réseau, CDN, WAF).  

✅ **Writeup terminé**
