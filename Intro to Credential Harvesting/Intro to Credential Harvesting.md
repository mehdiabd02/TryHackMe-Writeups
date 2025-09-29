# TryHackMe — Intro to Credential Harvesting — Writeup

## Task 1 — Credential extraction with Mimikatz

**Contexte / Méthode courte :**  
Avec un accès local à une machine Windows, nous avons extrait des identifiants en mémoire (LSASS) en utilisant Mimikatz pour récupérer mots de passe en clair présents dans les sessions actives.

**Questions & Réponses**

- **Q : What is Elon Tusk's Gmail password?**  
  **Answer :** `MyTusksAreThaB3st`

- **Q : What is svc-app's password?**  
  **Answer :** `S3rv!c3Acc!`

---

## Task 2 — Credential harvesting with Secretsdump

**Contexte / Méthode courte :**  
En utilisant des credentials locaux ou des accès récupérés, nous avons utilisé `secretsdump.py` (impacket) pour extraire les hives de registre (SAM, SYSTEM, SECURITY) et livrer NTLM hashes ainsi que d'autres secrets du domaine.

**Questions & Réponses**

- **Q : What is drgonzo's password?**  
  **Answer :** `lasvegas1`

- **Q : What is the domain Administrators NTLM hash?**  
  **Answer :** `d71ee9fb6a3f54496bdc6c941f7a2903`

- **Q : What is the flag located on the domain admin's Desktop?**  
  **Answer :** `THM{gotta_l0ve_cr3dential_st0res}`

---

## Conclusion 

Dans cette room, nous avons appris à localiser et extraire des identifiants dans différents composants d’un environnement Windows/Active Directory. De la mémoire (LSASS) aux hives du registre (SAM, SYSTEM, SECURITY) en passant par les secrets mis en cache, les identifiants sont souvent accessibles si l’on a les droits appropriés. Nous avons commencé par un accès administrateur local et utilisé des outils comme **Mimikatz** et **secretsdump.py** pour récupérer mots de passe, hashes et tokens, puis exploiter ces éléments pour atteindre des privilèges de domaine (domain admin).

---

**Remarque éthique :** ces techniques sont présentées ici à but éducatif et pour la défense (détection, durcissement, réponse). Ne les utilisez jamais sur des systèmes sans autorisation explicite.
