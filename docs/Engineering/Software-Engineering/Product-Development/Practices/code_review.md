# Code Review

<h3>Table of Contents</h3>
[TOC]

# The Code Reviewer’s Guide

Primary purpose of code review is - make sure that the overall code health of the code base is improving over time.

## The Standard of Code Review
- reviewers should favor approving a CL once it is in a state where it definitely improves the overall code health of the system being worked on, even if the CL isn’t perfect
- if a CL adds a feature that the reviewer doesn’t want in their system, then the reviewer can certainly deny approval even if the code is well-designed
- there is no such thing as “perfect” code—there is only better code
- Reviewers should not require the author to polish every tiny piece of a CL before granting approval. Rather, the reviewer should balance out the need to make forward progress compared to the importance of the changes they are suggesting
- Instead of seeking perfection, what a reviewer should seek is continuous improvement
- A CL that, as a whole, improves the maintainability, readability, and understandability of the system shouldn’t be delayed for days or weeks because it isn’t “perfect.
- Reviewers should always feel free to leave comments expressing that something could be better, but if it’s not very important, prefix it with something like “Nit: “ to let the author know that it’s just a point of polish that they could choose to ignore.
- mentoring
    - share knowledge to imrove code health over time
- resolving conflicts
    - Don’t let a CL sit around because the author and the reviewer can’t come to an agreement.
    - discuss, meet
    - escalate
    - But, Don’t let a CL sit around because the author and the reviewer can’t come to an agreement.

## Best Pratices
1. Know What to Look for in a Code Review
2. Build and Test — Before Review
3. Don't Review Code for Longer Than 60 Minutes
4. Check No More Than 400 Lines at a Time
5. Give Feedback That Helps (Not Hurts)
6. Communicate Goals and Expectations
7. Include Everyone in the Code Review Process
8. Foster a Positive Culture
9. Automate to Save Time

## What to look for in a code review?
### Design
-The code is well-designed.

### Functionality
- The functionality is good for the users of the code.
- Any UI changes are sensible and look good.
- Any parallel programming is done safely.
### Complexity
- The code isn’t more complex than it needs to be. Neither in re-use not for read.
- The developer isn’t implementing things they might need in the future but don’t know they need now.

### Tests
- Code has appropriate unit tests.
- Tests are well-designed.

### Naming
- The developer used clear names for everything.

### Comments
- Comments are clear and useful, and mostly explain why instead of what.

### Style
- Code is appropriately documented.
- The code conforms to our style guides.

### Consistency
- Style wise

### Documentation
- If a CL changes how users build, test, interact with, or release code, check to see that it also updates associated documentation, including READMEs.

### Every Line

- look at every line of code that you have been assigned to review
- at least be sure that you understand what all the code is doing.

### Context
- look at the CL in a broad context

### Good Things
- If you see something nice in the CL, tell the developer, especially when they addressed one of your comments in a great way. 
- Code reviews often just focus on mistakes, but they should offer encouragement and appreciation for good practices, as well


## Navigating a CL in Review
## Speed of Code Reviews
## How to Write Code Review Comments
## Handling Pushback in Code Reviews

# The Change Author’s Guide

## Writing Good CL Descriptions
## Small CLs
## How to Handle Reviewer Comments


# Terminology

- CL: Stands for “changelist”, which means one self-contained change that has been submitted to version control or which is undergoing code review. Organizations often call this a “change”, “patch”, or “pull-request”.
- LGTM: Means “Looks Good to Me”. It is what a code reviewer says when approving a CL.

# References
- https://google.github.io/eng-practices/
- https://stackoverflow.blog/2019/09/30/how-to-make-good-code-reviews-better/
- https://www.perforce.com/blog/qac/9-best-practices-for-code-review
