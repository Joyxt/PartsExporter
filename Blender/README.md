
# Blender Add-on: Batch Coords & FBX Exporter

Un Add-on simple et efficace pour **Blender** qui automatise l'exportation de données de position et de fichiers modèles en masse. Idéal pour les pipelines de jeu vidéo ou l'intégration technique.

## 🚀 Fonctionnalités

  * **Interface Intégrée** : Accessible directement via le panneau latéral (N-Panel) dans la vue 3D.
  * **Log de Coordonnées (TXT)** : Génère un fichier texte listant le nom et la position X, Y, Z (Monde) de chaque objet.
  * **Tri Alphabétique** : Trie automatiquement la liste des objets par nom avant l'écriture.
  * **Précision** : Arrondi automatique des coordonnées à **3 décimales**.
  * **Batch Export FBX** : Exporte simultanément chaque objet sélectionné dans un fichier `.fbx` individuel.
  * **Explorateur de Fichiers** : Utilise la fenêtre native de sauvegarde de Blender pour choisir le dossier de destination.

## 📝 Format de sortie (TXT)

Le fichier généré (`.txt`) suit ce format strict :
`NomObjet / X.xxx Y.yyy Z.zzz`

**Exemple :**

```text
Asset_Arbre_01 / 12.500 4.200 0.000
Asset_Rocher_A / -5.100 10.000 1.500
Asset_Rocher_B / -2.000 10.000 0.000
```

## 📦 Installation

1.  Téléchargez le fichier `export_coords_fbx.py`.
2.  Ouvrez Blender.
3.  Allez dans **Edit** \> **Preferences** \> **Add-ons**.
4.  Cliquez sur le bouton **Install...** en haut à droite.
5.  Sélectionnez le fichier `.py` téléchargé.
6.  Cochez la case à côté de **Import-Export: Export Coords & FBX Batch** pour l'activer.

## 🛠 Utilisation

1.  Dans la vue 3D, appuyez sur **N** pour ouvrir le panneau latéral.
2.  Cliquez sur l'onglet vertical **Export Tools**.
3.  Sélectionnez les objets que vous souhaitez exporter dans la scène.
4.  Cliquez sur le bouton **Exporter Coords & FBX**.
5.  Une fenêtre s'ouvre : choisissez le nom du fichier texte et le dossier de destination.
6.  L'add-on génère le fichier texte et tous les FBX correspondants.

## ⚙️ Détails Techniques

  * **Compatibilité** : Blender 2.80 et supérieur (Testé sur 3.x/4.x).
  * **Système de coordonnées** : Utilise `object.matrix_world` pour garantir que les positions sont absolues dans la scène.
  * **Paramètres FBX** :
      * `Axis Forward`: -Z
      * `Axis Up`: Y
      * `Use Selection`: True

## 📄 Extrait du code (Core)

```python
# Exemple de la boucle principale
for obj in selected_objects:
    # Récupération position Monde
    loc = obj.matrix_world.translation
    # Écriture dans le fichier
    f.write(f"{obj.name} / {loc.x:.3f} {loc.y:.3f} {loc.z:.3f}\n")
    
    # Export FBX individuel
    bpy.ops.export_scene.fbx(filepath=fbx_path, use_selection=True, ...)
```

## 👤 JOYxt

Add-on développé pour simplifier l'export de layout vers VimontFramework
