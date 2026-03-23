# psychic-adventure : A repository showing 'git author', 'author', 'contributor', 'committer', and 'submitter' variations

This contains a few simple examples showing the authorship issue where 'author' has a very clear meaning in general and professional contexts, which is significantly different from the term 'author' ('git author') that 'git' uses.

## Core Issue

Within 'git', an 'author' is simply the person who contributed one or more files to the repostiory.  They may not have authored them, but by default they are listed as the author.  This 'contributor' can change the 'git author' to be someone else, but git does not enforce this and would have no idea if it was correct attribution or not.  Further, a 'git author' is limited to:

* People with emails — So all historic (pre-1960 or so) people can't be authors. The 'contributor' can make-up an email, but that is not properly attributing authorship and is a burden with unclear benefit.  Using a convention of the author with a 'historical.invalid' email address can help make it clear this person does not have an email
* People with unknown emails — If the contributor does not know the email, the person can't be an author.  The 'contributor' can make-up an email, but that is now counter-productive since it implies the person doesn't have a valid email.  Using 'unknown.invalid' may solve this.
* A single person — Only a single person can be made the 'git author'.  By convention, all additional authors are put within the message itself under a 'Co-authored-by:' prefix.  This could simply be used for the true author as well with a 'Authored-by: ' trailer in the message.  Or used for all authorship to clearly separate it from the 'contributor' aspect that is the core of the 'git author' concept.

## Summary

Given the full limits of the above, it is best to take the approach mentioned in the 'A single person' limitation above.  

* We should interpret the 'git author' by default as the no more than the 'contributor' of the change to git.  
* A 'committer' can put a contributed change (e.g. contributed by a git patch or through a pull request) into a repository different from the 'contributor', that the 'committer' has permission to do so.  
* Authors different from the 'contributor' should be attributed properly with the '--author' tag, potentially using a '.invalid' email address to provide details.
* All 'authorship' should be made clear in the commit message with an 'Authored-by:', 'Co-authored-by:', etc. trailer matching scholarly practices of attribution, if other attribution options are not satisfactory.  The author of the commit should be changed to 'in.message@detailed.invalid' or something similar.
* If 'authorship' is unspecified, it can be guessed that the 'contributor' is claiming sole authorship.  But the lack of attribution could just as well be from oversight.