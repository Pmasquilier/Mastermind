---
deck: Mastermind my memory::Web Tools::Git
---

## Adding a local repository to GitHub with GitHub CLI
<!-- basicblock-start oid="Obs988cpO8e8PG9THHVOOiIS" -->
**How to add a local repository to GitHub with GitHub CLI ?**::

1.  Initialize the local directory as a Git repository.
    
    ```shell
    git init -b main
    ```
    
2.  Stage and commit all the files in your project.
    
    ```shell
    git add . && git commit -m "initial commit"
    ```
    
3.  To create a repository for your project on GitHub, use the **`gh repo create`** subcommand. When prompted, select **Push an existing local repository to GitHub** and enter the desired name for your repository.
    
4.  Follow the interactive prompts. Alternatively, to skip all the prompts, supply the path to the repository with the `--source` flag and pass a visibility flag (`--public`, `--private`, or `--internal`). For example, `gh repo create --source=. --public`. Specify a remote with the `--remote` flag. To push your commits, pass the `--push` flag.
<!-- basicblock-end -->