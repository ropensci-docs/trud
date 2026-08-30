# Get available NHS TRUD items

Scrapes [this
page](https://isd.digital.nhs.uk/trud/users/guest/filters/0/categories/1)
from the NHS TRUD website for all available items. The `item_number`
column in the result contains the identifiers you need for
[`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
and
[`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md).

***Subscription Required***

You must subscribe to TRUD items individually through the NHS TRUD
website before you can access them using
[`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
or
[`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md).
Simply having an API key is not sufficient. To see items you're already
subscribed to, use
[`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md).
To browse all available items, use `trud_items()`.

## Usage

``` r
trud_items()
```

## Value

A tibble, with columns `item_number` and `item_name`. Use the
`item_number` values as arguments to
[`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
and
[`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md).

## See also

- [`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md)
  to see only items you're subscribed to

- [`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
  to get detailed information about a specific item

- [`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md)
  to download files for a specific item

## Examples

``` r
trud_items()
#> # A tibble: 75 × 2
#>    item_number item_name                                                        
#>          <int> <chr>                                                            
#>  1         246 Cancer Outcomes and Services Data Set XML Schema                 
#>  2         245 Commissioning Data Set XML Schema                                
#>  3         599 Community Services Data Set Intermediate Database                
#>  4         393 Community Services Data Set post-deadline extract XML Schema     
#>  5         394 Community Services Data Set pre-deadline extract XML Schema      
#>  6         391 Community Services Data Set XML Schema                           
#>  7        1899 Diagnostic Imaging Data Set (DIDS) - CSV format                  
#>  8         248 Diagnostic Imaging Data Set XML Schema                           
#>  9         239 dm+d XML transformation tool                                     
#> 10        1859 Electronic Prescribing and Medicines Administration Data Sets XM…
#> # ℹ 65 more rows
```
