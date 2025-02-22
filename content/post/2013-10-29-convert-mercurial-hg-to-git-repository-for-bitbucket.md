+++
title = "Convert mercurial (hg) to git repository for bitbucket"
slug = "2013-10-29-convert-mercurial-hg-to-git-repository-for-bitbucket"
published = 2013-10-29T01:53:00.002000-07:00
author = "Pandurang Patil"
tags = [ "bitbucket", "mercurial", "git",]
+++
To convert `hg` repository on bitbucket to `git` repository follow below steps.
  

-   Create new repository with Repository Type selected as `Git`
-   follow below commands with the assumption that you already have `hg` repository cloned on your system. If not then you first need to clone existing `hg` repository. 

Steps to follow  

    $ git clone git://repo.or.cz/fast-export.git  
    $ mkdir <new git repo>  
    $ cd <new git repo>  
    $ git init  
    $ ../fast-export/hg-fast-export.sh -r <path to hg local repository>  
    $ git checkout HEAD  
    $ git remote add origin https://<username>@bitbucket.org/<username>/<new git repo>.git or if you are going to use ssh authentication to push   
    $ git remote add origin git@bitbucket.org:<username>/<new git repo>.git  
    $ git push origin master  

This will convert your `hg` repository to `git` repository and it also maintains the commit history inside `git` repository. 
