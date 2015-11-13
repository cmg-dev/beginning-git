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

* Ursprung in Linux Kernel-Community
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

### Daraus folgt

* (fast) jede Operation wirkt lokal

* eine Prüfsumme wird für jedes Objekt gebildet
* git hat eine intrinsische, rückwärtsgerichtete Integritätsprüfung!
* schwierig Daten zu manipulieren
]

---
class:
background-image: url(img/02_file_states.png)

.right-column[
### Drei Zustände, drei Sektionen

Eine Datei hat einen der folgenden Zustände:

1. committed -> Sicher in Datenbank

2. modified -> Änderung erkannt

3. staged -> Bereit für *commit*

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

1. Arbeiten an Dateien im *Working Directory*

2. *Stagen* eines Snapshots der Dateien zur *Staging Area*

3. Man führt einen *commit* durch, der die Dateien in der *Staging Area* als Snapshot im git-Verzeichnis speichert
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

Blick in das Repository

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

Alles spielt sich im *.git*-Ordner ab.

]

---
class:
background-image: url(background.png)

.example_page[

Ein paar Dateien Anlegen

```bash
git-dojo 𝚿 ls                                                        (b:master∂)
TestA.txt TestB.txt TestC.txt
```

Commit vorbereiten: Zur *Staging Area* hinzufügen

```bash
git-dojo 𝚿 git add                                                   (b:master∂)
```

Commit schreiben und Dateien von git verwalten lassen

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

Ein paar Dateien Anlegen

```bash
git-dojo 𝚿 ls                                                        (b:master∂)
TestA.txt TestB.txt TestC.txt
```
]

---
class:
background-image: url(img/05_example1.png)

.right-column[
### Was haben wir bisher getan?

**Explizit**

* drei Dateien angelegt

* diese *gestaged*

* einen *commit* erstellt

**Implizit**

* einen Branch erstellt

```bash
git-dojo 𝚿 git branch                                    (b:master)
  master
```

]

---
class:
background-image: url(img/05_1_example1.png)

.right-column[
### Was enthält der master
]

---
class:
background-image: url(img/05_2_example1.png)

.right-column[
### Arbeiten -> Commiten -> repeat.

```bash
git-dojo 𝚿 git commit -m"Mein 2. commit"                    (b:master∂)
[master ps2pduu] Mein 2. commit
 1 file changed, 1 insertions(+)

git-dojo 𝚿 git commit -m"Commit 3 :-)"                      (b:master∂)
[master ms226a5] Commit 3 :-)
 1 file changed, 1 insertions(+)
```
]

---
class:
background-image: url(img/05_3_example1.png)

.right-column[
### Woraus besteht ein *commit*?

Ein *commit* speichert im Wesentlichen die Informationen

* über den Autor
* den Zeitpunkt
* die Nachricht
* seinen *parent*

]

---
class:
background-image: url(img/00_commit_internals.png)

.right-column[
### Wo sind die Dateien?

Jeder *commit* hat eine *tree*. Genauer: jeder *commit* zeigt auf einen *tree*.

Jeder *tree* zeigt wiederum auf *blobs*, Dateien unspezifizierten Formats.

*blobs* werden in dem Ordner ```.git/objects/``` abgelegt

```bash
git-dojo 𝚿 ls -al .git/objects                                                 (b:master)
total 0
drwxr-xr-x  16 cmg  staff  544 13 Nov 11:17 .
drwxr-xr-x  14 cmg  staff  476 13 Nov 15:58 ..
drwxr-xr-x   4 cmg  staff  136 13 Nov 11:17 bh
drwxr-xr-x   3 cmg  staff  102 12 Nov 23:29 rr
drwxr-xr-x   3 cmg  staff  102 13 Nov 11:15 pl

```
]

---
class:
background-image: url(img/05_4_example1.png)

.right-column[
### Woher weiß git in welchem Branch es sich befindet?

git speichert eine Referenz (Pfad zum Branch) in **HEAD** ab.

Zu finden unter:

```bash
git-dojo 𝚿 cat .git/branch                              (b:master)
  ref: refs/heads/master
```
]

---
class: center, middle
background-image: url(background.png)
## branches

---
class:
background-image: url(background.png)

.right-column[
### Was sind branches?

Analog zu anderen VCS hat git ein 'Branching Modell'.

Man kann mehrere Zweige eines Repositories erzeugen.

Branches haben in git eine besondere Stellung.

]

---
class:
background-image: url(background.png)

.right-column[
### Was sind branches?

Es gibt zwei Arten von branches:

1. Lokale
  
  Zeigen auf einen commit im lokalen Repository.

2. Entfernte

  Alle anderen Repositories; Allerdings meistens **```origin```**

]

---
class:
background-image: url(background.png)

.right-column[
### Arbeiten mit lokalen branches
]

---
class: center, middle
background-image: url(background.png)
## Entfernte branches

---
class:
background-image: url(background.png)

.right-column[
### branch erzeugen
### branches anzeigen
]

---
class:
background-image: url(img/06_branching.png)

.right-column[
### branch erzeugen

```bash
git-dojo 𝚿 git branch Bug1                           (b:master)
```

### branches anzeigen

```bash
git-dojo 𝚿 git branch -a                              (b:master)
  Bug1
  *master
```
]

---
class:
background-image: url(background.png)

.right-column[
### *checkout* Lokalen branch
### *checkout* Entfernten branch
]

---
class:
background-image: url(background.png)

.right-column[
### Lokalen Branch löschen
### Entfernten Branch löschen
]

---
class: center, middle
background-image: url(background.png)
## Zusammenarbeit

---
class:
background-image: url(background.png)
.right-column[
### Fazit

Die Möglichkeiten zur Zusammenarbeit bei git sind vielfältig.

git stellt keine Ansprüche an die Projektstruktur.

Aus großer Macht folgt große Verantwortung!
]

---
class: center, middle
background-image: url(background.png)
## merging

---
class:
background-image: url(img/07_merging_FF.png)

.right-column[
### merge mit Fast Forward

Branch **master** auschecken:

```bash
git-dojo 𝚿 git checkout master                           (b:Bug1)
Switched to branch 'master'
```

Merge mit Standardverhalten:


```bash
git-dojo 𝚿 git merge                                   (b:master)

```
]

---
class:
background-image: url(img/07_merging_nFF.png)

.right-column[
### merge non Fast Forward

Branch **master** auschecken:

```bash
git-dojo 𝚿 git checkout master                           (b:Bug1)
Switched to branch 'master'
```

Merge mit option ```--no-ff```:


```bash
git-dojo 𝚿 git merge --no-ff                           (b:master)

```

Man erhällt einen Merge commit, der auf zwei *parents* zeigt.
]

---
class:
background-image: url(background.png)

.right-column[
### merge conflict

Arbeiten mehrere Personen an ein und demselben Quellcode, dann kommt es früher oder später zu Konflikten.

git stellt Leistungsfähige Mechanismen zur Lösung dieser Probleme bereit.

Also: **Keine Angst vor Konflikten!**

Damit ein Konflikt auftreten kann, muss eine Datei in git getrackt werden.

Ist eine Datei 'im git getrackt' dann können die Daten nicht verloren gehen. Auch beim rücksichtslosesten Merge nicht!
]
---
class:
background-image: url(background.png)

.example_page[

### Vorbereitung

**Entwickler A**

*commit* und *push* mit seine Änderungen

```bash
git-dojo 𝚿 git add TestA.txt                                             (b:master∂)
git-dojo 𝚿 git commit -m"TestA prepared to conflict"                     (b:master∂)
[master 54a4672] TestA prepared to conflict
 1 file changed, 1 insertion(+)

git-dojo 𝚿 git push                                                      (b:master)
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 340 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:cmg-dev/git-dojo
   a171e02..54a4672  master -> master
```
]

---
class:
background-image: url(background.png)

.example_page[

### Vorbereitung

**Entwickler B**

Tut das selbe wie Entwickler A...

```bash
git-dojo2 𝚿 git add TestA.txt                                            (b:master∂)
git-dojo2 𝚿 git commit -m"TestA shall now cause a merge conlict"         (b:master∂)
[master d451ea8] TestA shall now cause a merge conlict
 1 file changed, 1 insertion(+)
```
]

---
class:
background-image: url(background.png)

.example_page[
### OhOh... merge conflict :-(

Weil **Entwickler B** gewissenhaft ist, führt er vor dem *push* einen *pull* aus.

```bash
git-dojo2 𝚿 git pull                                                      (b:master)
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:cmg-dev/git-dojo
   a171e02..54a4672  master     -> origin/master
Auto-merging TestA.txt
CONFLICT (content): Merge conflict in TestA.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Das hat er jetzt davon...
]

---
class:
background-image: url(background.png)

.example_page[
### Was sagt *git status*?

```bash
git-dojo2 𝚿 git status                                                   (b:master∂)
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 1 different commit each, respectively.
  (use "git pull" to merge the remote branch into yours)
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   TestA.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
]

---
class:
background-image: url(background.png)

.example_page[
### Was ist passiert?

Es ist ohne große Hilfsmittel möglich den Konflikt zu lösen.

Das erste Tool ist *git diff*, das uns die Änderungen in einem Diff-Kommentar anzeigt

```bash
git-dojo2 𝚿 git diff                                                     (b:master∂)
diff --cc TestA.txt
index 32d0279,9f985ab..0000000
--- a/TestA.txt
+++ b/TestA.txt
@@@ -1,2 -1,2 +1,6 @@@
  Das ist ein Test...
++<<<<<<< HEAD
 +Merge me
++=======
+ Merge me...
++>>>>>>> 54a467267033f03aaf03be4cad8e11af9b6dd980
```

Eine Lösung des Problems führt über einen Handelsüblichen Texteditor.
]

---
class:
background-image: url(background.png)

.example_page[

### Lösung

```bash
git-dojo2 𝚿 cat TestA.txt                                                (b:master∂)
Das ist ein Test...
<<<<<<< HEAD
Merge me
=======
Merge me...
>>>>>>> 54a467267033f03aaf03be4cad8e11af9b6dd980
```

Mit einem Editor den Konflikt lösen.
Löschen der Diff-Kommentare, die Änderungen, die wir behalten wollen aber stehen lassen ;)

```bash
git-dojo2 𝚿 vim TestA.txt                                                (b:master∂)

git-dojo2 𝚿 cat TestA.txt                                                (b:master∂)
Das ist ein Test...
Merge me
```
]

---
class:
background-image: url(background.png)

.example_page[

### Lösung 2

```bash
git-dojo2 𝚿 git commit                                                    (b:master)
```

Löschen der Diff-Kommentare, die Änderungen, die wir behalten wollen aber stehen lassen ;)

```bash
git-dojo2 𝚿 git commit                                                   (b:master∂)
Merge branch 'master' of github.com:cmg-dev/git-dojo

# Conflicts:
#	TestA.txt
```
```bash
git-dojo2 𝚿 git commit                                                    (b:master)
[master f86d4f6] Merge branch 'master' of github.com:cmg-dev/git-dojo
```
]

---
class:
background-image: url(background.png)

.example_page[

### Lösung 3

Nun erfolgt der *push*

```bash
git-dojo2 𝚿 git push                                                      (b:master)
Counting objects: 4, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 563 bytes | 0 bytes/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To git@github.com:cmg-dev/git-dojo
   54a4672..f86d4f6  master -> master
```
]


---
class: center, middle
background-image: url(background.png)

## Best Practice

---
class:
background-image: url(background.png)

.right-column[
### *stash* benutzen
### *commits* sauber halten
]

---
class:
background-image: url(background.png)

.right-column[
### Zuerst *pullen*/ *mergen*

### Anschließend *commit*
]

---
class: center, middle
background-image: url(background.png)
## Spezielle Themen
---
class:
background-image: url(background.png)

.right-column[
### Delta Kompression

git führt bei der Speicherung der Daten eine [Delta Compression](https://gist.github.com/matthewmccullough/2695758) durch.

Dies stellt eine sehr effiziente Methode der Komprimierung für textbasierte Dokumente dar.

Auch 'binäre'-Objekte (z.B. .docx) können so gespeichert werden.
]

---
class:
background-image: url(background.png)

.right-column[
### git rebase

Restrukturierung der *commit*-Historie.

Tipp: **Finger Weg!**
]
---

---
class:
background-image: url(background.png)

.right-column[
### git flow
Workflow Muster für git mit starker Neigung zu Qualitätssteigerung des Quellcodes.

Nutzt zentralisiertes Repository für die Arbeit vieler Entwickler.

Thema einer anderen [Präsentation](http://5minds.github.io/git-flow-bestpractice)...
]
---
class: center, middle
background-image: url(background.png)
## Tipps und Tricks

---
class: middle
background-image: url(background.png)
### Cheat Sheet

Für die tägliche Arbeit kann ein [git cheat sheet](http://www.git-tower.com/blog/git-cheat-sheet/) sehr hilfreich sein.

---
