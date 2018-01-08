# wrassp

[![Build Status](https://travis-ci.org/IPS-LMU/wrassp.svg?branch=master)](https://travis-ci.org/IPS-LMU/wrassp)
[![Coverage Status](https://coveralls.io/repos/IPS-LMU/wrassp/badge.svg)](https://coveralls.io/r/IPS-LMU/wrassp)
[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/wrassp)](http://cran.r-project.org/package=wrassp)

`wrassp` is a wrapper for R around Michel Scheffers's [libassp](http://libassp.sourceforge.net/)
(Advanced Speech Signal Processor). The libassp library aims at providing functionality for handling speech signal files in most common audio formats and for performing analyses common in phonetic science/speech science. This includes the calculation of formants, fundamental frequency, root mean square, auto correlation, a variety of spectral analyses, zero crossing rate, filtering etc. This wrapper provides R with a large subset of libassp's signal processing functions and provides them to the user in a (hopefully) user-friendly manner.

This package is part of the next iteration of the EMU Speech Database Management System which aims to be as close to an all-in-one solution for generating, manipulating, querying, analyzing and managing speech databases as possible. For an overview of the system please visit this URL: [http://ips-lmu.github.io/EMU.html](http://ips-lmu.github.io/EMU.html).

## Installation

* install the current [CRAN release](http://cran.r-project.org/package=wrassp):
```r
install.packages("wrassp")
```

* or install the latest development version from GitHub (as large parts of `wrassp` are written in `C` make sure your system fulfills the requirements for package development (see [here](http://www.rstudio.com/ide/docs/packages/prerequisites))):
```r
library(devtools)
install_github("IPS-LMU/wrassp", build_vignettes = TRUE)
```

## Quick start

* load the library: 
```r
library("wrassp")
```

* get path to an audio file: 
```r
path2wav <- list.files(system.file("extdata", package = "wrassp"), pattern = glob2rx("*.wav"), full.names = TRUE)[1]
```

* calculate formants from audio file: 
```r
res=forest(path2wav, toFile=FALSE)
```

* plot the first 100 F1 values over time: 
```r
plot(res$fm[1:100,1],type='l')
```

* for more information see the `An introduction to the wraspp package` vignette: 
```r
vignette('wrassp_intro')
```


## Available signal processing functions

+ `acfana()`: Analysis of short-term autocorrelation function
+ `afdiff()`: Computes the first difference of the signal
+ `affilter()`: Filters the audio signal (see docs for types)
+ `cepstrum()`: Short-term cepstral analysis
+ `cssSpectrum()`: Cepstral smoothed version of `dftSpectrum()`
+ `dftSpectrum()`: Short-term DFT spectral analysis
+ `forest()`: Formant estimation
+ `ksvF0()`: F0 analysis of the signal
+ `lpsSpectrum()`: Linear Predictive smoothed version of `dftSpectrum()`
+ `mhsF0()`: Pitch analysis of the speech signal using Michel's/Modified Harmonic Sieve algorithm
+ `rfcana()`: Linear Prediction analysis
+ `rmsana()`: Analysis of short-term Root Mean Square amplitude
+ `zcrana()`: Analysis of the averages of the short-term positive and negative zero-crossing rates

(see the respective R documentation for more details on all of these functions)

## Available file handling functions

+ `read.AsspDataObj()`: read an existing SSFF file into a `AsspDataObj` which is its in-memory equivalent.
+ `write.AsspDataObj()`: write a `AsspDataObj` out to a SSFF file.

## For Developers

### Checking on rocker/r-devel docker image (prerequisite docker is installed)

- pull current r-devel image: `docker pull rocker/r-devel`
- check if pull worked: `docker images`
- check R version in image: `docker run rocker/r-devel:latest R --version`
- run interactive version of R `docker run --rm -ti rocker/r-devel:latest`


## Authors

**Raphael Winkelmann**

+ [github](http://github.com/raphywink)

**Lasse Bombien**

+ [github](http://github.com/quabolasse)


**Affiliations**

[INSTITUTE OF PHONETICS AND SPEECH PROCESSING](http://www.en.phonetik.uni-muenchen.de/)
