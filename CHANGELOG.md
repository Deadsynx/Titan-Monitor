## 1.0.0 — Release

- Première version stable de Titan Monitor.
- Gel fonctionnel après validation de la branche 0.9.35.
- Nettoyage du README et des anciens numéros de version de release.
- Dépendances principales figées dans `requirements.txt`.
- Ajout de `THIRD-PARTY-LICENSES.txt`.
- Aucun changement fonctionnel apporté à l’overlay Black Box.

## 0.9.35 — Easter Egg

- Clic sur le skeleton guitariste dans « À propos » : lecture de l’easter egg metalcore.
- Un second clic arrête et remet le morceau au début.
- Musique embarquée dans le build PyInstaller.
- Crédit Pixabay ajouté au README.
- Overlay Black Box inchangé.

## 0.9.34 — Screenshot Cleanup

- Suppression de la fonction de capture d’écran intégrée et de son entrée dans le menu System Tray.
- Nettoyage du code et de la documentation associés.
- Overlay Black Box inchangé.

## 0.9.33 — RAM Labels

- Écran principal : `DIMM#1`, `DIMM#2`, etc. deviennent `RAM #1`, `RAM #2`, etc.
- Overlay Black Box inchangé.

## 0.9.31 — Black Box
- Overlay simplifié en fenêtre noire opaque à coins carrés.
- Suppression de la transparence WebView2 pour éviter les artefacts de contour.
- Suppression du cycle de recréation de l’overlay au démarrage.
- Conservation des capteurs, RPM, seuils et redimensionnement automatique.

# Titan Monitor v0.9.30 — Adaptive Fan Overlay

## Correctifs
- L'overlay adapte désormais automatiquement sa hauteur au nombre de lignes réellement affichées.
- Le ventilateur CPU est détecté explicitement quand son nom l'indique.
- Fallback pour les cartes mères qui exposent CPU_FAN sous un nom générique `Fan #1`.
- La détection GPU FAN existante est conservée sans modification fonctionnelle.
- La pompe reste optionnelle et n'est affichée que lorsqu'elle est réellement identifiable.

# Titan Monitor v0.9.1 — Fan Overlay Preview

- Nouvelle section Ventilateurs avec détection LibreHardwareMonitor.
- Affichage RPM en temps réel avec minimum, maximum, moyenne et historique cliquable.
- Les noms de ventilateurs incluent leur contrôleur matériel quand disponible.
- 0 RPM est accepté pour les ventilateurs semi-passifs.
- Lecture seule : aucun contrôle PWM dans cette version.
- La logique de sauvegarde stable de la v0.8.6 est conservée.

# Titan Monitor v0.8.6 — Hotplate Internal

- Correction ciblée du blocage visuel du bouton **Enregistrer** dans la fenêtre Paramètres.
- Le frontend n'attend plus la résolution de la Promise pywebview pour rendre la main à l'utilisateur.
- Le bouton n'est plus désactivé pendant la sauvegarde et n'utilise plus de curseur Windows `wait`.
- Le backend de sauvegarde asynchrone de la v0.8.5 est conservé inchangé, les logs utilisateur ayant confirmé qu'il valide et écrit correctement `settings.json`.

# Titan Monitor v0.8.5 — Hotplate Internal

- Nouveau pont de sauvegarde `save_settings_json` : les paramètres traversent pywebview sous forme de JSON simple.
- Validation immédiate en mémoire puis écriture atomique de `settings.json` dans un worker dédié : aucun accès disque dans le clic **Enregistrer**.
- Journalisation des étapes de sauvegarde pour diagnostiquer précisément un éventuel blocage.
- Seuils par défaut : CPU 75 °C, GPU Core 75 °C, GPU Hotspot 90 °C, VRAM/Junction 90 °C, marge d'avertissement 10 °C.
- Installateur Inno Setup : AppId fixe conservé, mise à niveau dans le même dossier, fermeture propre de l'ancienne instance et nettoyage des anciens noms d'exécutables. Les réglages dans `%LOCALAPPDATA%\Titan Monitor` sont conservés.
- Publisher affiché : **DeadSynx**.

# Titan Monitor v0.8.4 — Hotplate Internal

- Corrige le blocage prolongé du bouton **Enregistrer** : plus de `fsync` bloquant dans le chemin UI et mise à jour du démarrage Windows uniquement si nécessaire, en arrière-plan.
- Corrige les faux **CRITICAL** de l’overlay lorsque CPU/GPU sont simplement à forte charge.
- Les sondes thermiques inconnues restent affichables mais ne peuvent plus déclencher une fausse alerte.

# Changelog

## 0.8.4 — Hotplate (internal)

- Correction du blocage pouvant durer ~1 minute lors de l’enregistrement des paramètres.
- Suppression du rafraîchissement JavaScript inter-fenêtres exécuté pendant l’appel pywebview de sauvegarde.
- La sauvegarde JSON répond désormais immédiatement après persistance.
- Section À propos mise à jour avec le créateur : **DeadSynx**.
- Build interne destiné aux tests avant la future v0.9.1 publique.

## 0.8.2 — Hotplate

### Fixed
- Rétablissement fiable de l'accès aux sondes : l'application se relance elle-même avec élévation Windows via `ShellExecute("runas")`, sans remettre le manifeste PyInstaller `--uac-admin` qui causait le code 740 après installation.
- Les lectures thermiques invalides à 0 °C (ou hors plage plausible) ne sont plus affichées comme de vraies températures.
- Les températures SSD/HDD SMART à 0 °C sont considérées comme indisponibles.
- Sauvegarde des paramètres rendue atomique et validation renforcée des booléens/nombres.
- Les paramètres sont rechargés à chaque ouverture de la fenêtre et propagés aux interfaces après enregistrement.

### Changed
- Nouvelle fenêtre Paramètres « Hotplate », plus lisible, avec interrupteurs, validation des seuils, chemin de sauvegarde affiché et bouton de réinitialisation.

## 0.8.1 — Clean Launch

### Corrections
- Suppression de `--uac-admin` dans la compilation PyInstaller : Titan Monitor ne réclame plus systématiquement une élévation au lancement.
- Correction du code 740 lors du lancement automatique après installation.
- Détection renforcée d’Inno Setup dans le PATH, Program Files, LocalAppData et le registre Windows.

### Build
- Un seul script `build_release.bat` produit l’EXE, l’installateur, la version portable et les empreintes SHA-256.
- Nettoyage automatique de `build`, `dist` et `release`.
- Vérifications explicites de Python, PyInstaller, des ressources et de l’installateur.

## 0.8.0 — Brutal Contact

### Added
- Journal applicatif rotatif `TitanMonitor.log`.
- Fenêtre « À propos » accessible depuis le System Tray.
- Capture de tous les écrans depuis le menu du tray.
- Script `build_release.bat` pour compiler l'EXE puis l'installateur.
- Projet Inno Setup produisant `TitanMonitorSetup_v0.8.0_Brutal_Contact.exe`.
- Licence MIT pour la préparation du dépôt GitHub.

### Changed
- Version interne et identité visuelle mises à jour en v0.8.0 — Brutal Contact.
- Build PyInstaller compatible avec l'automatisation de release.

### Notes
- L'installateur final doit être compilé sous Windows avec Inno Setup 6.
- L'utilisateur final n'a pas besoin d'installer Python.

## 0.7.2 — Drive Awake

### Fixed
- La boucle de détection du stockage est maintenant lancée dans la fenêtre principale, et non par erreur dans l’overlay.
- Détection PowerShell forcée en UTF-8 pour éviter les sorties JSON illisibles.
- La détection de base des SSD/HDD ne dépend plus des compteurs SMART facultatifs.
- Les informations SMART/NVMe sont ajoutées dans un second temps sans empêcher l’affichage des disques.

### Verified for the reported PC
- KINGSTON SA2000M8500G — 500 Go.
- NVMe CT1000P2SSD8 — 1 To.
- Volumes C: et D: détectables via les API Windows.

## 0.7.1 — Back to Basics

### Added
- Détection automatique des SSD, HDD et volumes locaux Windows.
- État matériel exposé par Windows (`HealthStatus` / `OperationalStatus`).
- Pourcentage de santé lorsque le contrôleur expose un compteur d'usure SMART/NVMe.
- Capacité, espace utilisé et espace restant en Go pour chaque volume.
- Température et heures de fonctionnement du disque lorsqu'elles sont disponibles.
- Tensions utiles exposées par LibreHardwareMonitor : CPU VCore, SoC, GPU et rails carte mère.

### Changed
- Retour à l'overlay classique et lisible de la branche 0.6.x.
- Version interne passée à 0.7.1.

### Notes
- Certains contrôleurs RAID/USB ne transmettent pas les données SMART à Windows. Dans ce cas, Titan Monitor affiche l'état Windows sans inventer un pourcentage de santé.
