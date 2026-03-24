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