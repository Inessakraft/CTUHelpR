
<!-- README.md is generated from README.Rmd. Please edit that file -->


# CTUHelpR ![travis](https://api.travis-ci.com/CTU-Basel/CTUHelpR.svg?branch=master) [![codecov](https://codecov.io/github/CTU-Basel/CTUHelpR/branch/master/graphs/badge.svg)](https://codecov.io/github/CTU-Basel/CTUHelpR) [![](https://img.shields.io/badge/dev%20version-0.0.2-blue.svg)](https://github.com/CTU-Basel/CTUHelpR) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/CTU-Basel/CTUHelpR?branch=master&svg=true)](https://ci.appveyor.com/project/CTU-Basel/CTUHelpR)

## Installing from github with devtools


```r
devtools::install_github("CTU-Basel/CTUHelpR")
```

## Basic usage
Load the package

```r
# load the package
library(CTUHelpR)
# internal file of the package
path <- system.file("exdata", "file.txt",
                    package = "CTUHelpR")
# print it
print_file_content(file_path = path)
```

```
## Hello world!
```

## For contributors
### Testing with devtools


```r
# run tests, this assumes you are one directory up from the CTUHelpR dir
devtools::test("CTUHelpR")
# spell check
# ignore words character vector allows to exclude technical terms in the check
ignore_words <- c()
devtools::spell_check("CTUHelpR", ignore = ignore_words)
```

### Linting with lintr


```r
# lint the package -> should be clean
library(lintr)
lint_package("CTUHelpR", linters = with_defaults(camel_case_linter = NULL,
                                                     object_usage_linter = NULL,
                                                     line_length_linter(125)))
```

### Building the vignette

```r
library(rmarkdown)
render("vignettes/CTUHelpR-package-vignette.Rmd",
       output_format=c("pdf_document"))
```

### Generating the README file

The README file contains both standard text and interpreted R code.
It must therefore be compiled. Changes should be made in the `README.Rmd`
file and the file "knited" with R. This is easiest with RStudio, but other
methods are available.


```r
library(knitr)
knit("README.Rmd")
```

### Building the `pkgdown` site

```r
library(pkgdown)
build_site()
```

### Handling dependencies

Dependencies to other R packages are to be declared in the `DESCRIPTION` file under `Imports:` and in
the specific `roxygen2` documentation of the functions relying on the dependency. It is suggested to
be as explicit as possible. i.e. Just import functions that are needed and not entire packages.

Example to import `str_match` `str_length` `str_wrap` from the `stringr` package:

```r
#' @importFrom stringr str_match str_length str_wrap
```

### Preparing a release on CRAN

```bash
# build the package archive
R CMD build CTUHelpR
# check the archive (should return "Status: OK", no WARNINGs, no NOTEs)
# in this example for version 0.0.1
R CMD check CTUHelpR_0.0.1.tar.gz
```

### Guidelines for contributors

Requests for new features and bug fixes should first be documented as an
[Issue](https://github.com/) on GitHub.
Subsequently, in order to contribute to this R package you should fork the main repository.
After you have made your changes please run the 
[tests](README.md#testing-with-devtools)
and 
[lint](README.md#linting-with-lintr) your code as 
indicated above. Please also increment the version number and recompile the
`README.md` to increment the dev-version badge (requires installing the
package after editing the `DESCRIPTION` file). If all tests pass and linting
confirms that your coding style conforms you can send a pull request (PR).
Changes should also be mentioned in the `NEWS` file. A test has been implemented
to remind you to make these changes (see [here](tests/testthat/test-version_diff.R)).
The PR should have a description to help the reviewer understand what has been 
added/changed. New functionalities must be thoroughly documented, have examples 
and should be accompanied by at least one [test](tests/testthat/) to ensure long term 
robustness. The PR will only be reviewed if all travis and AppVeyor checks are successful. 
The person sending the PR should not be the one merging it.
