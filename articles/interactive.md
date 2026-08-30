# Approach to Correcting Misspelt Local Government Areas

## Motivation

Nigeria has 774 Local Government Areas (LGAs). There are a number of
factors that can make working with them challenging:

1.  Some LGAs share the same name with their respective States
    e.g. Bauchi LGA in Bauchi State, and this can lead to wrong
    application of the data.
2.  Some LGAs bear the same name although they are in different States,
    e.g. Obi LGA in Benue and Nasarawa States.
3.  LGA spelling discrepancies are rife in the literature, and believe
    it or not, even in official government documents.

## A proposed solution

The function `fix_region` has methods that are designed to address
spelling errors LGAs[^1]. These fixes can be carried out in 3
incremental phases; if the user cannot effect the corrections at a
particular level s/he can proceed to the next stage. The phases are as
follows:

1.  Automatic
2.  Interactive
3.  Manual

#### 1. Automatic fixes

When the spelling error is slight and unambiguous, the function
automatically effects the repair. However, when there is only a single
misspelt LGA, and especially if it is supplied as a string, `fix_region`
will signal an error.

``` r

library(naijR)

fix_region("Legos Island")
#> Error in `fix_region()`:
#> ! Incorrect region name(s); consider reconstructing 'x' with `states()`
#>   or `lgas()` for a more reliable fix
```

The thinking is that an automated solution may not be necessary for a
single value that was probably provided interactively.

When another LGA is added, such that the argument passed to the function
is a character vector with more that one element:

``` r

fix_region(c("Legos Island", "Amuwo-Odofin"))
#> ℹ Successful fix(es):
#> -------------------
#> * Legos Island => Lagos Island
```

Sometimes when we use a character vector to perform this check, the
function `fix_region` may find it difficult to decide on what fixes to
apply. In such instances, the best thing is to convert the vector into
an `lgas` object.

``` r

chars <- c("Legos Island", "Amuwo Odofin")
fix_region(chars)
#> Error in `fix_region()`:
#> ! Incorrect region name(s); consider reconstructing 'x' with `states()`
#>   or `lgas()` for a more reliable fix

# Create an `lgas` object
lgs <- lgas(c("Legos Island", "Amuwo Odofin"))
#> Warning: One or more items is not an LGA. Spelling error?
fix_region(lgs)
#> ℹ Successful fix(es):
#> -------------------
#> * Amuwo Odofin => Amuwo-Odofin
#> * Legos Island => Lagos Island
#> [1] "Amuwo-Odofin" "Lagos Island"
#> attr(,"misspelt")
#> character(0)
#> attr(,"regions.fixed")
#>   Amuwo Odofin   Legos Island 
#> "Amuwo-Odofin" "Lagos Island"
```

Note that the constructor
[`lgas()`](https://docs.ropensci.org/naijR/reference/lgas.md), by
default, signals a warning when the vector we are supplying has misspelt
LGAs. However, to avoid the unnecessary verbosity whilst attempting the
fix, this warning is suppressed if
[`lgas()`](https://docs.ropensci.org/naijR/reference/lgas.md) is nested
in
[`fix_region()`](https://docs.ropensci.org/naijR/reference/fix_region.md).

``` r

fix_region(lgas(c("Legos Island", "Amuwo Odofin")))
#> ℹ Successful fix(es):
#> -------------------
#> * Amuwo Odofin => Amuwo-Odofin
#> * Legos Island => Lagos Island
#> [1] "Amuwo-Odofin" "Lagos Island"
#> attr(,"misspelt")
#> character(0)
#> attr(,"regions.fixed")
#>   Amuwo Odofin   Legos Island 
#> "Amuwo-Odofin" "Lagos Island"
```

When the spelling mistakes depart far from the available LGA spellings,
the user is shown a message stating what fixes could not be applied. To
now carry out a fix, one can proceed to the next stage.

``` r

fix_region(lgas(c("Orange County", "Amuwo Odofin")))
#> ℹ Successful fix(es):
#> -------------------
#> * Amuwo Odofin => Amuwo-Odofin
#> 
#> Fix(es) not applied:
#> --------------------
#> * Orange County
#> [1] "Amuwo-Odofin"  "Orange County"
#> attr(,"misspelt")
#> [1] "Orange County"
#> attr(,"regions.fixed")
#>   Amuwo Odofin 
#> "Amuwo-Odofin"
```

#### 2. Interactive fixes

When the automatic fix is not feasible, the user has the option of doing
it interactively by calling `fix_region` and setting its `interactive`
argument to `TRUE`. By following the prompts, the misspelt LGA as well
as possible replacements are presented. All the user needs to do is to
select the desired replacement value. This is particularly useful when
the user is not sure of what the correct spelling might be.

When a misspelt LGA has more than one match, the interactive approach is
the viable option for effecting fixes. In the example below, not all the
mispelt LGAs could be fixed automatically:

``` r

mispelt.adamawa <- c("Fufure", "Demsa", "Machika", "Fufure", "Ganye", "Hong")

# check for misspelt LGAs and, if necessary, attempt to fix
length(mispelt.adamawa)
#> [1] 6
sum(is_lga(mispelt.adamawa))
#> [1] 3
corrected.adamawa <- fix_region(mispelt.adamawa)
#> 'Machika' approximately matched more than one region - Machina, Michika
#> ℹ Successful fix(es):
#> -------------------
#> * Fufure => Fufore
#> 
#> Fix(es) not applied:
#> --------------------
#> * Machika
sum(is_lga(corrected.adamawa))
#> [1] 5
```

We see that the string ‘Machika’ is not an actual LGA and there are more
than one possible candidate LGA that are considered as possible
replacement. Our original intent was to use “Michika LGA”. To address
this mistake, we can run `fix_region` interactively. Note that the
`interactive` option is only available for use with objects of class
`lgas`.

``` r

adamawa <- fix_region(lgas(corrected.adamawa), interactive = TRUE)
```

Next, the user is provided with a prompt to provide a search item for
likely LGAs that would be an appropriate replacement for the misspelt
one. Possible replacements are presented and to select any value, the
appropriate number should be entered at the prompt. The option `RETRY`
allows the user to restart the query and provide another search term,
`SKIP` is to try out a different misspelt item (where there are more
than one) and to `QUIT` is to exit the prompt. On Windows machines, the
user can use the native dialog boxes by setting `graphic` to `TRUE`.

``` r

# Confirm that the spelling mistakes have been fixed.
all(is_lga(adamawa))
#> [1] TRUE
```

#### 3. Manual fixes

When spelling errors are identified and the correct one is already
known, then a manual fix can be applied. For this, we use the function
`fix_region_manual` and its use is straightforward[^2]:

``` r

adamawa <- fix_region_manual(corrected.adamawa,
                             wrong = "Machika",
                             correct = "Michika")
adamawa
#> [1] "Demsa"   "Fufore"  "Fufore"  "Ganye"   "Hong"    "Michika"
```

[^1]: There is a method for repairing the names of States but the
    operation is more manageable since there are far fewer States

[^2]: Works for both character vectors and `lgas` objects.
