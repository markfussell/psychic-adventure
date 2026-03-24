# Git 'author' confusion, specification, and proposed 'contributor' nomenclature 

This document describes a problem with the implications of 'git' using the term 'author' for someone who contributes file changes to a git repository.  It contains a description of the core issue, a suggested change to use clarifying terminology and approaches with git to clean up this 'author' issue, and examples of the different variations starting from common ('default') behavior to the suggested approaches.

## Core Issue

The crux of the issue: 'git' chose to use a term ('author') that has a very clear meaning in general and professional contexts.  But 'git' is using this well-defined term very differently from that general and professional meaning. 

Within 'git', an 'author' is simply the person who contributed one or more files to a repository.  They may not have authored them, but by default they are listed as the 'author' although they are really only known to be the 'contributor'.  This 'contributor' can change the 'git author' to be someone other than themselves, but git does not enforce this and would have no idea if it was correct attribution or not.  

Further, a 'git author' has technical limitations.  It can only be:

* People with emails — So all historic (pre-1960 or so) people can't be authors. The 'contributor' can fabricate an email, but that is not properly attributing authorship and is a burden with unclear benefit.  Using a convention of the author with an '@historical.invalid' email address can help make it clear this person does not have an email
* People with known emails — If the contributor does not know the email, the person can't be an author.  The 'contributor' can invent an email, but that is now counter-productive since it implies the person doesn't have a valid email.  Using an '@unknown.invalid' email may solve this.
* A single person — Only a single person can be made the 'git author'.  By convention, all additional authors are put within the trailing part of a commit message with a 'Co-authored-by:' prefix.  This could simply be used for the true author to augment that claim with an 'Authored-by:' section in the message with further details.  Or it could be used for all authorship to clearly separate it from the 'contributor' aspect that is the core of the 'git author' concept.  

## Suggested Approach

Given the full limits of the above, it is best to take the approach mentioned in the 'A single person' limitation above.  

* We should interpret the 'git author' as no more than the ***'contributor'*** of the change to git.  That is all it means semantically to git and conflating it with the common and professional term 'author' is misleading.
* A 'committer' can put a contributed change (e.g. contributed by a git patch or through a pull request) into a repository different from the 'contributor'.  This 'contributor' and 'committer' distinction is the essence of the functionality that git provides.    
* ***Authors*** different from the 'contributor' ***should be attributed properly by the 'contributor'*** with the '--author' tag, potentially using a '.invalid' email address to provide details about an author without a known-valid email.
* All 'authorship' should be made clear in the commit message with an 'Authored-by:', 'Co-authored-by:', etc. trailing annotation matching scholarly practices of attribution, if other attribution options are not satisfactory for clarity.  For example, if the contributor is truly the author, it should be part of the message to make that assertion clear.  If the authorship is more complex, the author of the commit should be changed to 'in.message@detailed.invalid' or something similar.
* If 'authorship' is unspecified, it can be guessed that the 'contributor' is claiming sole authorship.  But the lack of attribution could just as well be from oversight.  
* ***Git itself, makes no claim to who is the true 'author' of anything within it.***  It just enables the 'contributor' to specify authorship in multiple different ways, some of which are ambiguous and some of which are clear and precise.

## Examples: Gettysburg Address

All the following examples had exactly the same text

### V1: Default Git Behavior
Contributor is automatically 'git author'

The 'v1' version was committed with the following.
```bash
sh% git add gettysburg_address__bliss__v1.txt
sh% git commit -m "Bliss's Version of Gettysburg Address"
```

This produced the version available here:
* <https://github.com/markfussell/psychic-adventure/blame/a7ba58f0bf062d1c91b6ab50a391ccc8c5c3fe30/gettysburg_address__bliss__v1.txt>

Which has a blame that looks like this:
![image1.png](images%2Fimage1.png)

### V2: Git Author change
Contributor changes the contribution git-author as part of commit

The 'v2' version was committed with the following.
```bash
sh% git add gettysburg_address__bliss__v2.txt
sh% git commit -m "Bliss's Version of Gettysburg Address" 
   --author="Abraham Lincoln <abraham.lincoln@historical.invalid>" 
```

This produced the version available here:
* <https://github.com/markfussell/psychic-adventure/blame/efec82cc038920b6a07f346ef7c47a26c570bb78/gettysburg_address__bliss__v2.txt>

Which has a blame that looks like this:
![image2.png](images%2Fimage2.png)

### V3: Git Author and Message change

Contributor changes the contribution git-author to the main author and annotates the message with both Author and Provenance information 

The 'v3' version was committed with the following.
```bash
sh% git add gettysburg_address__bliss__v3.txt
sh% git commit  
   --author="Abraham Lincoln <abraham.lincoln@historical.invalid>" 
   -m "Bliss's Version of Gettysburg Address 
      Author: Abraham Lincoln • https://www.abrahamlincolnonline.org
      Provenance: Colonel Alexander Bliss
      "
```

This produced the version available here:
* <https://github.com/markfussell/psychic-adventure/blame/93468773801c31ead9cc436ee25901dbe00e4385/gettysburg_address__bliss__v3.txt>

Which has a blame that looks like this:
![image3.png](images%2Fimage3.png)

And commit details that look like this:
![image6.png](images%2Fimage6.png) 

### V3: Git Author and Message change: Detailed

Contributor changes the contribution git-author to 'In Message' and annotates the message with both Author and Provenance information

The 'v4' version was committed with the following.
```bash
sh% git add gettysburg_address__bliss__v4.txt
sh% git commit  
   --author="Detailed In Message <in.message@detailed.invalid>" 
   -m "Bliss's Version of Gettysburg Address 
      Author: Abraham Lincoln • https://www.abrahamlincolnonline.org
      Provenance: Colonel Alexander Bliss
      "
```

This produced the version available here:
* <https://github.com/markfussell/psychic-adventure/blame/dc32f539ec4ab6da94c622bc409ddf2349f76bc8/gettysburg_address__bliss__v4.txt>

Which has a blame that looks like this:
![image4.png](images%2Fimage4.png)

And commit details that look like this:
![image7.png](images%2Fimage7.png)  