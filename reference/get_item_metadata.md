# Retrieve metadata for a NHS TRUD item

Sends a request to the release list endpoint, returning a list of
metadata pertaining to the specified NHS TRUD item. Use the `item`
numbers from
[`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
or
[`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md).

***Subscription Required***

You must subscribe to TRUD items individually through the NHS TRUD
website before you can access them using `get_item_metadata()` or
[`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md).
Simply having an API key is not sufficient. To see items you're already
subscribed to, use
[`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md).
To browse all available items, use
[`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md).

## Usage

``` r
get_item_metadata(item, release_scope = c("all", "latest"))
```

## Arguments

- item:

  An integer, the item to be downloaded. Get these from
  [`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
  or
  [`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md).

- release_scope:

  Which releases to retrieve metadata for. Use `"all"` to get all
  releases, or `"latest"` to get only the most recent release.

## Value

A list containing item metadata, including release information that can
be used with
[`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md).
Release IDs for specific downloads are in the `id` field of each
release.

## See also

- [`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
  to find item numbers

- [`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md)
  to see items you can access

- [`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md)
  to download files using this metadata

## Examples

``` r
if (FALSE) { # identical(Sys.getenv("IN_PKGDOWN"), "true") & Sys.getenv("TRUD_API_KEY") != ""
# Get metadata for Community Services Data Set pre-deadline extract XML Schema
get_item_metadata(394) |>
  # Display structure without showing sensitive API keys in URLs
  purrr::map_at("releases", \(release) purrr::map(release, names))

# Include metadata for any previous releases using `release_scope = "all"`
get_item_metadata(394, release_scope = "all") |>
  # Display structure without showing sensitive API keys in URLs
  purrr::map_at("releases", \(release) purrr::map(release, names))
}
# An informative error is raised if your API key is invalid or missing
try(withr::with_envvar(c("TRUD_API_KEY" = ""), get_item_metadata(394)))
#> Error in get_item_metadata(394) : 
#>   ✖ Can't find NHS TRUD API key
#> ℹ Set your NHS TRUD API key as an environment variable using
#>   `Sys.setenv(TRUD_API_KEY='<<your-key>>')`, or preferably use a `.Renviron`
#>   file
#> ℹ To get an API key, first sign up for a NHS TRUD account at
#>   <https://isd.digital.nhs.uk/trud/users/guest/filters/0/account/form>
#> ℹ To find Your API key, log in and visit your account profile page
#>   (<https://isd.digital.nhs.uk/trud/users/authenticated/filters/0/account/manage>).
```
