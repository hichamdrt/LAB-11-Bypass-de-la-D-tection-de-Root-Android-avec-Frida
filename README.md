# LAB-11-Bypass-de-la-D-tection-de-Root-Android-avec-Frida
# 🔐 LAB 11 — Analyse et contournement pédagogique de la détection Root Android avec Frida

## Présentation du laboratoire

Ce laboratoire a pour objectif d’étudier le mécanisme de détection du root dans une application Android et d’observer comment un outil d’instrumentation dynamique comme **Frida** peut être utilisé, dans un environnement pédagogique autorisé, afin de neutraliser cette protection.

L’analyse est réalisée dans un environnement contrôlé à des fins d’apprentissage en sécurité mobile.

### Informations du laboratoire

| Élément         | Valeur                          |
| --------------- | ------------------------------- |
| Application     | Uncrackable1                    |
| Package Android | `com.example.mstg.uncrackable1` |
| Outil principal | Frida                           |
| Environnement   | Android Emulator                |

---

# 🎯 Objectifs pédagogiques

À travers ce lab, l’apprenant doit être capable de :

* comprendre le fonctionnement de la détection root sur Android ;
* analyser le comportement initial d’une application protégée ;
* identifier le package d’une application avec Frida ;
* utiliser un script Frida pour contourner une protection anti-root ;
* vérifier le comportement de l’application après le bypass.

---

# 1. Présentation du lab

La première étape consiste à présenter le contexte du laboratoire ainsi que les différentes manipulations qui seront réalisées.

Le laboratoire intitulé :

## LAB 11 — Analyse et Bypass de la Détection Root Android avec Frida

montre comment une application Android peut détecter un environnement rooté et comment cette détection peut être neutralisée à l’aide de hooks Java dans un cadre pédagogique sécurisé.

**Capture associée :** `pic1`

---

# 2. Observation du comportement initial

Lors du lancement de l’application **Uncrackable1** sur l’émulateur Android, l’application effectue automatiquement des vérifications liées au root.

L’application affiche alors le message suivant :

```text id="2yyr1n"
Root detected! This is unacceptable. The app is now going to exit.
```

Cette alerte indique que le mécanisme anti-root est actif et que l’application interrompt volontairement son exécution.

L’utilisateur ne peut donc pas accéder à l’interface principale tant que cette protection reste active.

**Capture associée :** `pic2`

---

# 3. Identification du package avec Frida

Avant d’injecter un script Frida, il est nécessaire d’identifier précisément le package Android de l’application cible.

La commande utilisée est :

```bash id="n1p4ui"
frida-ps -Uai
```

### Explication

| Option     | Description                                 |
| ---------- | ------------------------------------------- |
| `frida-ps` | Liste les processus et applications         |
| `-U`       | Connexion à l’appareil ou émulateur Android |
| `-a`       | Affiche les applications                    |
| `-i`       | Affiche les informations détaillées         |

Dans la liste obtenue, on retrouve :

| Application  | Package                         |
| ------------ | ------------------------------- |
| Uncrackable1 | `com.example.mstg.uncrackable1` |

**Capture associée :** `pic3`

---

# 4. Injection du script Frida

Une fois le package identifié, l’étape suivante consiste à lancer l’application avec Frida tout en injectant un script JavaScript chargé de neutraliser la détection root.

Commande utilisée :

```bash id="l1y5xm"
frida -U -f com.example.mstg.uncrackable1 -l E:\MGR\mobile\lab\bypass.js
```

## Détails de la commande

| Élément                         | Rôle                                             |
| ------------------------------- | ------------------------------------------------ |
| `frida`                         | Outil d’instrumentation dynamique                |
| `-U`                            | Connexion à l’émulateur Android                  |
| `-f`                            | Lance l’application cible                        |
| `com.example.mstg.uncrackable1` | Package Android ciblé                            |
| `-l`                            | Charge un script JavaScript                      |
| `bypass.js`                     | Script utilisé pour contourner la détection root |

Après exécution, Frida se connecte à l’émulateur puis injecte automatiquement le script dans l’application au démarrage.

**Capture associée :** `pic3`

---

# 5. Vérification après le bypass

Après l’injection du script Frida, l’application est relancée.

Cette fois :

* le message *Root detected* n’apparaît plus ;
* l’application ne se ferme plus automatiquement ;
* l’interface principale devient accessible.

Cela confirme que le mécanisme de détection root a été neutralisé avec succès dans le cadre du laboratoire.

**Capture associée :** `pic4`

---

# ✅ Résultats obtenus

## Avant le bypass

* Détection du root active ;
* affichage d’un message d’alerte ;
* fermeture automatique de l’application.

## Après le bypass

* application accessible normalement ;
* suppression du blocage lié au root ;
* accès complet à l’interface utilisateur.

---

# 🧰 Commandes utilisées

## Identification des applications Android

```bash id="x7ulx0"
frida-ps -Uai
```

## Injection du script Frida

```bash id="ndn12r"
frida -U -f com.example.mstg.uncrackable1 -l E:\MGR\mobile\lab\bypass.js
```
<img width="241" height="468" alt="image" src="https://github.com/user-attachments/assets/79016317-9d7b-4838-8eb1-00571bead212" />
<img width="251" height="311" alt="image" src="https://github.com/user-attachments/assets/3afd0b93-e5a9-457b-88d5-bedae83511f0" />
<img width="1441" height="1091" alt="image" src="https://github.com/user-attachments/assets/0d02ebed-2d1f-4766-bca2-d1e9ec56a551" />
<img width="1987" height="791" alt="image" src="https://github.com/user-attachments/assets/b9d5743c-02ee-41d1-954a-fe8eab56a7fa" />
<img width="1987" height="791" alt="image" src="https://github.com/user-attachments/assets/8b7cfe0a-4b78-4e95-ba1b-fe7e4a276f05" />
