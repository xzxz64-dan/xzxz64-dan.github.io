---
layout: default
---

# Command-Line Course

## Course Introduction

This page summarizes what I learned in the command-line course KIK-LG221. The course introduced practical tools for working with files, processing text, writing shell scripts, connecting to remote computers, using version control, and publishing a website with Jekyll and GitHub Pages.

The main skills I practised were:

* navigating and managing files from the command line;
* processing text and linguistic data with Unix tools;
* writing reusable shell scripts;
* managing software and Python environments;
* working with remote servers and Git repositories; and
* building and publishing a static website.

| Module | Main topic | Example tools |
| --- | --- | --- |
| 1 | Command-line environments and file management | `pwd`, `ls`, `cd`, `cp`, `mv`, `chmod` |
| 2 | Text and corpus processing | `iconv`, `tr`, `sort`, `uniq`, `sed` |
| 3 | Shell scripts and software environments | Bash, environment variables, `brew`, `pip`, `venv` |
| 4 | Processes, remote connections, and version control | `ps`, `kill`, `ssh`, `scp`, Git |
| Final module | Static websites and publishing | Jekyll, Bundler, GitHub Pages |

## Module 1: Introduction to Command-Line Environments

The first module introduced the command-line environment and the structure of a file system. I learned how to inspect the current directory, move between directories, create and remove files and folders, copy and rename files, download content, and read or edit text files. I also learned how file permissions control who can read, write, or execute a file.

![A timeline of operating systems](https://imgs.xkcd.com/comics/operating_systems.png)

*A humorous timeline of operating systems. Source: [xkcd #1508](https://xkcd.com/1508/).*

```bash
pwd
ls -la
mkdir practice
cd practice
touch notes.txt
cp notes.txt notes-copy.txt
mv notes-copy.txt renamed.txt
chmod u+rw renamed.txt
rm renamed.txt notes.txt
cd ..
rmdir practice
```

The commands above demonstrate a basic file-management workflow. `pwd` displays the current location, `ls -la` lists files including hidden files, and `mkdir` creates a directory. The `cp`, `mv`, and `rm` commands copy, rename, and remove files, while `chmod u+rw` gives the file owner read and write permissions.

**Reflection:** After this module, I became more comfortable navigating the file system without relying on a graphical file manager. Learning about permissions also helped me understand why access to a file or command can sometimes be denied.

## Module 2: Text Processing in Linux

The second module focused on processing text efficiently. I learned the differences between ASCII, Latin-1, and UTF-8, as well as how to convert character encodings and line-ending formats. I also practised inspecting files, counting their contents, changing letter case, sorting lines, removing duplicates, selecting columns, searching with regular expressions, and editing text with `sed`.

A few basic commands can be used to inspect and transform text files:

```bash
head -n 5 life_of_bee.txt
wc -l -w -m life_of_bee.txt
grep '^[A-Z]' sentence.txt
tr '[:upper:]' '[:lower:]' < life_of_bee.txt > life_of_bee.lower.txt
```

`head` prints the first five lines, while `wc` counts lines, words, and characters. `grep` selects lines that begin with an uppercase letter. The final command uses `tr` to convert uppercase letters to lowercase and `>` to save the output in a new file.

**Reflection:** This module showed me that simple Unix tools become much more powerful when they are connected with pipes. Producing a word-frequency list made the value of reproducible command-line workflows especially clear for linguistic data.

## Module 3: Shell Scripts and Software Environments

The third module introduced shell scripting and software installation. I learned how scripts receive command-line parameters, how `if` statements control execution, and how command substitution stores the output of a command. I also worked with environment variables, shell configuration files, Homebrew, `pip`, and isolated Python virtual environments.

```bash
#!/bin/bash

name=$1

if [ -z "$name" ]; then
  echo "Please give your name."
else
  echo "Hello $name"
fi
```

This simple script reads the first command-line argument from `$1`. The `if` statement checks whether the argument is empty. It prints an instruction when no name is provided and otherwise prints a greeting. The module also introduced environment variables, package installation, and Python virtual environments.

**Reflection:** Writing scripts helped me see how repeated command sequences can be turned into reusable and less error-prone tools. Virtual environments were also useful because they provide a clean way to manage project-specific Python dependencies.

## Module 4: Processes, Remote Connections, and Version Control

The fourth module covered process management, remote computers, and version control. I learned how to run a process in the background, find its process identifier, and stop it when necessary. I also practised connecting to a server with SSH and copying files between computers with `scp`.

```bash
python3 train_model.py > training.log 2>&1 &
jobs
ps aux | grep train_model.py
kill PID

ssh username@puhti.csc.fi
scp run_model.sh username@puhti.csc.fi:~/project/
```

The `&` starts the Python program as a background job, while `> training.log 2>&1` saves both normal output and errors in one log file. `ps` helps locate the PID and `kill` stops the selected process. The final two commands open a secure remote connection and copy a local file to the server.

I also used Git and GitHub to record and share changes:

```bash
git clone git@github.com:xzxz64-dan/cmdline-course.git
cd cmdline-course
git branch frequency-bee
git checkout frequency-bee
git add life_of_bee.freq
git commit -m "Add word frequency data"
git push -u origin frequency-bee
git checkout main
git merge frequency-bee
git revert COMMIT_ID
```

This workflow clones a repository, creates and checks out the `frequency-bee` branch, stages and commits a change, and publishes the branch to GitHub. The branch can then be merged into `main`, while `git revert` provides a safe way to undo an earlier commit without deleting the repository's history.

**Reflection:** Version control made experimentation safer because each meaningful change could be recorded and recovered. Branches were particularly useful for developing a feature separately before merging it into the main version of a project.

## Final Module: Jekyll and GitHub Pages

In the final module, I learned how Jekyll converts Markdown files into a static website. The `_config.yml` file stores site-wide settings, files in `_layouts` define the shared HTML structure, and Sass files control the visual style. GitHub Pages publishes the generated website from a GitHub repository, while Jekyll provides a much faster local preview during development.

```bash
bundle install
bundle exec jekyll serve

git branch cmdline-course
git checkout cmdline-course
git add cmdline_course.md
git commit -m "Add command-line course summary"
git push -u origin cmdline-course
```

`bundle install` installs the Ruby dependencies listed for the site. `bundle exec jekyll serve` builds the website and serves it locally, normally at `http://127.0.0.1:4000/`. The Git commands keep the new course page isolated on its own branch until it has been reviewed and is ready to merge.

**Reflection:** Building this website connected many skills from the course: terminal navigation, package management, Git branches, Markdown, and remote publishing. Previewing changes locally before pushing them to GitHub made the development process faster and reduced the risk of publishing a broken page.
