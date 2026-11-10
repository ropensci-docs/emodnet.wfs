# Connect to a data source (service)

Initialise an EMODnet WFS client

## Usage

``` r
emodnet_init_wfs_client(service, service_version = NULL, logger = NULL)
```

## Arguments

- service:

  the EMODnet OGC WFS service name. For available services, see
  [`emodnet_wfs()`](https://docs.ropensci.org/emodnet.wfs/reference/emodnet_wfs.md).

- service_version:

  **\[deprecated\]** the WFS service version. Now always "2.0.0".

- logger:

  the logger. Either `NULL` (no logging info), `"INFO"` (log about ows4R
  requests) or `"DEBUG"` (including curl details).

## Value

An
[`ows4R::WFSClient`](https://eblondel.github.io/ows4R/reference/WFSClient.html)
R6 object with methods for interfacing an OGC Web Feature Service.

## See also

`WFSClient` in package `ows4R`.

## Examples

``` r
wfs <- emodnet_init_wfs_client(service = "bathymetry")
#> ✔ WFS client created successfully
#> ℹ Service: "https://ows.emodnet-bathymetry.eu/wfs"
#> ℹ Version: "2.0.0"
```
