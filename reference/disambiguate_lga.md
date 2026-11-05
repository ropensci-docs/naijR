# Disambiguate Synonymous States and LGAs

Some LGAs in Nigeria bear the name of the States to which they belong
to. This function will apply an attribute to such an LGA to distinguish
it from its State.

## Usage

``` r
disambiguate_lga(lga, state = NULL, ...)
```

## Arguments

- lga:

  An object of class `lgas` of length `1L`.

- state:

  The name of the State to which the LGA is to belong to.

- ...:

  Arguments to be passed to [`menu`](https://rdrr.io/r/utils/menu.html).

## Value

The object of class `lgas` with the (possibly) modified `State`
attribute.

## Details

For `state`, if it is not provided by the user, an interactive prompt
will be presented to the user to select the appropriate state - but only
in interactive sessions; if run as a batch command, this function will
signal an error.

## Examples

``` r
obi.lga <- lgas("Obi")    # Warning
#> Warning: 'Obi' LGA is found in 2 States: Benue, Nasarawa
try(map_ng(obi.lga))      # Error
#> Error in plot_sf(x, ...) : 
#>   NA value(s) in bounding box. Trying to plot empty geometries?

obi.benue <- disambiguate_lga(obi.lga, "Benue")

if (interactive())
  map_ng(obi.benue)
```
