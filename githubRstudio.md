---
title: 'github with rstudio on windows'
output: html_document
---

- register an account on [github](https://github.com), create a repository, say, tools
- download and install platform-specific version of git from [git-scm](http://git-scm.com/downloads)
- git configure: open the bash version of git and type:

```
git config --global user.name 'rhohz'
git config --global user.email 'rhozhanghz@gmail.com'
```

- generate ssh key: open git-gui, click help --> show ssh key, if not exist, generate one, and copy to clipboard.
- add ssh key to github: in github website, settings --> ssh keys --> add ssh key
- open rstudio and set the path to git executable: tools --> global options --> git/svn

![where is your git.exe file?](toolsFig/rstudioGitSet.png)

- version control in rstudio
      - in github website, copy the repository path (https://github.com/rhohz/tools)
	  - in rstudio, file --> new project --> version control -- git, paste repository path below 'repository url'
	  
- commit and push: 
      - right to git token, select 'commit' (or Ctrl + alt + M), check the files to commit, fill in something in commit message, and click commit
	  - click push, fill in uername and passward
- open an existed project: file --> open project
