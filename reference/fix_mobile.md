# Fix mobile numbers

Fixes up local mobile phone numbers to a uniform text format.

## Usage

``` r
fix_mobile(x)
```

## Arguments

- x:

  Values to be fixed, represented either as `numeric` or `character`
  vectors.

## Value

The updated vector, usually the column of a data frame.

## Details

This format is specific to that used in a given location - for now the
function is useful only for Nigeria mobile numbers, which come in the
format expressed by the regex pattern `"^0[7-9][0-1][0-9]{8}$"`.

## Note

There is an option for producing warnings on any mobile number entries
that may have been removed from the vector, by setting the option
`verbose` to `TRUE`.

## Examples

``` r
fix_mobile("803-123-4567")    # Adds leading '0" and removes separators
#> [1] "08031234567"
```
