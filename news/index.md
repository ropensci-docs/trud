# Changelog

## trud (development version)

## trud 0.2.1

CRAN release: 2026-03-16

### Bug fixes

- Fixed download failure for items with spaces in archive filenames by
  URL-encoding the download URL
  ([\#7](https://github.com/ropensci/trud/issues/7)).

## trud 0.2.0

CRAN release: 2025-08-18

### Major changes

- Enhanced parameter design with enum validation:

  - [`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
    and
    [`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md)
    now use `release_scope = c("all", "latest")` parameter instead of
    `latest_only` boolean. This makes function calls more expressive and
    eliminates boolean ambiguity.
  - [`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md)
    now uses
    `file_type = c("archive", "checksum", "signature", "publicKey")`
    parameter instead of `download_file`.

- Added `overwrite` parameter to
  [`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md)
  allowing users to explicitly control whether existing files should be
  overwritten.

- **Breaking changes:**

  - Removed `TRUD_API_KEY` parameter from all exported functions. API
    keys must now be set via the `TRUD_API_KEY` environment variable
    only.
  - [`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md)
    parameter `download_file` renamed to `file_type` with enhanced
    validation.
  - [`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
    and
    [`get_subscribed_metadata()`](https://docs.ropensci.org/trud/reference/get_subscribed_metadata.md)
    parameter `latest_only` replaced with `release_scope`.

### Minor changes and bug fixes

- Improved documentation and user experience:
  - Enhanced subscription workflow documentation with clear step-by-step
    guidance.
  - Added explanation that
    [`purrr::map_at()`](https://purrr.tidyverse.org/reference/map_if.html)
    pattern is used in examples to avoid exposing API keys.
  - Clarified how to obtain and use release IDs from
    [`get_item_metadata()`](https://docs.ropensci.org/trud/reference/get_item_metadata.md)
    for downloading specific releases.
- Enhanced robustness and testing:
  - Added validation warnings to
    [`trud_items()`](https://docs.ropensci.org/trud/reference/trud_items.md)
    to detect changes in NHS TRUD website structure that might break the
    scraper.
  - Refactored tests to use
    [`withr::local_tempdir()`](https://withr.r-lib.org/reference/with_tempfile.html)
    for better test isolation and cleanup.
  - Improved test descriptions to be more specific and informative.
  - Enhanced error handling with better retry logic and rate limiting.
- Technical improvements:
  - Added support for custom user agent headers via `TRUD_USER_AGENT`
    environment variable.
  - Improved file existence handling in
    [`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md)
    with clearer warning messages.
  - Enhanced request handling with retry logic, and rate limiting.
  - Consistently return file paths invisibly from
    [`download_item()`](https://docs.ropensci.org/trud/reference/download_item.md).

## trud 0.1.0

CRAN release: 2024-07-22

- Initial CRAN submission.
