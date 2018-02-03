# Git

This repository should be forked as part of the collaborative Git exercises.

## Overview

This focuses on slightly-more-advanced-than-an-introduction features of git. If
you're new to git, consider checking out our
[intoduction presentation](https://jmunixusers.github.io/presentations/Git) and
then come back and give this a try!

The examples and situations are specifically arranged to result in certain
issues that will naturally come up in collaborative environments. Please avoid
working ahead to prevent troubleshooting issues at unexpected times.

## Teams

For this activity, find a person nearby who you can work with. Ideally, you
will want to be in teams of two; however, teams of 3 will probably work out
fine. Assign a number (1..n where n is the number of people on the team) to
each person on your team. All futher instructions will assume teams of 2, but
can be easily adjusted.

## Forking

Person 1 from each team needs to fork the upstream
[UUG repo](https://github.com/jmunixusers/git-201). To fork a repository,
click the "Fork" button in the upper-right corner of the page. If prompted,
fork the repository to your personal GitHub account. 

Person 1 should add all others as collaborators on the repository. On the
GitHub website for Person 1's fork, Person 1 should go to Settings, then
Collaborators, then add all other team members as collaborators. The other
team members should accept the invite.

## Cloning

To clone the repository, run `git clone https://github.com/$USERNAME/git-201`.
Replace `$USERNAME` with Person 1's GitHub username. Then type `cd git-201`.

## Set up

If you haven't done this at some point in the past, run the following two
commands

    git config --global user.name "$YOURNAME"
    git config --global user.email "$EMAILADDRESS"

Replace `$YOURNAME` with your first and last name and `$EMAILADDRESS` with the
email address you used to sign up for GitHub. Leave the quotation marks in.

## Background

The year is 1609 and Shakespeare has just written his Sonnet #18. He is about
to publish it; however, he got his copy of Microsoft Word from TPB and instead
of having malware added, it simply has the spell checker removed. Instead of
lecturing him on how he should have just used LibreOffice, you decide to lend
him a hand. Now because it's 1609 you don't have spellcheck either, so the
spelling errors will need to be corrected mostly one-at a time manually. Also
because it's 1609, there's a good chance you're illiterate, so not all of the
changes that will be made in this exercise are actually fixes.

Sonnet 18 can be found in the CHANGEME.txt file.

## Making the first fix

The first issue found is by Person 1 on Line 11. The apostrophe in "untrimm'd"
needs to be replaced with an "e". After saving the file, add the changes to
the stage with `git add CHANGEME.txt`. Once that is done, commit the changes
with `git commit`

### Writing a commit message

Much like there are style guides for code, commits have style guides as well.
The general style is an introductory line less than 50 characters written in 
the present imperative tense, which means that all commit messages should start
with something like

> Fix the spelling of untrimmed

And not

> I fixed the spelling of untrimmed

After writing a summary, you can continue to write paragraphs explaining the
details of your change. Each line should wrap at 72 characters and each
paragraph should be separated by a single line. For example, this commit might
get a commit message like:

> Fix the spelling of untrimmed
>
> Spelling is hard. It seemed like a good choice at first to replace
> vowels that we weren't sure about with apostrophes, but that adds a
> bunch of weird symbols to the text. Replace the symbols with actual
> letters.
>
> There are five vowels in the English alphabet. "E" seems like a good
> choice here.

Once you've got a good commit message and assuming git kindly dropped you in
vim to write the message, press the Esc key and then type ":wq" and press Enter.

### Pushing the commit

Now that the commit has been written, it's time to share it with the world.
Person 1, type `git push -u origin master`.

*Sidenote*: The `-u origin master` is only necessary the first time you push to
a repository. It tells git that you want to track the remote named origin and
the branch named master.

## A second fix

Person 2 can now fix the issue on line 9. It's very similar, again an apostrophe
needs to be replaced with the letter "E". Make the change in the file, add
the file to the stage with `git add CHANGEME.txt`, then `git commit`. Write a
commit message.

Now type `git push -u origin master`.

### How to fix the error

Git has now given Person 2 a fairly helpful error message. You can't push
because someone else (Person 1) has pushed changes that you don't have. There
are two ways to fix this. We can do either of:

* Merge the changes into your branch
* Rebase your changes atop the remote changes

Both merging and rebasing mean different things. Merging means that you take
two different histories of a project and smush them together and you get a
merge commit which represents all the changes from the alternate history.

Rebasing means that you take the known history and replay all the commits from
the alternate history on top of the known.

*In this example, Person 2 has the alternate history (not a real git word), and
the stuff on GitHub is the real history*

Here, we will rebase. Run the command `git pull --rebase`.

Now look at the output of `git log` and see that Person 2's change exists in
the log on top of Person 1's change. At this point, Person 2 should `git push`
and it should work successfully. Person 1 should now run `git pull` to get the
latest changes.

## More fixes!

Person 1 and 2 both notice different issues on line 14. Person 1 should change
"Death" to "death" and Person 2 should change "wander'st" to "wanders". Person
2 should commit and push their changes then Person 1 should attempt to do the
same. Person 1 will get an error when pushing, just like they did before. This
time, Person 1 should just do a `git pull` because it's easier to type.

### Merge conflicts

Person 1 should open CHANGEME.txt in their favorite text editor and look around
Line 14. It should look something like:

```
<<<<<<< HEAD
Nor shall death brag thou wander’st in his shade,
=======
Nor shall Death brag thou wanders in his shade,
>>>>>>> abunchoflettersandnumbershere
```

Person 1 should resolve this in any way that seems acceptable. It is important
to remove the lines that Git added. Make any modifications to the changed
line as necessary. In a real project, this merge conflict may span several
lines; just change the lines as needed and remove the ones with `>>>`,
`===`, and `<<<`.

After making the changes to the file, tell git that you're done resolving the
conflict by running `git add README.txt`. Then run `git merge --continue`.

Person 1 will now need to create a merge commit. Just leave the message as
the default. Person 1 should `git push` and Person 2 should `git pull`.

## Branching

Clearly this whole mess of every person having to communicate every single
change they want to push and making everyone else `git pull`. This can be
minimized with using branches. Generally branches that are made for the purpose
of fixing a particular issue are referred to as topic branches.

`git checkout` is a tool to switch between branches and when passed the `-b`
flag, it will create the branch if it doesn't exist.

We will play around with these and how to turn them into Pull Requests.
