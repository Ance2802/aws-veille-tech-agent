# 🤖 Agent de Veille Technologique Serverless (AWS & Gemini)

## 📝 Description du projet
Ce projet est un **Agent IA autonome et événementiel** déployé sur AWS. Il est conçu pour automatiser la veille technologique. Dès qu'un document texte est déposé dans un bucket Amazon S3, l'agent se déclenche automatiquement, analyse le contenu grâce à l'API Google Gemini, génère une synthèse structurée en 3 points clés, et sauvegarde le résultat dans un nouveau fichier sur S3.

## 🏗️ Architecture
L'architecture repose sur un modèle **Serverless** et **Event-Driven** (piloté par les événements) :

1. **Stockage (Amazon S3)** : Reçoit les fichiers bruts et stocke les synthèses générées.
2. **Événement (S3 Event Notification)** : Détecte le dépôt d'un nouveau fichier et réveille la fonction de calcul.
3. **Calcul (AWS Lambda)** : Fonction Python qui orchestre le processus (lecture, appel API, écriture).
4. **Intelligence Artificielle (Google Gemini API)** : Analyse le texte et génère la synthèse.
5. **Sécurité (AWS IAM)** : Gère les permissions pour que la Lambda puisse interagir avec S3.

## ⚙️ Fonctionnalités clés
- **Traitement dynamique** : L'agent lit le nom du fichier déclencheur grâce à l'événement S3 et nomme automatiquement le fichier de sortie (`synthese_NOM_DU_FICHIER.txt`).
- **Génération de contenu structuré** : Utilisation du modèle `gemini-2.5-flash` avec un prompt spécifique pour obtenir une synthèse claire et professionnelle.
- **Gestion des erreurs** : Le code inclut un bloc `try/except` pour gérer les erreurs de réseau, les timeouts ou les clés API invalides, retournant un statut HTTP approprié.

## 🚀 Comment ça marche (Le flux)
1. L'utilisateur téléverse un fichier (ex: `notes_reunion.txt`) dans le bucket S3.
2. AWS S3 envoie un signal à la fonction AWS Lambda.
3. La fonction Lambda lit le contenu du fichier et construit un prompt.
4. La Lambda fait une requête HTTP à l'API Gemini.
5. La réponse de l'IA est écrite dans un nouveau fichier (ex: `synthese_notes_reunion.txt`) dans le même bucket S3.

## 🛠️ Stack Technique
- **Cloud** : AWS (Lambda, S3, IAM)
- **Langage** : Python 3.14 (boto3, urllib)
- **Intelligence Artificielle** : Google Gemini API

## 🧠 Compétences démontrées
Ce projet valide les compétences suivantes :
- Conception d'architectures Serverless sur AWS.
- Gestion des permissions IAM.
- Intégration d'API REST d'IA générative dans un environnement Cloud.
- Automatisation de workflows (Event-Driven).
- Gestion des erreurs dans un environnement distribué (timeouts, gestion des clés API).

---
*Projet réalisé par Ance YOUBI dans le cadre de ma formation en Architecture Cloud et Agents IA.*
