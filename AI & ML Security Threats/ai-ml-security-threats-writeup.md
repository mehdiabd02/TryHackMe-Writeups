# TryHackMe — AI/ML Security Threats Writeup

## Task 1 — Introduction
This room focuses on understanding AI/ML concepts, their security implications, and how attackers can exploit these technologies. The goal is to explore AI cyber threats, defenses, and practical use cases.

---

## Task 2 — Machine Learning Basics

### Question 1
**Question:** What category of machine learning combines both labelled and unlabelled data?  
**Answer:** semi-supervised learning

### Question 2
**Question:** What is the first layer in a neural network that handles incoming raw data?  
**Answer:** input layer

### Question 3
**Question:** Which learning method does not require human-labeled data and can extract features from raw, unstructured input?  
**Answer:** deep learning

### Question 4
**Question:** What are the weighted connections between nodes in a neural network meant to simulate in the human brain?  
**Answer:** synapses

---

## Task 3 — LLMs

### Question 1
**Question:** What type of AI model enabled major advancements in ChatGPT and similar tools?  
**Answer:** large language models

### Question 2
**Question:** What is the first training stage where an LLM processes massive amounts of data?  
**Answer:** pre-training

### Question 3
**Question:** What type of neural network introduced by Google in 2017 powers modern LLMs?  
**Answer:** transformer

---

## Task 4 — AI-Specific Threats

### Question 1
**Question:** What framework was developed by MITRE to guide the understanding of AI-specific cyber threats?  
**Answer:** ATLAS

### Question 2
**Question:** What type of attack involves cloning an AI model by interacting with its API?  
**Answer:** model theft

### Question 3
**Question:** What generative AI technique can replicate a person’s voice or appearance with high realism?  
**Answer:** deepfake

### Question 4
**Question:** What common social engineering attack has become harder to detect due to AI-generated fluent and convincing messages?  
**Answer:** phishing

---

## Task 5 — AI in Cybersecurity

### Question 1
**Question:** According to IBM, how many days faster does AI help identify and contain breaches?  
**Answer:** 108

### Question 2
**Question:** What cybersecurity task benefits from AI helping to imagine attacker behavior we might not consider?  
**Answer:** threat hunting

### Question 3
**Question:** Explainability tools such as SHAP and LIME help with what?  
**Answer:** model monitoring

---

## Task 6 — Practical

### Question 1
**Question:** What's the flag?  
**Answer:** thm{443/60/16384}  

**Method used:** I asked the prompt: *"what are these values: DoH port, SYN flood timeout and ephemeral port range size?"* and retrieved the values, which correspond to the flag.

---

## Conclusion

At the beginning of this room, it was noted that *"Knowledge is power"* and that this is especially true in the fight against AI cyber threats. The rate at which this technology has exploded onto the scene has left many feeling left in the dust. Now, with a better understanding of AI and the underlying technology which enables it to be the force it currently is in our (and all) industry, you understand what is posing a threat to our systems and what needs to be secured as a result.  

Here is a recap of what's been covered:

- **Artificial Intelligence (AI)** is the overarching field concerned with enabling machines/systems to mimic human behaviour.  
- **Machine learning (ML)** is a subfield of AI in which a model can be fed and trained on input and used to make predictions.  
- **Deep learning (DL)** is then a subfield of ML. It no longer needs human interaction and can self-teach and process massive amounts of data, possible through the use of **Neural Networks**.  
- **DL** has enabled the emergence of technologies like **LLMs** (and other generative AI), which, through the use of transformer neural networks and attention, can be queried in natural language, understand it, and respond in a human-like, conversational fashion.  
- **AI is a dangerous weapon** in the hands of an attacker. It has the potential to enhance existing cyber attacks like phishing and increase the attack surface by introducing AI vulnerabilities.  
- While being dangerous in the hands of attackers, **AI can also be invaluable in the fight against AI cyber threats** and should be adopted — but done so securely, ensuring vulnerabilities are not introduced.  

**Final Note:**  
This room provided the foundations of AI/ML concepts, their link to cybersecurity threats, and how defenders can leverage them responsibly. Knowledge gained here empowers you to better assess, detect, and counter AI-driven threats in real-world scenarios.
