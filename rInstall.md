---
title: 'R Installation'
---

## Install R on MS Windows: modify specification

Suppose R is installed in the folder `d:/R`

### Change menu language as english
    
Edit file `d:/etc/Rconsole`, set the language as english: `language = english`

### set R mirror to ustc, set package directory
   
Edit file `d:/etc/Rprofile.site`, add the line below:

```r
# the added packages are installed in this path
.libPaths("e:/RLib")  
   
#  Modified the mirror and set rpubs
options(repos = c(CRAN = "http://mirrors.aliyun.com/CRAN",
                  CRANextra = "http://www.stats.ox.ac.uk/pub/RWin"),
        rpubs.upload.method = "internal")
```

### Add Welcome information

Open file `d:/etc/Rprofile.site`, add the line below:

```r 
.First <- function(){
          cat("\nWelcome to R, Rho! It's", date(), ".\n Have a good day. \n\n")}
```

### package update

Whenever R's new version appear, remove the old one, install the latest one, and enter this command:

```r
    update.packages(lib.loc = "e:/Rlib", checkBuilt = TRUE, ask = FALSE)
```

## Install R on Ubuntu

```bash
  sudo apt-add-repository -y "deb http://mirrors.xmu.edu.cn/CRAN/bin/linux/ubuntu `lsb_release -cs`/"
  sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
  sudo apt-get update
  sudo apt-get install r-base-core r-base-dev r-base-html r-doc-html
```
### update R
Whenever there is a new R version, run the below on terminal:    
```bash
   sudo apt-get upgrade
```

### Set R default language as English

```bash
    sudo gedit /etc/R/Renviron
```
Add the line below:
LANGUAGE = 'en'

### set R mirror as aliyun

```bash
    sudo gedit /etc/R/Rprofile.site
```

Add the following lines: 

```r
      options(repos = 'http://mirrors.xmu.edu.cn/CRAN', rpubs.upload.method = 'internal')
```

You can add any R command to this file, e.g.

```r
    .First <- function(){
          cat("\nWelcome to R, Rho! It's", date(), ".\n Have a good day. \n")}
```
              
### Set added packages installation path as "~/RLib":

```bash
     sudo gedit /etc/R/Renviron.site
```
Add the following line:

```r
    R_LIBS = ~/RLib
```
### knitr on ubuntu terminal:

```bash
     cd my/Path
     Rscript -e "require('knitr'); knit('myFile.rnw')"
     xelatex myFile
```

### Misc

#### Get R help on terminal:   
```bash
    R --help
```
#### Get R Path on terminal:   
```bash
    which R
```
#### Get R version information on terminal:   
```bash
    R --version
```

Packages for the CRAN repository are built on a Launchpad PPA called RutteR. It is possible to use the PPA itself, which includes a few more packages than the CRAN repository.

### RutteR PPA

```bash
sudo add-apt-repository ppa:marutter/rrutter
sudo apt-get update
```

#### Install RCurl on ubuntu: 
  
```bash
    sudo apt-get install r-cran-rcurl
```

Pls ref [RCurl FAQ](http://www.omegahat.org/RCurl/FAQ.html)

#### Install RQuantLib on ubuntu

```bash
    sudo apt-get install r-cran-rquantlib
```
On ubuntu 14.04 and R 3.1.1, failed.

#### Installing xlsx

1. Installing openjdk version 7

```bash
sudo apt-get install openjdk-7-*
```

The installation is properly registered by your system using

```bash
update-alternatives --config java
```

and choosing openjdk-7 as the default JVM.

2. Installing rjava

```bash
sudo R CMD javareconf
sudo apt-get install r-cran-rjava
```

3. Installing xlsx

```{r}
install.packages("xlsx")
```

To search R's package in *.deb* format, call to <http://launchpad.net>.
