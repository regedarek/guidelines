# Git styleguide

Read [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/).

[GitHub's Pull Requests](https://help.github.com/articles/using-pull-requests) are good and should be used for larger features and fixes. Opening a Pull Request as soon as you start working on a feature or bug branch is good for code review and having an open discussion about the code.

## Workflow

When starting working on a new support branch (ex. a *feature*):

1. Pull down any changes from `origin`: `git pull origin master`
2. Checkout a new feature branch: `git checkout -b feature/<descriptive-but-short-name>`
3. After one commit, push the feature branch to the GitHub repo: `git push -u origin feature/<name>`
4. Visit the GitHub repo page and open a new Pull Request for the branch
5. Do code, commits and tests. Continually push to the GitHub repo and do discussions and code review
6. When ready, merge the changes into `master`. This should *ideally* be made by another team member
7. Rinse and repeat from 1.

Manual merge in terminal (instead of step 7 above):

1. When in `master`, merge the changes from the feature branch: `git merge --no-ff feature/<name>`
2. Delete the feature branch: `git branch -d feature/<name>`
3. Push: `git push origin master`

## Branch naming conventions

- Feature branch; `feature/<name>`
- Hotfix/bug branch; `fix/<name>`

## Commit messages

Read [A note about git commit messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).

- Short but descriptive, 50 characters or less
- Begin the message with a **action verb**:
	- Ex. `Fix bug where records would be stored twice`
	- Other examples of action verbs: `change, add, remove, improve`
- One should be able to understand the commit by reading the message
	- If not, you should have probably separated the commit into several
- Use [Markdown](https://daringfireball.net/projects/markdown/) in the commit message if needed
- Use present tense
- If the commit is related to a GitHub issue, please refer to the issue number in the message
	- Ex. `git commit -m "Fix #9 where records would be stored twice"`
	- GitHub will automatically link to the issue page from the message and close the issue (super cool)

You may split up the commit message with heading + body:

	Capitalized, short (50 chars or less) summary

	More detailed explanatory text, if necessary.  Wrap it to about 72
	characters or so.  In some contexts, the first line is treated as the
	subject of an email and the rest of the text as the body.  The blank
	line separating the summary from the body is critical (unless you omit
	the body entirely); tools like rebase can get confused if you run the
	two together.

