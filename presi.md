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

## Was ist git?

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
]

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
* das macht schwierig Daten zu manipulieren
]

---
class:
background-image: url(img/02_file_states.png)

.right-column[
### Drei Zustände, drei Sektionen

Eine Datei hat **immer** einen der folgenden Zustände:

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

  Ist *checkout* einer Version des Projekts.

1. Staging Area

  Sammelt Dateien, die beim nächsten *commit* übernommen werden.

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

**1. Ein paar Dateien Anlegen**

```bash
git-dojo 𝚿 ls                                                        (b:master∂)
TestA.txt TestB.txt TestC.txt
```
]

---
class:
background-image: url(background.png)

.example_page[

**1. Ein paar Dateien Anlegen**

```bash
git-dojo 𝚿 ls                                                        (b:master∂)
TestA.txt TestB.txt TestC.txt
```

**2. Commit vorbereiten: Zur *Staging Area* hinzufügen**

```bash
git-dojo 𝚿 git add                                                   (b:master∂)
```

]

---
class:
background-image: url(background.png)

.example_page[

**1. Ein paar Dateien Anlegen**

```bash
git-dojo 𝚿 ls                                                        (b:master∂)
TestA.txt TestB.txt TestC.txt
```

**2. Commit vorbereiten: Zur *Staging Area* hinzufügen**

```bash
git-dojo 𝚿 git add                                                   (b:master∂)
```

** 3. Commit schreiben und Dateien von git verwalten lassen**

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
background-image: url(img/05_example1.png)

.right-column[
### Was haben wir bisher getan?
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

Der **master** enthält den Hash des Commits auf den er zeigt.

]

---
class:
background-image: url(img/05_1_example1.png)

.right-column[
### Exkurs Hash

git generiert zu jeden Objekt ein SHA-1 Hash.

Referenzierungen werden nur über diesen Hash gemacht.

```bash
git-dojo 𝚿 cat .git/refs/heads/master                    (b:master)
bac26a6fd948d6565b36c6205fbb08a3b420dd57
```

Es ist ausreichend die ersten 7 Stellen des Hash zu verwenden!

Das ist die Standardeinstellung und ~30k Commits können so eindeutig identifiziert werden.
]

---
class:
background-image: url(img/05_2_example1.png)

.right-column[
### Modify -> Add ->  Commit -> repeat

**Neue Änderungen ins Repository aufnehmen**

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
background-image: url(img/05_2_example1.png)

.right-column[
### Modify -> Add ->  Commit -> repeat

Ein *commit* zeigt immer auf seinen Vorgänger.

git speichert so einen Baum zurück zum ersten *commit*.
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
background-image: url(img/05_3_example1.png)

.right-column[
### Woher weiß git in welchem Branch es sich befindet?
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
class:
background-image: url(img/00_commit_internals.png)

.right-column[
### Wo sind die Dateien?

Jeder *commit* hat eine *tree*. Genauer: jeder *commit* zeigt auf einen *tree*.

Jeder *tree* zeigt wiederum auf *blobs*.

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
background-image: url(img/00_1_commit_internals.png)

.right-column[
### Wo sind die Dateien?

So sieht es bei jeden beliebigen Commit aus.

Aus Gründen der Übersicht, werden die *tree*-Objekte nicht dargestellt.
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
background-image: url(img/06_branching.png)

.right-column[
### branch erzeugen

```bash
git-dojo 𝚿 git branch Bug1                           (b:master)
```

### branches anzeigen

```bash
git-dojo 𝚿 git branch                                (b:master)
  Bug1
  *master
```
]

---
class:
background-image: url(img/06_1_branching.png)

.right-column[

### Arbeiten mit lokalen branches

**Branch auschecken**
``` bash
git-dojo 𝚿 git checkout Bug1                          (b:master)
Switched to branch 'Bug1'
```

**commit** der Arbeit

```bash
git-dojo 𝚿 git commit -m"Bug identifiziert"             (b:Bug1∂)
[Bug1 13rrt37] Ein commit in Bug1
 1 file changed, 2 insertions(+)
 create mode 100644 TestA.clone.txt

git-dojo 𝚿 git commit -m"Bug gefixt"                    (b:Bug1∂)
[Bug1 pa2d216] Ein commit in Bug1
 1 file changed, 3 insertions(+)
 create mode 100644 TestB.clone.txt
```
]

---
class:
background-image: url(img/06_2_branching.png)

.right-column[

### Arbeiten mit lokalen branches

**Arbeit finalisieren**

Jetzt ist ein guter Zeitpunkt gekommen um automatisierte Tests durchlaufen zu lassen.

An diesem Punkt können wir auch entscheiden, die Arbeit mit anderen Entwicklern zu teilen.

Zuerst aber lernen wir, wie wir zwischen Branches wechseln.
]

---
class:
background-image: url(img/06_4_branching.png)

.right-column[

### Von Bug1 nach master wechseln

```bash
git-dojo 𝚿 git checkout master                            (b:Bug1)
Switched to branch 'master'
```

**HEAD** zeigt nun auf **master**

]

---
class:
background-image: url(img/06_3_branching.png)

.right-column[

### Von master nach Bug1 wechseln

```bash
git-dojo 𝚿 git checkout Bug1                            (b:master)
Switched to branch 'Bug1'
```

Der nächste Schritt ist das Zusammenführen der Branches

]

---
class:
background-image: url(img/07_merging_FF.png)

.right-column[

### Zusammenführen von master und Bug1

```bash
git-dojo 𝚿 git checkout master                            (b:Bug1)
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

git-dojo 𝚿 git merge Bug1                               (b:master)
Merge made by the 'recursive' strategy.
 TestA.clone.txt | 2 ++
 TestB.clone.txt | 3 +++
 2 files changed, 5 insertions(+)
 create mode 100644 TestA.clone.txt
 create mode 100644 TestB.clone.txt
```
]

---
class: center, middle
background-image: url(background.png)
## Entfernte branches

---
class:
background-image: url(img/09_remote_branch.png)

.right-column[

### remote branches anzeigen

```bash
git-dojo 𝚿 git branch -r                              (b:master)
  origin/master
```

Alle auf dem remote befindlichen Branches werden so angezeigt.
]

---

class:
background-image: url(img/09_1_remote_branch.png)

.right-column[

### Lokalen Branch *puschen*
**Lokalen Branch einem *remote* bekannt machen**

```bash
git-dojo 𝚿 git checkout Bug1                          (b:master)
Switched to branch 'Bug1'

git-dojo 𝚿 git push -u origin Bug1                      (b:Bug1)
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:cmg-dev/git-dojo
 *[new branch]      Bug1 -> Bug1
```
]

---
class:
background-image: url(img/09_1_remote_branch.png)

.right-column[

### remote tracking branches

Branches mit sog. *Upstream Tracking* haben eine direkte Beziehung mit einem entfernten Branch.

Wenn in einem *tracking*-Branch ein *pull* oder *push* ausgeführt weiß git sofort von wo es die Daten holen soll.

```bash
git-dojo 𝚿 cat .git/config                                (b:Bug1)
(...)
[branch "master"]
        remote = origin
        merge = refs/heads/master
[branch "Bug1"]
        remote = origin
        merge = refs/heads/Bug1
(...)
```
]

---
class:
background-image: url(background.png)

.right-column[

### *checkout* entfernten branch

```bash
git-dojo 𝚿 git checkout -b Bug1 origin/Bug1             (b:master)
Switched to branch 'Bug1'
Your branch is up-to-date with 'origin/Bug1'.
```

### *checkout* lokalen tracking branch

```bash
git-dojo 𝚿 git checkout Bug1             (b:master)
```
]

---
class:
background-image: url(background.png)

.right-column[
### Lokalen Branch löschen

```bash
git-dojo 𝚿 git branch -D Bug1                           (b:master)
Deleted branch Bug1 (was aec1cab).
```
### Entfernten Branch löschen

```bash
git-dojo 𝚿 git push origin :Bug1                        (b:master)
To git@github.com:cmg-dev/git-dojo
 - [deleted]         Bug1
```
]

---
class: center, middle
background-image: url(background.png)
## Zusammenarbeit

---
class:
background-image: url(img/08_collaboration.png)
.right-column[
### Alice und Bob

Zwei Entwickler arbeiten nun an gemeinsamer Codebasis.

Beide *clonen* das Basisrepository:

**Alice**

```bash
src 𝚿 git clone git@github.com:cmg-dev/git-dojo
```

**Bob**

```bash
src 𝚿 git clone git@github.com:cmg-dev/git-dojo
```
]

---
class:
background-image: url(img/08_collaboration.png)
.right-column[
### Alice und Bob

Zwei Entwickler arbeiten nun an gemeinsamer Codebasis.

**Alice**

```bash
src 𝚿 git clone git@github.com:cmg-dev/git-dojo
Cloning into 'git-dojo'...
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 3 (delta 1), reused 2 (delta 1), pack-reused 0
Receiving objects: 100% (3/3), 4.04 KiB | 0 bytes/s, done.
Resolving deltas: 100% (1/1), done.
Checking connectivity... done.
```
]

---
class:
background-image: url(img/08_1_collaboration.png)
.right-column[
### Alice und Bob

**Alice** hat sich um den Bugfix gekümmert

Drei *commits* hat Alice gebraucht.

**Bob** hat eine GUI implementiert

Bob hat die Änderungen für die GUI in einem *commit* zusammengefasst.
Aber sein *commit* ist nach Alice Arbeit entstanden.

]

---
class: middle, center
background-image: url(background.png)

## Zusammenführen

---
class: top, center
background-image: url(img/08_2_collaboration.png)

### Alice führt einen *push* aus

---
class:
background-image: url(img/s8_push.png)
.right-column[
### Alice führt einen *push* aus

```bash
git-dojo 𝚿 git push                                     (b:master)

Counting objects: 5, done.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 167.98 KiB | 0 bytes/s, done.
Total 5 (delta 2), reused 0 (delta 0)
To git@www.github.com:cmg-dev/git-dojo
   4tuihw90...f41aa9d  master -> master push
```
]

---
class: top, center
background-image: url(img/08_3_collaboration.png)

### Bob führt einen *pull* aus

---
class:
background-image: url(img/s8_pull.png)
.right-column[
### Bob führt einen *pull* aus

```bash
git-dojo 𝚿 git pull                                     (b:master)

remote: Counting objects: 5, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 5 (delta 2), reused 3 (delta 2), pack-reused 0
Unpacking objects: 100% (5/5), done.
From www.github.com:cmg-dev/beginning-git
   f41aa9d..38f0c16  master     -> origin/master
Updating f41aa9d..38f0c16
Fast-forward
```
]

---
class: top, center
background-image: url(img/08_4_collaboration.png)

## Alice will Bob's Änderungen haben

---
class: top, center
background-image: url(img/08_5_collaboration.png)

## Vollständig synchronisiert

---
class:
background-image: url(background.png)
.right-column[

### Fazit

In diesem Abschnitt haben wir:

1. den Standard Workflow zum Arbeiten mit Remote-Repositories verwendet

2. änderungen zum Remote *gepusht*

3. änderungen vom Remote *gepullt*

Diese Arbeitsweise lässt sich mit vielen Entwicklern gut umsetzen.
]

---
class: center, middle
background-image: url(background.png)

## merging

---
class:
background-image: url(img/06_2_branching.png)

.right-column[
### Kurzer Rückblick

Für das Zusammenführen haben wir zwei Möglichkeiten:

1. Fast Forward

  Merge ohne einen *merge commit*

2. non Fast Forward

  Mit einem *merge commit*

]

---
class:
background-image: url(img/07_merging_FF.png)

.right-column[
### merge - 'Fast Forward'

Branch **master** auschecken:

```bash
git-dojo 𝚿 git checkout master                           (b:Bug1)
Switched to branch 'master'
```

Merge mit Standardverhalten:


```bash
git-dojo 𝚿 git merge Bug1                              (b:master)

```
]

---
class:
background-image: url(img/07_merging_nFF.png)

.right-column[
### merge - 'non Fast Forward'

Branch **master** auschecken:

```bash
git-dojo 𝚿 git checkout master                           (b:Bug1)
Switched to branch 'master'
```

Merge mit option ```--no-ff```:


```bash
git-dojo 𝚿 git merge Bug1 --no-ff                      (b:master)

```

Man erhällt einen Merge commit, der auf zwei *parents* zeigt.
]

---
class: center, middle
background-image: url(background.png)

## merging - Konflikte beheben

---
class:
background-image: url(background.png)

.right-column[
### merge conflict

Arbeiten mehrere Personen an ein und demselben Quellcode, dann kommt es früher oder später zu Konflikten.

git stellt leistungsfähige Mechanismen zur Lösung dieser Probleme bereit.

Also: **Keine Angst vor Konflikten!**

Damit ein Konflikt auftreten kann, muss eine Datei in git getrackt werden.

Ist eine Datei 'im git getrackt' dann können die Daten nicht verloren gehen. Auch beim rücksichtslosesten Merge nicht!
]
---
class:
background-image: url(background.png)

.example_page[

### Vorbereitung

**Alice**

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

**Bob**

Tut das selbe wie Alice...

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

Weil **Bob** gewissenhaft ist, führt er vor dem *push* einen *pull* aus.

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

.example_page[

### ssh Benutzen

**Public - Private Schlüsselpaar erzeugen**

```bash
  » ssh-keygen -t rsa
```

Bei verwenden der git Befehle in folgender Form:
```bash
  » git clone git@xyz.com:REPO.git
```

Wird automatisch ssh-Verschlüsselung eingesetzt um den Transport ab zu sichern
]

---
class:
background-image: url(background.png)

.example_page[

### Sieben Regeln für gute *commit*-Nachrichten

1. Trennen von *subject* und *body*  mit einer leeren Zeile

1. Auf 50 Zeichen pro Zeile beschränken

1. *Subject*mit Großbuchstaben beginnen

1. *Subject*Zeile nicht mit einen Punkt beenden

1. Verwenden des Imperativs in *subject*

1. Zeilenumbruch bei 72 Zeichen im *body*

1. Im *body* Was und Warum erklären nicht Wie

[Quelle](http://chris.beams.io/posts/git-commit/)
]
---
class:
background-image: url(background.png)

.example_page[

### Sieben Regeln für gute *commit*-Nachrichten - Ein Beispiel
```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequenses of this
change? Here's the place to explain them.

(...)
```

[Quelle](http://chris.beams.io/posts/git-commit/)
]

---
class:
background-image: url(background.png)

.example_page[

### Sieben Regeln für gute *commit*-Nachrichten - Ein Beispiel
```
(...)

Further paragraphs come after blank lines.

 - Bullet points are okay, too

  - Typically a hyphen or asterisk is used for the bullet, preceded
     by a single space, with blank lines in between, but conventions
        vary here

        If you use an issue tracker, put references to them at the bottom,
        like this:

        Resolves: #123
        See also: #456, #789
```

[Quelle](http://chris.beams.io/posts/git-commit/)
]

---
class:
background-image: url(background.png)

.right-column[
### *stash* benutzen
]

---
class:
background-image: url(background.png)

.example_page[
### *commits* sauber halten

Unabsichtig zu git hinzugefügte Dateien sind ärgerlich.

Daher sollte jeder *commit* gewissenhaft durchgeführt werden:

1. Mit *git status* prüfen welche Änderungen vorgenommen wurden

2. **Explizit** mit ```git add <Datei_1> .. <Datei_N> ``` arbeiten

3. Prüfen ob nur das in der *Staging Area* ist, was im *commit* landen soll

4. *commit* durchführen

]

---
class:
background-image: url(background.png)

.example_page[

### *commits* sauber halten

Wenn eine Datei zur *Stating Area* hinzugefügt wurde, die dort nicht hin soll, kann man sie mit:

```bash
  » git rm <Datei>
```

entfernt werden.

Will man den gesamten ```git add```-Vorgang zurück setzen kann:

```bash
  » git reset
```

verwendet werden.

]
---
class:
background-image: url(background.png)

.example_page[

### *commits* sauber halten

Um eine Datei vollständig aus dem Repository zu nehmen, kann der Befehl:

```bash
  » git filter-branch
```

verwendet werden.

Das ist ein sehr starker Eingriff in die Struktur des Repositories.

Nur verwenden wenn man unbedingt muss!
]

---
class:
background-image: url(background.png)

.right-column[
### Zuerst *pullen*/ *mergen*

Wenn man an einem branch arbeitet, in dem andere Entwckler ihre Arbeit commiten, sollte man vor einem *commit* die Änderungen holen.

### Anschließend *commit*

Man erhält einen *merge commit* vor dem *commit* der eigenen Arbeit.

]

---
class: top, center
background-image: url(img/00_1_misc.png)

### Pull first vs. Other

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
