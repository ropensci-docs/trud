# Download NHS TRUD item

Downloads files for a specified NHS TRUD item. By default this downloads
the latest release. Use the `item` numbers from
[`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
or
[`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md).

***Subscription Required***

You must subscribe to TRUD items individually through the NHS TRUD
website before you can access them using
[`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
or `download_item()`. Simply having an API key is not sufficient. To see
items you're already subscribed to, use
[`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md).
To browse all available items, use
[`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md).

## Usage

``` r
download_item(
  item,
  directory = ".",
  file_type = c("archive", "checksum", "signature", "publicKey"),
  release = NULL,
  overwrite = FALSE
)
```

## Arguments

- item:

  An integer, the item to be downloaded. Get these from
  [`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
  or
  [`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md).

- directory:

  Path to the directory to which this item will be downloaded to. This
  is set to the current working directory by default.

- file_type:

  The type of file to download. Options are `"archive"` (the main
  release file), `"checksum"`, `"signature"`, or `"publicKey"`. Defaults
  to `"archive"`.

- release:

  The release ID to be downloaded. Release IDs are found in the `id`
  field of each release from
  [`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md).
  If `NULL` (default), the latest item release will be downloaded.

- overwrite:

  If `TRUE`, existing files will be overwritten. If `FALSE` (default),
  existing files will be skipped and the function will return the
  existing file path.

## Value

The file path to the downloaded file, returned invisibly.

## Working with specific releases

To download a specific (non-latest) release:

1.  Use
    [`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
    with `release_scope = "all"` to retrieve metadata for all releases

2.  The release IDs are stored under the `id` item for each release

3.  Pass the desired release ID to the `release` parameter of
    `download_item()`

## See also

- [`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
  to find item numbers

- [`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md)
  to see items you can access

- [`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
  to explore available releases before downloading

## Examples

``` r
if (FALSE) { # identical(Sys.getenv("IN_PKGDOWN"), "true") & Sys.getenv("TRUD_API_KEY") != ""
# Download Community Services Data Set pre-deadline extract XML Schema
x <- download_item(394, directory = tempdir())

# List downloaded files
unzip(x, list = TRUE)

# Download a previous release
# First get all releases to see available options
metadata <- get_item_metadata(394, release_scope = "all")
release_id <- metadata$releases[[2]]$id

y <- download_item(394, directory = tempdir(), release = release_id)

unzip(y, list = TRUE)

# Overwrite existing files if needed
z <- download_item(394, directory = tempdir(), overwrite = TRUE)
}
# An informative error is raised if your API key is invalid or missing
try(withr::with_envvar(c("TRUD_API_KEY" = ""), download_item(394)))
#> Error in download_item(394) : 
#>   ✖ Can't find NHS TRUD API key
#> ℹ Set your NHS TRUD API key as an environment variable using
#>   `Sys.setenv(TRUD_API_KEY='<<your-key>>')`, or preferably use a `.Renviron`
#>   file
#> ℹ To get an API key, first sign up for a NHS TRUD account at
#>   <https://isd.digital.nhs.uk/trud/users/guest/filters/0/account/form>
#> ℹ To find Your API key, log in and visit your account profile page
#>   (<https://isd.digital.nhs.uk/trud/users/authenticated/filters/0/account/manage>).
```
