# M01 Write-Up — Dev Environment, Git & GitHub

> Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort
> could follow your path on their own.

## What I built

I created a public GitHub repository, [node-js-training-implementation](https://github.com/johnmartin-marasigan/node-js-training-implementation), to complete Module 1 of the Node.js training program.

I configured my development environment using Visual Studio Code, Git, Homebrew, nvm, Node.js 24, and Bruno.

The repository contains:

- .nvmrc — pins the project's Node.js major version to 24.
- .gitignore — excludes dependencies, environment files, local databases, generated Prisma client files, build outputs, and coverage reports.
- .env.example — provides sample environment configuration without exposing secrets.
- hello-node.js — a basic JavaScript script that prints Hello, Node.js! to the terminal.

I implemented these changes on the feat/m01-hello-node feature branch rather than committing directly to main.

The changes were organized into three Conventional Commits:

1. chore: configure Node.js 24 version
2. chore: add Git ignore rules and environment template
3. feat: add hello-node script

I verified the Node.js installation and successfully executed the script using node hello-node.js.

I published the feature branch to GitHub using GitHub Desktop.

Pull Request: https://github.com/johnmartin-marasigan/node-js-training-implementation/pull/1

Peer review, merge-conflict resolution, and final merge: Pending.

## Why it's built this way (key decisions)

Branch and commit structure

I created the feat/m01-hello-node feature branch to keep development changes separate from main. This follows the GitHub Flow approach, where changes are developed on a dedicated branch, reviewed through a Pull Request, and merged after approval.

I organized the implementation into three Conventional Commits, separating environment configuration, project configuration, and the Node.js script.

This approach makes the commit history easier to understand because each commit represents a specific change. It also helps reviewers identify what was introduced at each stage.

Public repository vs. private repository

I used a public GitHub repository because it is the convention established by the training program.

If the repository were private and followed a no-direct-push rule, the development process would still use feature branches and Pull Requests. However, repository access would need to be granted to the appropriate collaborators, and changes to main would need to follow the team's review and merge restrictions.

Merge-conflict resolution

Deferred per trainer instruction, as no partner has been assigned.

## How to build it (teach it to the next trainee)

### 1. Prepare the development environment

Install Visual Studio Code, Git, a Node.js version manager such as nvm, and Bruno.

Use the version manager to install the Node.js version required by the training program. Create a `.nvmrc` file in the project root to ensure the project uses a consistent Node.js version.

Verify the environment:

```bash
node --version
npm --version
git --version
```

### 2. Initialize the repository

Create a public GitHub repository and initialize Git locally.

```bash
git init -b main
git remote add origin <repository-url>
```

The remote connects the local repository to GitHub, allowing branches and commits to be shared.

Create an initial README and commit it before beginning feature development.

### 3. Create a feature branch

Instead of developing directly on `main`, create a dedicated branch:

```bash
git switch -c feat/m01-hello-node
```

A feature branch isolates changes until they are ready for review and integration.

### 4. Implement and commit changes

Create the following files:

- `.nvmrc` — specify the Node.js version.
- `.gitignore` — exclude dependencies, secrets, generated files, databases, build outputs, and coverage reports.
- `.env.example` — provide sample environment variables.
- `hello-node.js` — print `Hello, Node.js!` to the terminal.

Verify the script:

```bash
node hello-node.js
```

Use `git status` and `git diff` to inspect changes before staging and committing them.

Organize changes into meaningful Conventional Commits rather than placing everything into one commit.

For example:

```text
chore: configure Node.js 24 version
chore: add Git ignore rules and environment template
feat: add hello-node script
```

This creates a readable history and helps reviewers understand each change independently.

### 5. Publish the feature branch

Push the branch to GitHub:

```bash
git push -u origin feat/m01-hello-node
```

Alternatively, publish the branch using GitHub Desktop.

In my case, I used GitHub Desktop because it handled GitHub authentication without requiring me to configure terminal authentication separately.

### 6. Open a Pull Request

On GitHub, open a Pull Request with:

- Base branch: `main`
- Compare branch: `feat/m01-hello-node`

Provide a descriptive title and summarize the changes and verification performed.

Review the changed files before submitting the Pull Request.

A Pull Request allows collaborators to inspect and discuss changes before integrating them into the main branch.

### 7. Request peer review

*Deferred per trainer instruction, as no partner has been assigned.*

### 8. Create and resolve a merge conflict

*Deferred per trainer instruction, as no partner has been assigned.*

### 9. Merge the Pull Request

*Pending — document the actual merge method, final verification, and merged Pull Request URL.*

Before merging, confirm that the Pull Request contains at least three Conventional Commits and follow the trainer's instructions regarding peer review and conflict resolution.

## Concepts worth explaining

### 1. Working tree, staging area, and commits

Git uses three important stages when tracking changes to a project.

- **Working tree:** This is where I create, modify, or delete files. Changes here are not automatically included in a commit.
- **Staging area:** This is where I select which changes should be included in my next commit using `git add`.
- **Commit:** This records a snapshot of the staged changes in the repository's history.

For example, when I created `hello-node.js`, the file initially existed in my working tree. I used `git add` to stage it and `git commit` to record the change.

This separation is useful because I can review my changes and decide exactly what belongs in each commit instead of committing everything at once.

### 2. `git revert` vs. `git reset`

Both commands can undo changes, but they work differently.

**`git revert`** creates a new commit that reverses the changes introduced by an earlier commit. It preserves the existing commit history, making it generally safer when undoing changes that have already been shared with other developers.

**`git reset`** moves the current branch's HEAD to a specified commit. Depending on the option used, it can also affect the staging area and working tree.

The three common reset options are:

- `--soft`: Moves HEAD while keeping the changes staged.
- `--mixed`: Moves HEAD and unstages the changes while keeping them in the working tree.
- `--hard`: Moves HEAD and resets both the staging area and working tree to match the target commit, potentially discarding uncommitted changes.

**When to use each:**

I would use `git revert` when I need to undo a commit that has already been pushed and shared because it preserves the history other developers rely on.

I would consider `git reset` when correcting my own local commits before sharing them, especially when I want to reorganize or redo my changes.

The key difference is that **`revert` preserves history by adding a new commit, while `reset` moves the branch's history pointer**.

## What tripped me up

### 1. Configuring nvm and Node.js

During the initial environment setup, I encountered configuration issues with nvm and npm.

One issue involved an npm `prefix` setting in `.npmrc`, which conflicted with nvm's version management.

I learned how nvm manages Node.js installations and how shell configuration files such as `.zprofile` and `.zshrc` affect the terminal environment.

After resolving the configuration issue, I successfully activated Node.js 24 using nvm.

### 2. Understanding Git remotes

While configuring the GitHub repository, I initially added an unnecessary `upstream` remote pointing to the original training repository.

I learned that `origin` typically refers to the remote repository used for my own work, while `upstream` is commonly used to reference the original repository when working with forks.

Since my implementation repository is independent, I removed the unnecessary `upstream` remote.

This helped me better understand how local repositories connect to remote repositories.

### 3. GitHub authentication when pushing changes

When I attempted to push my feature branch through the terminal, Git requested GitHub credentials.

Rather than continuing with password-based authentication, I used GitHub Desktop to publish the branch successfully.

I learned that GitHub supports different authentication methods, including credential managers, SSH, and GitHub CLI.

### 4. Understanding Git's working tree and staging area

Initially, I needed more practice understanding how Git handles modified, staged, and committed changes.

I practiced commands such as `git status`, `git diff`, `git restore`, and `git stash` to understand how changes move through the Git workflow.

The stash exercise helped me understand how to temporarily set aside uncommitted changes and restore them later without creating a commit.

### 5. Merge-conflict resolution

*Deferred per trainer instruction, as no partner has been assigned.*

## Checkpoint evidence

### 1. GitHub repository and Pull Request

**Repository:** [node-js-training-implementation](https://github.com/johnmartin-marasigan/node-js-training-implementation)

**Feature branch:** `feat/m01-hello-node`

**Pull Request:** https://github.com/johnmartin-marasigan/node-js-training-implementation/pull/1

**Merge status:** Pending final merge; peer review and merge-conflict exercise deferred per trainer instruction.

The feature branch contains three Conventional Commits:

| Commit | Description |
|---|---|
| `6f34b4f` | `chore: configure Node.js 24 version` |
| `628bef3` | `chore: add Git ignore rules and environment template` |
| `0c13774` | `feat: add hello-node script` |

### 2. Project configuration files

**`.gitignore`**

The file excludes dependencies, environment files, local databases, generated Prisma client files, build outputs, and coverage reports.

**`.env.example`**

The file provides sample configuration values:

```dotenv
NODE_ENV=development
PORT=3000
```

This demonstrates how environment configuration can be shared without committing actual secrets.

### 3. Node.js verification

The project uses Node.js 24, specified in `.nvmrc`.

I successfully executed:

```bash
node hello-node.js
```

Expected output:

```text
Hello, Node.js!
```

### 4. Git revert vs. reset explanation

`git revert` creates a new commit that reverses an earlier commit while preserving the existing history. It is generally the safer option when undoing changes that have already been shared with other developers.

`git reset` moves the current branch's HEAD to another commit. Depending on whether `--soft`, `--mixed`, or `--hard` is used, it can also change the staging area and working tree.

I would generally use `git revert` for shared commits and `git reset` when reorganizing my own local, unpublished commits.

### 5. Final checkpoint verification

The following evidence is still required before M01 can be marked complete:

- Peer review deferred per trainer instruction.
- Merge-conflict exercise deferred per trainer instruction.
- Merged Pull Request URL.
- Final confirmation that all Definition of Done requirements are satisfied.

## What I'd do differently

Pending final M01 review and completion.
