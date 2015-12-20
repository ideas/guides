# Git Guide

A guide for programming within version control.

## Table of Contents

  - [Repository](#repository)
  - [Workflow](#workflow)
  - [Issues and Pull Requests](#issues-and-pull-requests)
  - [Resources](#resources)

## Repository

  - Don’t include files in source control that are specific to your development machine or process. Create a global .gitignore to ignore these files.

    ```sh
    touch ~/.gitignore_global
    git config --global core.excludesfile ~/.gitignore_global
    ```

  - Delete local and remote feature branches after merging.

    ```sh
    git push origin --delete <branch-name>
    ```

## Workflow

  - Fork the main repository and create feature branches on the copy.

    ```sh
    git checkout -b <branch-name>
    ```

  - Add the original repository as a remote and sync with it.

    ```sh
    git remote add upstream https://github.com/<original-owner>/<original-repository>.git
    ```

  - Use the [GitHub Flow](https://guides.github.com/introduction/flow/).

  - Write a [good commit message](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html). Here is a model:

    ```
    Capitalized, short (50 chars or less) summary

    More detailed explanatory text, if necessary.  Wrap it to about 72
    characters or so. In some contexts, the first line is treated as the
    subject of an email and the rest of the text as the body.  The blank
    line separating the summary from the body is critical (unless you omit
    the body entirely); tools like rebase can get confused if you run the
    two together.

    Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
    or "Fixes bug." This convention matches up with commit messages generated
    by commands like git merge and git revert.

    Further paragraphs come after blank lines.
    ```

  - Submit a pull request. In the description reference relevant issues with the [special keyword syntax](https://help.github.com/articles/closing-issues-via-commit-messages/) (eg. "Closes #0").

## Issues and Pull Requests

  - Use labels (`bug`, `duplicate`, `enhancement`, `help` `wanted`, `invalid`, `question`, or `wontfix`).

    Use the `blocker` label when the issue blocks a release.

    Use the `critical` label when the issue causes data loss, crashes or hangs processes, makes the application unresponsive, etc.

  - Use milestones.

    - Project with releases: Use a version number (eg. "3.2.1").

    - Project with no releases: Use either "Current" or "Backlog". "Current" contains issues to be worked on next, "Backlog" contains issues to be worked on later.

  - Assign issues to the person who has something to do with it. For example if you have an issue assigned to you and you ask a question in a comment, assign the issue to the person who is supposed to reply. After replying to the issue, it should be assigned back to you. In case of a pull request, assign it to the person who has the authority to merge it.

## Resources

  - https://help.github.com/articles/ignoring-files/#create-a-global-gitignore
  - https://help.github.com/articles/deleting-unused-branches/
  - https://help.github.com/articles/fork-a-repo/
  - https://help.github.com/articles/configuring-a-remote-for-a-fork/
  - https://help.github.com/articles/syncing-a-fork/
