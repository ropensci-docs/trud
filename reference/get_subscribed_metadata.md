# Get metadata for subscribed NHS TRUD items

A convenience wrapper around
[`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
and
[`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md),
retrieving metadata for only items that the user is subscribed to. This
is particularly useful for seeing what data you can download with
[`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md).
If you need access to additional items, browse available options with
[`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md),
then subscribe through the NHS TRUD website.

## Usage

``` r
get_subscribed_metadata(release_scope = c("all", "latest"))
```

## Arguments

- release_scope:

  Which releases to retrieve metadata for. Use `"all"` to get all
  releases, or `"latest"` to get only the most recent release.

## Value

A tibble, with item metadata stored in the list column `metadata`. Use
the `item_number` column values with
[`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md).

## See also

- [`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
  to browse all available items

- [`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
  for detailed metadata on specific items

- [`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md)
  to download items you're subscribed to

## Examples

``` r
if (FALSE) { # identical(Sys.getenv("IN_PKGDOWN"), "true") & Sys.getenv("TRUD_API_KEY") != ""
  # Get metadata for all subscribed items
  subscribed <- get_subscribed_metadata()

  # Show structure without exposing API keys in URLs
  subscribed$metadata[[1]] |>
    purrr::map_at("releases", \(release) purrr::map(release, names))
}
```
