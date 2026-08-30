# Distance between two Nigerian state capitals

Retrieves the precomputed road (driving) distance between Nigerian state
capitals. Both `a` and `b` can be vectors of the same length, in which
case distances are computed element-wise.

## Usage

``` r
ng_distance(a, b, unit = c("km", "miles"))
```

## Arguments

- a, b:

  Character vector. Name(s) of city/cities (case-insensitive). Must be
  the same length; vector recycling is not permitted.

- unit:

  Character. Unit of distance to return. One of "km" (default) or
  "miles".

## Value

Numeric vector of road distances in the requested unit (rounded to 1
decimal place), with the same length as `a` and `b`.

## Details

Distances are approximate driving distances sourced from travel
allowance guidance provided by UNDP Nigeria. They represent typical road
travel and may vary due to route choice, road conditions, or detours.

## Examples

``` r
ng_distance("Lagos", "Kano")
#> [1] 1139
ng_distance("Abuja", "Port Harcourt", unit = "miles")
#> [1] 508.3
ng_distance("Ibadan", "enugu")  # case-insensitive
#> [1] 558
ng_distance(c("Lagos", "Abuja"), c("Kano", "Enugu"))  # vectorized
#> [1] 1139  393
```
