# OWASP Broken Access Control — Writeup

## Task 1 — Introduction
In this room, we will examine application security (AppSec) and incident response (IR). More specifically, we will learn how shifts in threat landscapes, software architecture, and attacker behaviour have made AppSec IR, an intersection of these two practices, increasingly relevant and teach the basics of this hybrid function.

---

## Task 2 — Basics
- **What is IDOR?**  
  Insecure direct object reference ✅  

- **What occurs when an attacker can access resources or data belonging to other users with the same level of access?**  
  Horizontal privilege escalation ✅  

- **What occurs when an attacker can access resources or data from users with higher access levels?**  
  Vertical privilege escalation ✅  

- **What is ABAC?**  
  Attribute-Based Access Control ✅  

- **What is RBAC?**  
  Role-Based Access Control ✅  

---

## Task 3 — Deploying the Machine
*(Deployment step — no answer required)*

---

## Task 4 — Reconnaissance
- **What is the type of server that is hosting the web application?**  
  Apache ✅  

- **What is the name of the parameter in the JSON response from the login request that contains a redirect link?**  
  redirect_link ✅  

- **What Burp Suite module allows us to capture requests and responses between ourselves and our target?**  
  Proxy ✅  

- **What is the admin’s email that can be found in the online users’ table?**  
  admin@admin.com ✅  

---

## Task 5 — Exploitation
- **What kind of privilege escalation happened after accessing admin.php?**  
  Vertical ✅  

- **What parameter allows the attacker to access the admin page?**  
  isadmin ✅  

- **What is the flag in the admin page?**  
  THM{I_C4n_3xpl01t_B4c} ✅  

---

## Task 6 — Mitigations
Pour réduire les risques de **Broken Access Control**, il est recommandé de :  
- Mettre en place un contrôle d’accès basé sur les rôles (RBAC).  
- Utiliser des requêtes paramétrées pour éviter les injections SQL.  
- Gérer les sessions de façon sécurisée (cookies protégés, expiration).  
- Valider et assainir toutes les entrées utilisateur, et utiliser `password_hash`.  
- Appliquer le principe du moindre privilège et surveiller les accès non autorisés.  

---

## Conclusion
Broken Access Control est une vulnérabilité critique qui survient lorsque les contrôles d’accès ne sont pas correctement appliqués. Elle peut mener à une **escalade horizontale** (accès à des données d’autres utilisateurs du même niveau) ou à une **escalade verticale** (accès à des privilèges supérieurs, comme ceux d’un administrateur).  

Les impacts incluent le vol de données sensibles, la compromission de systèmes critiques, voire la prise de contrôle complète du réseau. Pour s’en protéger, il est essentiel de mettre en place des contrôles d’accès robustes, de surveiller les activités suspectes et d’appliquer les bonnes pratiques de développement sécurisé.  

**Références utiles pour les développeurs PHP :**  
- [OWASP PHP Configuration Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/PHP_Configuration_Cheat_Sheet.html)  
- [PHP The Right Way: Security](https://phptherightway.com/#security)  
- [Secure Coding in PHP](https://www.owasp.org/index.php/PHP_Security_Cheat_Sheet)  
