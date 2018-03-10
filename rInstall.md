---
title: 'R Installation'
---

## Install R on MS Windows: modify specification

ref: <http://statmath.wu.ac.at/software/R/qfin/>

### Installation

- Install the current version of R from <http://CRAN.R-project.org/bin/windows/base/>
- Install *Rtools* from <http://cran.at.r-project.org/bin/windows/Rtools/>

Suppose R is installed in the folder `d:/R`

### Change menu language as English
    
Edit file `d:/etc/Rconsole`, set the language as english: `language = english`

### set R mirror to ustc, set package directory
   
Edit file `d:/etc/Rprofile.site`, add the line below:

```r
# the added packages are installed in this path
.libPaths("e:/RLib")  
   
#  Modified the mirror and set rpubs
options(repos = c(CRAN = "http://mirrors.aliyun.com/CRAN",
                  CRANextra = "http://www.stats.ox.ac.uk/pub/RWin"),
        rpubs.upload.method = "internal",
        defaultPackages = c(getOption('defaultPackages'), 'tibble')
       )

#  change timezone
Sys.setenv(TZ='Asia/Shanghai')

# Add Welcome information
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

### set R mirror as ustc

```bash
    sudo gedit /etc/R/Rprofile.site
```

Add the following lines: 

```r
      options(repos = 'https://mirrors.ustc.edu.cn/CRAN', rpubs.upload.method = 'internal')
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

### Change timezone

```bash
sudo gedit /etc/R/Renviron.site
```

add this line:

```
TZ = 'Asia/Shanghai'
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

#### Install XML on ubuntu

```
sudo apt-get install libxml2 libxml2-dev
```

Then `install.packages('XML')`

#### Install RCurl on ubuntu
  
```bash
    sudo apt-get install libcurl4-openssl-dev
```

Then `install.packages('RCurl')`

Pls ref [RCurl FAQ](http://www.omegahat.org/RCurl/FAQ.html)

#### Install RQuantLib on ubuntu

On ubuntu terminal

```bash
    sudo apt-get install libquantlib0-dev
```

On R, `install.packages('RQuantLib')`

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

#### devtools

```bash
sudo apt-get install gfortran build-essential libxt-dev libcurl4-openssl-dev libxml++2.6-dev libssl-dev
```

```{r}
install.packages('devtools')
```
