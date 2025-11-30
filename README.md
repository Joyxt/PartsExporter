# PartsExporter
This MaxScript script for 3ds Max automates data extraction and the export of 3D models. It generates a text file containing the coordinates of the selected objects and simultaneously exports each object as an individual .fbx file.


Voici une proposition de fichier `README.md` (format standard pour GitHub) prêt à être copié-collé.

J'ai structuré le document pour qu'il soit clair, professionnel et qu'il explique bien les prérequis (comme le réglage de l'export FBX).

-----

# 3ds Max Batch Exporter: Coords & FBX

Ce script MaxScript pour **3ds Max** permet d'automatiser l'extraction de données et l'export de modèles 3D. Il génère un fichier texte contenant les coordonnées des objets sélectionnés et exporte simultanément chaque objet en fichier `.fbx` individuel.

## 🚀 Fonctionnalités

1.  **Tri Alphabétique** : Trie automatiquement les objets sélectionnés par nom (ex: `Mirror_00`, `Mirror_01`) avant le traitement.
2.  **Génération de Log (TXT)** : Crée un fichier texte unique répertoriant :
      * Le nom de l'objet.
      * Ses coordonnées (X, Y, Z) en position Monde (World).
      * Formatage précis : Arrondi à **3 décimales**.
3.  **Batch Export FBX** : Exporte chaque objet sélectionné dans un fichier `.fbx` séparé, situé dans le même dossier que le fichier texte.

## 📝 Format de sortie (TXT)

Le fichier texte généré utilise le format suivant :
`NomObjet / X.xxx Y.yyy Z.zzz`

**Exemple :**

```text
Mirror_Eclat_00 / 10.500 0.000 25.125
Mirror_Eclat_01 / 12.100 1.555 25.125
Mirror_Eclat_02 / 15.000 2.000 30.000
```

## 🛠 Installation et Utilisation

### Prérequis

  * **Version** : Testé sur 3ds Max 2021 (compatible avec la plupart des versions récentes).
  * **Configuration FBX** : Le script utilise les **derniers paramètres d'export FBX** utilisés manuellement dans 3ds Max.
      * *Conseil : Faites un export manuel "à blanc" une fois pour configurer vos options (Y-up/Z-up, Embed Media, etc.) avant de lancer le script.*

### Comment l'utiliser

1.  Ouvrez 3ds Max.
2.  Allez dans `Scripting` \> `Run Script...` (ou glissez-déposez le script dans la fenêtre).
3.  Sélectionnez les objets que vous souhaitez exporter dans votre scène.
4.  Exécutez le script.
5.  Une fenêtre de dialogue s'ouvre : choisissez le dossier de destination et le nom du fichier texte.
6.  Le script génère le fichier texte et tous les FBX, puis ouvre automatiquement le dossier de destination.

## 📄 Code Snippet (Core Logic)

```maxscript
-- Extrait de la logique de tri et d'écriture
qsort objsToSort compareNames
for obj in objsToSort do (
    format "% / % % %\n" obj.name sx sy sz to:theFile
    exportFile (exportDir + obj.name + ".fbx") #noPrompt selectedOnly:true using:FBXEXP
)
```

## 👤 Skalito

Script créé pour automatiser le pipeline d'export vers VimontFramework

-----

**Note :** N'oubliez pas de sauvegarder votre scène avant de lancer des opérations de batch export par sécurité.
