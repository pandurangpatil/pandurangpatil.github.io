+++
title = "Convert mercurial (hg) to git repository for bitbucket"
slug = "2013-10-29-convert-mercurial-hg-to-git-repository-for-bitbucket"
published = 2013-10-29T01:53:00.002000-07:00
author = "Pandurang Patil"
tags = [ "bitbucket", "mercurial", "git",]
+++
<span
style="font-family: &quot;Helvetica Neue&quot;, Arial, Helvetica, sans-serif;">To
convert hg repository on bitbucket to git repository follow below
steps.</span>  
  

-   <span
    style="font-family: &quot;Helvetica Neue&quot;, Arial, Helvetica, sans-serif;">Create
    new repository with Repository Type selected as Git</span>
-   <span
    style="font-family: &quot;Helvetica Neue&quot;, Arial, Helvetica, sans-serif;">follow
    below commands with the assumption that you already have hg
    repository cloned on your system. If not then you first need to
    clone existing hg repository. </span>

Steps to follow  

    1:  $ git clone git://repo.or.cz/fast-export.git  
    2:  $ mkdir <new git repo>  
    3:  $ cd <new git repo>  
    4:  $ git init  
    5:  $ ../fast-export/hg-fast-export.sh -r <path to hg local repository>  
    6:  $ git checkout HEAD  
    7:  $ git remote add origin https://<username>@bitbucket.org/<username>/<new git repo>.git  
    8:  or if you are going to use ssh authentication to push   
    9:  $ git remote add origin git@bitbucket.org:<username>/<new git repo>.git  
    10:  $ git push origin master  

  
<span
style="font-family: &quot;Helvetica Neue&quot;, Arial, Helvetica, sans-serif;">This
will convert your hg repository to git repository and it also maintains
the commit history inside git repository. </span>
