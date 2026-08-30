# Objects for Representing the Local Government Areas (LGAs) of Nigeria

Objects for Representing the Local Government Areas (LGAs) of Nigeria

## Usage

``` r
lgas(region = NA_character_, strict = FALSE, warn = TRUE)

is_lga(x)

as_lga(x)

# S3 method for class 'lgas'
print(x, ...)

# S3 method for class 'lgas'
c(...)

# S3 method for class 'lgas'
x[[i, exact = TRUE]]

# S3 method for class 'lgas'
x[i]

# S3 method for class 'lgas'
na.exclude(object, ...)
```

## Arguments

- region:

  Context-dependent. Either State(s) of the Federation or Local
  Government Area(s) - internal checks are performed to determine what
  applies. In cases where States are synonymous to LGAs, the default
  behaviour is to use the State as a basis for selecting the LGAs. This
  can be modified with `strict`. The default value is `NA_character_`
  and will return all 774 LGAs.

- strict:

  logical; in the event of a name clash between State/LGA, return only
  the specified LGA when this argument is set to `TRUE`.

- warn:

  logical; issue a warning when one or more elements are not actually
  Local Government Areas (or were misspelt).

- x:

  An object of type `character`. This includes higher dimension object
  classes like `matrix` and `array`. For `as_lga`, a string representing
  a Local Government Area that shares its name with one of its States.

- ...:

  Arguments used for methods. See documentation of generic for details.

- i, exact:

  See help file for [`?Extract`](https://rdrr.io/r/base/Extract.html)

- object:

  An object of class `regions`

## Value

If length of `ng.state` == 1L, a character vector containing the names
of Local Government Areas; otherwise a named list, whose elements are
character vectors of the LGAs in each state. `is_lga` returms a vector
the same length as the input object (each element that is not a valid
Local Government Area will evaluate to `FALSE`); with `as_lga`, an
object of class `lgas`.

## Note

There are six (6) LGAs that share names with their State - Bauchi,
Ebonyi, Gombe, Katsina, Kogi and Ekiti.

## Examples

``` r
how_many_lgas <- function(state) {
  require(naijR)
  stopifnot(all(is_state(state)))
  cat(sprintf("No. of LGAs in %s State:", state),
    length(lgas(state)),
    fill = TRUE)
}
how_many_lgas("Sokoto")
#> No. of LGAs in Sokoto State: 23
how_many_lgas("Ekiti")
#> No. of LGAs in Ekiti State: 16
is_lga(c("Pankshen", "Pankshin"))
#> [1] FALSE  TRUE

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
