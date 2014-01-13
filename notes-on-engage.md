# Notes on `Engage` Team Branching Practice

In addition to using the `git Workflow`, `Engage` team also has a very
interesting additional branching practice, the `acceptance branch`.

It's completely new to me. I'm writing this down, in the hopes that
it might be useful someday.

## The `acceptance branch`

* Consider the `acceptance branch` a kitchen sink. Anything that are
pull-requested into `develop` or `master`, **also** go into
`acceptance branch`.

* The `acceptance branch` is **never** merged or pull-requested into any other
branches.

* You are **not allowed** to branch off of the `acceptance branch`

* The purpose of the `acceptance branch` is for QA to test everything possible,
the minute they are ready. Also, as a rough estimate of how the fixes,
features **might** work together.
