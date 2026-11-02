# Esercizio di risoluzione di un merge conflict

**Il tempo massimo in laboratorio per questo esercizio è di _20 minuti_.
Se superato, sospendere l'esercizio e riprenderlo per ultimo!**

Si visiti https://github.com/APICe-at-DISI/OOP-git-merge-conflict-test.
Questo repository contiene due branch: `master` e `feature`

Per ognuna delle seguenti istruzioni, si annoti l'output ottenuto.
Prima di eseguire ogni operazione sul worktree o sul repository,
si verifichi lo stato del repository con `git status`.

1. Si cloni localmente il repository

PS C:\Users\matti> git clone https://github.com/APICe-at-DISI/OOP-git-merge-conflict-test.git
Cloning into 'OOP-git-merge-conflict-test'...
remote: Enumerating objects: 24, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 24 (delta 5), reused 13 (delta 5), pack-reused 8 (from 1)
Receiving objects: 100% (24/24), done.
Resolving deltas: 100% (6/6), done.

PS C:\Users\matti> cd .\OOP-git-merge-conflict-test\

PS C:\Users\matti\OOP-git-merge-conflict-test> git status
On branch master
Your branch is up to date with 'origin/master'.
nothing to commit, working tree clean

2. Ci si assicuri di avere localmente entrambi i branch remoti

PS C:\Users\matti\OOP-git-merge-conflict-test> git branch -v
* master 2f617a5 switch to Java 25 IO.println

PS C:\Users\matti\OOP-git-merge-conflict-test> git checkout -b feature origin/feature
branch 'feature' set up to track 'origin/feature'.
Switched to a new branch 'feature'

PS C:\Users\matti\OOP-git-merge-conflict-test> git branch -v
* feature d809d3e switch to Java 25 IO.println
  master  2f617a5 switch to Java 25 IO.println

PS C:\Users\matti\OOP-git-merge-conflict-test> git status
On branch feature
Your branch is up to date with 'origin/feature'.
nothing to commit, working tree clean

3. Si faccia il merge di `feature` dentro `master`, ossia: si posizioni la `HEAD` su `master` e da qui si esegua il merge di `feature`

PS C:\Users\matti\OOP-git-merge-conflict-test> git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

PS C:\Users\matti\OOP-git-merge-conflict-test> git status
On branch master
Your branch is up to date with 'origin/master'.
nothing to commit, working tree clean

PS C:\Users\matti\OOP-git-merge-conflict-test> git merge feature
Auto-merging HelloWorld.java
CONFLICT (content): Merge conflict in HelloWorld.java
Automatic merge failed; fix conflicts and then commit the result.

PS C:\Users\matti\OOP-git-merge-conflict-test> git status
On branch master
Your branch is up to date with 'origin/master'.
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)
Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   HelloWorld.java
no changes added to commit (use "git add" and/or "git commit -a")

4. Si noti che viene generato un **merge conflict**!

5. Si risolva il merge conflict come segue:
   - Il programma Java risultante deve stampare sia il numero di processori disponibili (funzionalità presente su `master`) che il nome dell'autore del file (funzionalità presente su `feature`)

PS C:\Users\matti\OOP-git-merge-conflict-test> cat HelloWorld.java
final String AUTHOR = "Danilo Pianini";
int procNumber() {
        return Runtime.getRuntime().availableProcessors();
}
void main() {
        IO.println("This program is running in a PC with " + procNumber() + " logic processors!");
        IO.println("This program has been realised by " + AUTHOR);
}

PS C:\Users\matti\OOP-git-merge-conflict-test> javac HelloWorld.java

PS C:\Users\matti\OOP-git-merge-conflict-test> java HelloWorld
This program is running in a PC with 8 logic processors!
This program has been realised by Danilo Pianini

PS C:\Users\matti\OOP-git-merge-conflict-test> git add HelloWorld.java

PS C:\Users\matti\OOP-git-merge-conflict-test> git commit --no-edit
[master 9c5d358] Merge branch 'feature'

PS C:\Users\matti\OOP-git-merge-conflict-test> git log --all --graph --oneline
*   9c5d358 (HEAD -> master) Merge branch 'feature'
|\
| * d809d3e (origin/feature, feature) switch to Java 25 IO.println
| * e4ee4cb switch to Java 25 compact source file
| * bed943f Print author information
* | 2f617a5 (origin/master, origin/HEAD) switch to Java 25 IO.println
* | 9c519e7 switch to Java 25 compact source file
* | 8e0f29c Change HelloWorld to print the number of available processors
|/
* d956df6 Create .gitignore
* 700ee0b Create HelloWorld

6. Si crei un nuovo repository nel proprio github personale

7. Si aggiunga il nuovo repository creato come **remote** e si elenchino i remote

PS C:\Users\matti\OOP-git-merge-conflict-test> git remote add mine https://github.com/matti-vita/61-git-remotes-merge-conflict.git
PS C:\Users\matti\OOP-git-merge-conflict-test> git remote -v
mine    https://github.com/matti-vita/61-git-remotes-merge-conflict.git (fetch)
mine    https://github.com/matti-vita/61-git-remotes-merge-conflict.git (push)
origin  https://github.com/APICe-at-DISI/OOP-git-merge-conflict-test.git (fetch)
origin  https://github.com/APICe-at-DISI/OOP-git-merge-conflict-test.git (push)

8. Si faccia push del branch `master` sul proprio repository
9. Si setti il branch remoto `master` del nuovo repository come *upstream* per il proprio branch `master` locale

PS C:\Users\matti\OOP-git-merge-conflict-test> git push -u mine master
Enumerating objects: 27, done.
Counting objects: 100% (27/27), done.
Delta compression using up to 8 threads
Compressing objects: 100% (19/19), done.
Writing objects: 100% (27/27), 3.86 KiB | 3.86 MiB/s, done.
Total 27 (delta 6), reused 24 (delta 6), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (6/6), done.
To https://github.com/matti-vita/61-git-remotes-merge-conflict.git
 * [new branch]      master -> master
branch 'master' set up to track 'mine/master'.