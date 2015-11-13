class: middle, center
background-image: url(background-intro.png)

# Beginning git

---
class: middle, center
background-image: url(background.png)

## Versionskontrollsysteme (VCS)

---
class:
background-image: url(background.png)

.right-column[

### Woher kommt git?
]

---
class:
background-image: url(background.png)

.right-column[

### Woher kommt git?

* Urpsrung in Linux Kernel-Community
* Von Linus Torvalds entwickelt
* Eingesetzt für die Kernel Entwicklung
* Weitere OpenSource Projekte folgen
* github.com und Bitbucket.com starten
* Ausgereifte GUIs entstehen
* ...
* Microsoft TFS verwendet git!

]

---
class: top, center
background-image: url(background.png)

### Was kann git?

---
class: top, center
background-image: url(img/01_design_goals.png)

### Was kann git?

---
class: middle, center
background-image: url(background.png)

## git ist ein Dateisystem!

---
class:
background-image: url(background.png)

.right-column[
### Warum das?

* git denkt in **Snapshots**
* Andere in **Differences**


* (fast) jede Operation wirkt lokal


* eine Prüfsumme wird jedes mal gebildet
* git hat eine intrinsische, rückwärtsgerichtete Integritätsprüfung!
* schwierig Daten zu manipulieren
]

---
class:
background-image: url(img/02_file_states.png)

.right-column[
### Drei Zustände, drei Sektionen

Eine Datei kann entweder:

1. committed -> Sicher in Datenbank

2. modified -> Änderung erkannt

3. staged -> Bereit für *commit*

sein.
]


---
class:
background-image: url(img/03_dirs.png)

.right-column[
### Sektionen
1. Arbeitsverzeichnis

  *checkout* einer Version des Projekts

1. Staging Area

  Datei wird beim nächsten *commit* eingeschlossen.

1. .git Verzeichnis (Repository)

  Wichtigster Teil von git.
  Alle Metadaten und Objekte liegen hier.

]
---
class:
background-image: url(img/04_workflow.png)

.right-column[
### Workflow

Zum Schluss betrachten wir den typischen, alltäglichen Workflow

1. Arbeiten an Datein im *Working Directory*

2. *Stagen* eines Snapshots der Datein zur *Staging Area* 

3. Man führt einen *commit* durch, der die Datein in der *Staging Area* als Snapshot im git-Verzeichnis speichert
]
---
class:
background-image: url(background.png)

.example_page[
### Ein trockenes Beispiel:

```bash
git-dojo 𝚿 git status                                           (b:master∂)
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   TestA.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   TestB.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        TestC.txt
```
]

---
class: middle, center
background-image: url(background.png)

## Der Einstieg...

---
background-image: url(img/s0_start.png)
.right-column[
## Anfang

```bash
  » git init .
```

Macht einen leeren Ordner zum Repository.

]

---
background-image: url(img/s0_start.png)
.right-column[
## Anfang

Blick ins Repo

```bash
  » ls -al
      .git/
      ▸ branches/
      ▸ hooks/
      ▸ info/
      ▸ objects/
      ▸ refs/
        config
        description
        HEAD
```

Es exisitert alles im Ordner *.git*
]

---
class:
background-image: url(background.png)

.example_page[

Ein paar Datein Anlegen

```bash
git-dojo 𝚿 ls                                                        (b:master∂)
TestA.txt TestB.txt TestC.txt
```

Commit vorbeteiten: Zur *Staging Area* hinzufügen

```bash
git-dojo 𝚿 git add                                                   (b:master∂)
```

Commit schreiben und Datein in die Obhut von git geben

```bash
git-dojo 𝚿 git commit -m "Sinnvolle Nachricht"                        (b:master)
[master (root-commit) bac26a6] Sinnvolle Nachricht
 3 files changed, 5 insertions(+)
 create mode 100644 TestA.txt
 create mode 100644 TestB.txt
 create mode 100644 TestC.txt
```
]

---
class:
background-image: url(background.png)

.example_page[

Ein paar Datein Anlegen

```bash
git-dojo 𝚿 ls                                                        (b:master∂)
TestA.txt TestB.txt TestC.txt
```
]
---
class: center, middle
background-image: url(background.png)
## Tipps und Tricks

---
