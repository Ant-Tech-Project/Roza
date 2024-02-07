# What is a `merge` conflict? 

A merge conflict is an event that occurs when `Git` is unable to automatically resolve differences in code between two commits.
When all the changes in the code occur on different lines or different files, `Git` will successfully merge commits without your help.

### What can cause a conflict?
When there are conflicting changes on the same lines, a **“merge conflict”** occurs because `Git` doesn’t know which
code to keep and which to discard.

**Conflicts can happen when:** 
- merging a branch
- rebasing a branch
- cherry picking a commit. 

If `Git` detects a conflict, it will highlight the conflicted area and ask you which code to keep.
Once you tell `Git` which code you want,
you can save the file and proceed with the `merge`, `rebase`, or `cherry-pick`.

# Strategies for conflict resolution

When faced with a merge conflict in Git, there are several strategies you can use to resolve the conflict and successfully complete the merge:

**Manual Resolution:**

* Open the conflicted files in your preferred text editor.
* Git will mark the conflicting sections with `<<<<<<<`, `=======`, and `>>>>>>>` markers, representing the conflicting changes from different branches.
* Manually edit the conflicted sections to keep the desired changes and remove the conflict markers.
* Save the changes.

**Using a Merge Tool:**

Git provides various merge tools that can help visualize and resolve conflicts more efficiently.

- VS Code Extensions: 

* `GitLens`
* `Git Graph`
* `Source Control`
* `Git History`

- Command line tools:
- `git mergetool`
- `git difftool`

- Graphical tools:  
* [GitKraken](https://www.gitkraken.com/)
* [Sourcetree](https://www.sourcetreeapp.com/)
* [Tower](https://www.git-tower.com/)


# Practice conflict resolution

I have created a new branch called `conflict-resolution` to practice resolving merge conflicts.

In  `main` branch I created a file:

```
resource "aws_instance" "example" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}

resource "compute" "configure" {
  provisioner "local-exec" {
    command = "./scripts/configure.sh" 
  }
}
```

---

```
git add main.tf
git commit -m "from main"
```

---

```
git switch conflict-resolution
#changed `main.tf` content 12th line `configure.sh` to script.sh
git add main.tf
git commit -m "changes from test branch"
```

---

```
git switch main
git merge conflict-resolution
```

And now we have a conflict. In order to resolve this conflict we need to open the file in our editor and edit the conflicted section or use a merge tools mentioned above.

# Step-by-step instruction for how to resolve a conflict

- Step 1: Identify the Conflict

When Git encounters conflicting changes during a merge operation, it halts the process and prompts you to resolve the conflict manually. The conflicted files will contain markers indicating the conflicting sections.

- Step 2: Open the Conflicted File

Locate the conflicted file in your project directory and open it in a text editor or a Git merge tool. The conflicted sections will be marked with "`<<<<<<<`", "`=======`", and ">>>>>>>", representing the changes from different branches.

- Step 3: Understand the Conflict

Carefully review the conflicting sections to understand the nature of the conflict. Identify the changes made in both branches and determine how to reconcile them.

- Step 4: Resolve the Conflict

Manually edit the conflicted sections in the file to incorporate the desired changes from both branches. Remove the conflict markers ("`<<<<<<<`", "`=======`", and "`>>>>>>>`") and ensure that the final result is syntactically correct and logically coherent.

- Step 5: Save the Changes

Once you've resolved the conflict, save the changes to the file in your text editor.

- Step 6: Stage the Resolved File

After saving the changes, stage the resolved file using the "git add" command. This indicates to Git that the conflict has been resolved and the file is ready to be committed.

- Step 7: Commit the Merge

Commit the resolved merge by running "git commit". Provide a meaningful commit message that describes the resolution of the conflict.

- Step 8: Verify the Resolution

After committing the merge, verify that the conflict has been successfully resolved by reviewing the changes in the file. Ensure that the final result incorporates the desired modifications from both branches.

- Step 9: Push the Changes

If you're working in a shared repository, push the resolved changes to the remote repository using "git push". This ensures that the conflict resolution is propagated to other team members.

- Step 10: Clean Up

Once the conflict is resolved and pushed to the remote repository, you can clean up any temporary files or branches created during the conflict resolution process.