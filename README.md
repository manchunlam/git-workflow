# git Workflow

This is a sandbox project to visualize various use-cases in our git workflow

## Table of Contents
1. [Golden Rules](#i-golden-rules)
2. [Roles](#ii-roles)
3. [Use Cases](#iii-use-cases)
    1. [Make a Fix for Production](#a-make-a-fix-for-production-code)
        1. [Prepare a Hotfix](#1-prepare-a-hotfix)
        2. [Finish a Hotfix](#2-finish-a-hotfix)
    2. [Make a Feature](#b-make-a-feature)
        1. [Prepare a Feature](#1-prepare-a-feature)
        2. [Finish a Feature](#2-finish-a-feature)
    3. [Making a Release](#c-making-a-release)
        1. [Prepare for a Release](#1-prepare-for-a-release)
        2. [Finish a Release](#2-finish-the-release)
        3. [After the Release](#3-after-the-release)

## I. Golden Rules

Thy shall follow these rules, no exception.

5. All **manual merges** must use **`--no-ff`**
  To make sure your branches are **up-to-date before merge**, please do

    ```sh
    git fetch origin && git reset --hard origin/$branch-name
    ```

1. `feature` branches
    1. Branch off of `develop`, and

    2. Pull-requests (PR) back into `develop`
2. `hotfix` branches
    1. Branch off of `master`, and

    2. PR back into `master`
3. `release` branches
    1. Branch off of **`develop`**

    2. **Manual merge into `master`**

    3. **After** release, **manual merge** `master` **into** `develop`
4. All other branches
    1. **Where you branch off of, is where you will PR back to.**

## II. Roles

This document assumes each team have at least 2 roles

1. _Developer_
    * Anyone who code
    * Can only use Pull Request to get code into project
2. _Maintainer_
    * Allowed to use **manual merge** to get code into project
    * He/She is fully accountable for any merge conflicts

## III. Use Cases

### A. Make a Fix for Production Code

#### 1. Prepare a Hotfix

This stage uses Pull Request.

1. Branch off of `master`
2. Name the branch "$initials/fix-$what" (e.g. `jl/fix-like-module`)
3. After coding, deploy **personal fix-branch** to staging for QA
4. If QA oks it, rebase `fix-branch` onto `master`
5. Open PR from `fix-branch` to `master`

#### 2. Finish a Hotfix

This stage uses **manual merge**

For the Maintainer

1. Get both `master`, and `develop`
2. Perform a manual, `--no-ff` merge from `master` **into** `develop`

### B. Make a Feature

#### 1. Prepare a Feature

This stage uses Pull Request.

1. Branch off of `develop`
2. Name the branch "$feature-description" (e.g.  `super-awesome-module`)
3. After coding, deploy **feature-branch** to staging for QA
4. If QA oks it, **and Product wants it in the next release**,
    1. Rebase `feature-branch` onto `develop`
    2. Open PR from `feature-branch` onto `develop`

If there are more than 1 developer working on the same feature,

1. Follow Step 1, and 2 above
2. Every developer makes his/her own **personal** feature branch by branching off of
  "$feature-description"
3. Name your own branch "$initials/$feature-description" (e.g.
  `jl/super-awesome-module`)
4. Use PR to get your own branch into main feature-branch
5. Rebase your personal branch onto feature-branch **often** to get other
  developers' progress

#### 2. Finish a Feature

This stage uses a Pull Request.

For the Maintainer

1. Rebase `feature-branch` onto `develop`
2. **Only** the main feature-branch gets a PR to `develop`

### C. Making a Release

#### 1. Prepare for a Release

This stage uses Pull Request.

When it's time for a release,

1. Branch off of `develop`
2. Name the branch `release-$version` (e.g. `release-3.0.7`)
    * [Semantic versioning](http://semver.org/spec/v2.0.0.html) is **strongly**
      encouraged
3. Deploy release-branch to staging for QA to test
4. If QA finds any issues, developers will **branch off of release-branch** to
work on a fix
5. These before-release-fixes will **PR back into release-branch**
6. Repeat Step 4, and 5, until QA is happy

#### 2. Finish the Release

The stage uses **manual merge**

For the Maintainer

1. Get both `master`, and `release-branch`
2. Perform a manual, `--no-ff` merge from `release-branch` **into** `master`

#### 3. **After** the Release

This stage uses **manual merge**

For the Maintainer

1. Get both `master`, and `develop`
2. Perform a manual, `--no-ff` merge from `master` **into `develop`**
