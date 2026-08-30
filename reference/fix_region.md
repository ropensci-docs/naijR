# Fix Misspelling of Administrative Regions

Correct any misspelled names of administrative regions e.g. States and
LGAs.

## Usage

``` r
fix_region(x, ...)

# S3 method for class 'states'
fix_region(x, ...)

# S3 method for class 'lgas'
fix_region(x, interactive = FALSE, quietly = FALSE, graphic = FALSE, ...)

# Default S3 method
fix_region(x, ...)

fix_region_manual(x, wrong, correct)
```

## Arguments

- x:

  An S3 object of class `states` or `lgas`. For `fix_region.default`, a
  character vector (or an object coercible to one) can be passed but
  only that for 'States' can be interpreted.

- ...:

  Arguments passed to methods.

- interactive:

  Logical. When `TRUE`, the function prompts the user to interactively
  select the correct LGA names from a list of available options.

- quietly:

  Logical; default argument is `FALSE`.

- graphic:

  Whether to make use of native GUI elements (on Windows only).

- wrong:

  The misspelled element(s) of `x`.

- correct:

  The correction that is to be applied to the misspelled element(s)

## Value

The transformed object. If all names are correct, the object is returned
unchanged.

## Details

`fix_region` will look through a character vector and try to determine
if State or LGA names have been wrongly entered. This presupposes that
the atomic vector is of type `character`. It does not test any missing
values in the vector, leaving them untouched.

`fix_region_manual` allows users to interactively and directly change
update the spelling.

## Note

When passed a character vector of length `1L`, in the case of a
misspelled LGA, the function signals an error; the presumption is that a
fix can readily be applied interactively. When all the items provided
are misspelled, nothing happens, but the user is advised to use the
appropriate constructor function so as to improve the accuracy of the
repairs. When there is a mix of misspelled and properly spelled LGAs,
other avenues for fixing the mistakes are available via mode
`interactive`.

## Examples

``` r
try(fix_region("Owerri north")) # ERROR
#> Error in fix_region("Owerri north") : 
#>   Incorrect region name(s); consider reconstructing 'x' with `states()` or
#> `lgas()` for a more reliable fix
fix_region(c("Owerri north", "Owerri West"))

x <- c("Pankshen", "Pankshin", "Q'uan Pam")
is_lga(x)
#> [1] FALSE  TRUE FALSE
x <- fix_region(x, quietly = TRUE)
is_lga(x)
#> [1]  TRUE  TRUE FALSE
fix_region_manual(x, "Q'uan Pam", "Qua'an Pan")
#> [1] "Pankshin"   "Pankshin"   "Qua'an Pan"
all(is_lga(x))
#> [1] FALSE
```
