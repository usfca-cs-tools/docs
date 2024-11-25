# Code Review Process

## Prerequisites

You should already be familiar with [git basics](git-basics.md) and [git next ste[s](git-next-steps.md)

## Introduction

1. We will use a code review process where instructors and/or TAs will periodically review your code and make suggestions.
1. It's really important to develop a clean and organized style of coding so you'll be ready to work on a long-lived codebase with large teams of programmers.
1. In commercial software development, a lot of effort is spent helping junior developers learn how to make their contributions fit into the style and architecture of a larger system.

## Before the Code Review

1. Your instructor will guide you to do your work on either the `main` branch or the `dev` branch. 
1. Before the code review, you should create a dedicated branch for suggestions made during the code review. You may wish to name the branch `project02-code-review` or something similar.

## During the Code Review

1. During the code review meeting, the reviewer (instructor or TA) will ask you to talk through key aspects of the assignment. As you do that, the reviewer will file "issues" (bug reports) on pieces of the code which should be improved.
1. Issues may be small, like improving naming, or large, like improving the design for extensiblity.

## After the Code Review

1. You will switch your local repo to the code review branch and look over the issues filed by the reviewer.
1. For each issue, make changes to the source code (potentially multiple files) to fix that issue. Then commit the changes for that issue with an explanatory commit message like "fix #1 by freeing memory when I'm done with it"
1. When you're done with issues, create a Pull Request to merge your changes from the code review branch on to your working branch (`main` or `dev`)
1. The PR should be assigned to you, but list the instructor or TA you met with as Reviewer.
1. The reviewer will review your changes to ensure that the issues are fixed and either approve the review or request changes. 
1. After the review is approved, you may merge the PR onto your working branch, which will automatically close the issues named in the commit messages. The reviewer will update Canvas with your grade.