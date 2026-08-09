# Titan Monitor

**Hardware monitoring for Windows**  
Version **1.0.0**

Titan Monitor affiche en temps réel les températures et l’utilisation du CPU, du GPU et de la mémoire à partir de LibreHardwareMonitor. Il comprend un tableau de bord cyberpunk, un historique interactif, un overlay, des alertes thermiques, des journaux CSV et un diagnostic local.

## Fonctions principales

- Températures CPU, GPU, hotspot et VRAM selon les sondes disponibles
- Utilisation CPU, GPU et RAM
- Graphiques d’historique glissant
- Overlay noir opaque, déplaçable et à hauteur dynamique
- RPM CPU FAN et GPU FAN dans l’overlay quand les capteurs sont disponibles
- Icône System Tray et notifications thermiques
- Seuils configurables
- Export automatique en CSV
- Diagnostic instantané et score de santé indicatif

## Prérequis

- Windows 10 ou 11
- Python 3.11+ pour lancer les sources
- Droits administrateur pour accéder aux capteurs matériels

```cmd
python -m pip install -r requirements.txt
python main.py
```

Le pilote PawnIO est facultatif, mais recommandé pour certaines sondes de carte mère :

```cmd
winget install PawnIO
```

## Compilation Windows

Ouvre un terminal administrateur dans le dossier du projet puis lance :

```cmd
build.bat
```

L’exécutable sera produit dans le dossier `dist`.

## Données utilisateur

Les paramètres et journaux sont stockés dans :

```text
%LOCALAPPDATA%\Titan Monitor
```

## Avertissement

Les diagnostics sont indicatifs. Ils ne remplacent pas une vérification matérielle et n’affirment jamais avec certitude la cause d’une anomalie.

## Historique

Consulte [`CHANGELOG.md`](CHANGELOG.md).

## Stockage et tensions

Titan Monitor détecte automatiquement les disques physiques et les volumes locaux :

- type SSD/HDD/NVMe lorsque Windows le fournit ;
- état de santé et état opérationnel ;
- pourcentage de santé si le compteur d'usure est disponible ;
- capacité, espace utilisé et espace libre en Go ;
- température et heures de fonctionnement si disponibles.

La lecture de santé repose sur les API de stockage Windows. Elle n'égale pas systématiquement le niveau de détail de CrystalDiskInfo : certains contrôleurs ne transmettent pas tous les attributs SMART.

## Screenshots

<img width="516" height="619" alt="image" src="https://github.com/user-attachments/assets/8ebe7fd5-558b-4b0f-9cba-565243c6cc80" />
<img width="1883" height="1326" alt="image" src="https://github.com/user-attachments/assets/45520dbd-4147-4876-9775-9b3640473bc3" />
<img width="740" height="911" alt="image" src="https://github.com/user-attachments/assets/cd67f047-ecb9-4f15-b189-4ebbed18fcc8" />
<img width="1051" height="1095" alt="image" src="https://github.com/user-attachments/assets/3ada039c-33d2-4676-9a9f-63525f93e985" />



## Composants tiers

Titan Monitor utilise plusieurs composants open source tiers. Les notices de licence
et informations de redistribution sont regroupées dans [`THIRD-PARTY-LICENSES.txt`](THIRD-PARTY-LICENSES.txt).

## Easter Egg music

Easter Egg music: “Metalcore Music for Extreme Sports 20s” — Farran_Ez  
Used under the Pixabay Content License.
