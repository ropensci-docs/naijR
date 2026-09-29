# Objects for Representing the Federal States of Nigeria

Objects for Representing the Federal States of Nigeria

## Usage

``` r
states(states, gpz = NULL, all = TRUE, warn = TRUE)

is_state(x)

as_state(x)

# S3 method for class 'states'
print(x, ...)

# S3 method for class 'states'
c(...)

# S3 method for class 'states'
x[[i, exact = TRUE]]

# S3 method for class 'states'
x[i]

# S3 method for class 'states'
na.exclude(object, ...)
```

## Arguments

- states:

  A character vector with strings representing one or more States of
  Nigeria. If missing, the function will return a `states` object
  containing all the States.

- gpz:

  `NULL` (the default) or, case insensitively, one or more of the
  following strings: `"nc", "ne", "nw", "se", "ss"` and `"sw"` (see
  "Details").

- all:

  logical; whether to include the Federal Capital Territory (FCT) in the
  result.

- warn:

  logical; issue a warning when one or more elements are not actually
  States (i.e. they were misspelt).

- x:

  For `is_state` a vector to be tested. For `as_state`, a string
  representing a State that shares its name with one of its Local
  Government Areas.

- ...:

  Arguments used for methods. See documentation of generic for details.

- i, exact:

  See help file for [`?Extract`](https://rdrr.io/r/base/Extract.html)

- object:

  An object of class `regions`

## Value

The States of Nigeria as a whole or by zones, as an S3 object of class
`states`. `is_state` returns a logical vector.of same length as the
input. If the input object is not even of type `character`, return the
object unaltered, with a warning. In the case of `as_state`, an object
of class `states`.

## Details

`gpz` represents a geopolitical zone which, in the Nigerian context, is
a national subdivision that groups contiguous states that bear certain
socio-cultural and political similarities. Historically, they arise from
sub-national administrative divisions known as 'Regions' that existed at
the time of the country's independence. There are at present 6 such
zones - North-Central, North-East, North-West, South-East,South-South
and South-West.

For `is_state`, An element-wise check of a supplied vector is carried
out. To test an entire vector and return a single boolean value,
functions such as [`base::all`](https://rdrr.io/r/base/all.html) or
[`base::any`](https://rdrr.io/r/base/any.html) should be used (see
examples).

## Note

`is_state` throws a warning, when a missing value is among the elements.
It works only for atomic vectors, throwing an error when this is not the
case or when `NULL` is passed to it. This design decision was made to
allow rapid iteration through data frames without interruption, since
spelling mistakes tend to be common.

## Examples

``` r
states()  # lists names of all States
#> States
#> ------ 
#> * Abia
#> * Adamawa
#> * Akwa Ibom
#> * Anambra
#> * Bauchi
#> * Bayelsa
#> * Benue
#> * Borno
#> * Cross River
#> * Delta
#> * Ebonyi
#> * Edo
#> * Ekiti
#> * Enugu
#> * Federal Capital Territory
#> * Gombe
#> * Imo
#> * Jigawa
#> * Kaduna
#> * Kano
#> * Katsina
#> * Kebbi
#> * Kogi
#> * Kwara
#> * Lagos
#> * Nasarawa
#> * Niger
#> * Ogun
#> * Ondo
#> * Osun
#> * Oyo
#> * Plateau
#> * Rivers
#> * Sokoto
#> * Taraba
#> * Yobe
#> * Zamfara 
states(gpz = "se")  # lists States in South-East zone
#> States
#> ------ 
#> * Abia
#> * Anambra
#> * Ebonyi
#> * Enugu
#> * Imo 
all(is_state(naijR::states()))
#> [1] TRUE
is_state(c("Maryland", "Baden-Baden", "Plateau", "Sussex"))
#> [1] FALSE FALSE  TRUE FALSE

# With coercion
kt.st <- states("Katsina")  # Ensure this is a State, not an LGA.
kt.lg <- suppressWarnings(as_lga(kt.st))
is_state(kt.st)             # TRUE
#> [1] TRUE
is_lga(kt.lg)               # TRUE
#> [1] TRUE

## Where there's no ambiguity, it doesn't make sense to coerce
## This kind of operation ends with an error
if (FALSE) { # \dontrun{
as_state("Kano")
as_lga("Michika")
} # }
```
