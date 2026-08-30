# Map of Nigeria

Maps of the Federal Republic of Nigeria that are based on the basic
plotting idiom utilised by
[maps:map](https://rdrr.io/pkg/maps/man/map.html) and its variants.

## Usage

``` r
map_ng(
  region = character(),
  data = NULL,
  x = NULL,
  y = NULL,
  breaks = NULL,
  categories = NULL,
  excluded = NULL,
  exclude.fill = NULL,
  title = NULL,
  caption = NULL,
  show.neighbours = FALSE,
  show.text = FALSE,
  legend.text = NULL,
  leg.title,
  plot = TRUE,
  ...
)
```

## Arguments

- region:

  A character vector of regions to be displayed. This could be States or
  Local Government Areas.

- data:

  An object containing data, principally the variables required to plot
  in a map.

- x, y:

  Numeric object or factor (or coercible to one). See *Details*.

- breaks:

  Numeric. A vector of length \>= 1. If a single value i.e. scalar, it
  denotes the expected number of breaks. Internally, the function will
  attempt to compute appropriate category sizes or fail if out-of
  bounds. Where length is \>= 3L, it is expected to be an arithmetic
  sequence that represents category bounds as for
  [`cut`](https://rdrr.io/r/base/cut.html) (applicable only to
  choropleth maps).

- categories:

  The legend for the choropleth-plotted categories. If not defined,
  internally created labels are used.

- excluded:

  Regions to be excluded from a choropleth map.

- exclude.fill:

  Colour-shading to be used to indicate `excluded` regions. Must be a
  vector of the same length as `excluded`.

- title, caption:

  An optional string for annotating the map.

- show.neighbours:

  Logical; `TRUE` to display the immediate vicinity neighbouring
  regions/countries.

- show.text:

  Logical. Whether to display the labels of regions.

- legend.text:

  Logical (whether to show the legend) or character vector (actual
  strings for the legend). The latter will override whatever is provided
  by `categories`, giving the user additional control.

- leg.title:

  String. The legend title. If missing, a default value is acquired from
  the data. To turn off the legend title, pass `NULL`.

- plot:

  Logical. Turn actual plotting of the map off or on.

- ...:

  Further arguments passed to
  [`plot`](https://r-spatial.github.io/sf/reference/plot.html)

## Value

An object of class `sf`, which is a standard format containing the data
used to draw the map and thus can be used by this and other popular R
packages to visualize the spatial data.

## Details

The default value for `region` is to print all State boundaries. `data`
enables the extraction of data for plotting from an object of class
`data.frame`. Columns containing regions (i.e. States as well as
supported sub-national jurisdictions) are identified. The argument also
provides context for quasiquotation when providing the `x` and `y`
arguments.

For `x` and `y`, when both arguments are supplied, they are taken to be
point coordinates, where `x` represent longitude and `y` latitude. If
only `x` is supplied, it is assumed that the intention of the user is to
make a choropleth map, and thus, numeric vector arguments are converted
into factors i.e. number classes. Otherwise factors or any object that
can be coerced to a factor should be used.

For plain plots, the `col` argument works the same as with
[`map`](https://rdrr.io/pkg/maps/man/map.html). For choropleth maps, the
colour provided represents a (sequential) colour palette based on
[`RColorBrewer::brewer.pal`](https://rdrr.io/pkg/RColorBrewer/man/ColorBrewer.html).
The available colour options can be checked with
`getOption("choropleth.colours")` and this can also be modified by the
user.

If the default legend is unsatisfactory, it is recommended that the user
sets the `legend.text` argument to `FALSE`; the next function call
should be [`legend`](https://rdrr.io/r/graphics/legend.html) which will
enable finer control over the legend.

## Note

When adjusting the default colour choices for choropleth maps, it is
advisable to use one of the sequential palettes. For a list of of
available palettes, especially for more advanced use, review
[`RColorBrewer::display.brewer.all`](https://rdrr.io/pkg/RColorBrewer/man/ColorBrewer.html).

## See also

[`vignette("nigeria-maps")`](https://docs.ropensci.org/naijR/articles/nigeria-maps.md)
for additional ways to use this function.

## Examples

``` r
if (FALSE) { # \dontrun{
map_ng() # Draw a map with default settings
map_ng(states("sw"))
map_ng("Kano")} # }
```
