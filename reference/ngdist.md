# Road Distances Between Nigerian State Capitals

A symmetric distance matrix containing approximate road (driving)
distances in kilometres between all 37 Nigerian State capitals
(including Abuja for the Federal Capital Territory).

## Usage

``` r
ngdist
```

## Format

An object of class `dist` with 37 labels — one for each State capital.
The labels are city names in title case (e.g. `"Lagos"`,
`"Port Harcourt"`).

## Details

The matrix holds \\37 \times 36 / 2 = 666\\ unique pairwise distances.
Values are sourced from UNDP and represent typical road travel; actual
distances may vary with route choice, road conditions, or detours.

For a convenient way to look up individual distances, see
[`ng_distance`](https://docs.ropensci.org/naijR/reference/ng_distance.md).

## See also

[`ng_distance`](https://docs.ropensci.org/naijR/reference/ng_distance.md)
for querying a single pair of cities.

## Examples

``` r
data(ngdist)
labels(ngdist)          # city names
#>  [1] "Abakaliki"     "Abeokuta"      "Abuja"         "Ado Ekiti"    
#>  [5] "Akure"         "Asaba"         "Awka"          "Bauchi"       
#>  [9] "Benin City"    "Birnin Kebbi"  "Calabar"       "Damaturu"     
#> [13] "Dutse"         "Enugu"         "Gombe"         "Gusau"        
#> [17] "Ibadan"        "Ikeja"         "Ilorin"        "Jalingo"      
#> [21] "Jos"           "Kaduna"        "Kano"          "Katsina"      
#> [25] "Lafia"         "Lokoja"        "Maiduguri"     "Makurdi"      
#> [29] "Minna"         "Osogbo"        "Owerri"        "Port Harcourt"
#> [33] "Sokoto"        "Umuahia"       "Uyo"           "Yenagoa"      
#> [37] "Yola"         
as.matrix(ngdist)[1:5, 1:5]
#>           Abakaliki Abeokuta Abuja Ado Ekiti Akure
#> Abakaliki         0      656   477       566   506
#> Abeokuta        656        0   722       340   280
#> Abuja           477      722     0       480   420
#> Ado Ekiti       566      340   480         0    60
#> Akure           506      280   420        60     0
```
