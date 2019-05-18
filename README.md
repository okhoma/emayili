
<!-- README.md is generated from README.Rmd. Please edit that file -->

# emayili <img src="man/figures/emayili-hex.png" align="right" alt="" width="120" />

[![Travis-CI build
status](https://travis-ci.org/datawookie/emayili.svg?branch=master)](https://travis-ci.org/datawookie/emayili)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
[![Codecov test
coverage](https://img.shields.io/codecov/c/github/datawookie/emayili.svg)](https://codecov.io/github/datawookie/emayili)

emayili is a package for sending emails from R. The design goals are:

  - works on all manner of SMTP servers and
  - has minimal dependencies (or dependencies which are easily
    satisfied).

The package name is an adaption of the Zulu word for email, emayili.

## Installation

At the moment you need to install a specific branch of the `{curl}`
package.

``` r
devtools::install_github("jeroen/curl", ref = "smtp")
```

Then install `{emayili}`.

``` r
devtools::install_github("datawookie/emayili")
```

## Usage

First create a message object.

``` r
library(emayili)
library(dplyr)

email <- envelope()
```

Add addresses for the sender and recipient.

``` r
email <- email %>%
  from("alice@yahoo.com") %>%
  to("bob@google.com") %>%
  cc("craig@google.com")
```

Add a subject.

``` r
email <- email() %>% subject("This is a plain text message!")
```

Add a body.

``` r
email <- email() %>% body("Hello!")
```

Add an attachment.

``` r
email <- email() %>% attachment("image.jpg")
```

Create a SMTP server object and send the message.

``` r
smtp <- server(host = "smtp.gmail.com",
               port = 465,
               username = "bob@gmail.com",
               password = "bd40ef6d4a9413de9c1318a65cbae5d7")
smtp(email, verbose = TRUE)
```

## Similar Packages

There are a selection of other R packages which also send
    emails:

  - [blastula](https://cran.r-project.org/web/packages/blastula/index.html)
  - [blatr](https://cran.r-project.org/web/packages/blatr/index.html)
    (Windows)
  - [gmailr](https://cran.r-project.org/web/packages/gmailr/index.html)
  - [mail](https://cran.r-project.org/web/packages/mail/index.html)
  - [mailR](https://cran.r-project.org/web/packages/mailR/index.html)
  - [sendmailR](https://cran.r-project.org/web/packages/sendmailR/index.html)
