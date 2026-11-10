# Metadata about data available from the different services: data (layers) from a data source (service), metadata on layers from a service, metadata on layers from all services.

Get WFS available layer information

## Usage

``` r
emodnet_get_layer_info(wfs, layers)

emodnet_get_wfs_info(wfs = NULL, service = NULL, service_version = NULL)

emodnet_get_all_wfs_info()
```

## Arguments

- wfs:

  A `WFSClient` R6 object with methods for interfacing an OGC Web
  Feature Service. From
  [`emodnet_init_wfs_client()`](https://docs.ropensci.org/emodnet.wfs/reference/emodnet_init_wfs_client.md).

- layers:

  a character vector of layer names. To get info on layers, including
  `layer_name` use `emodnet_get_wfs_info()`.

- service:

  the EMODnet OGC WFS service name. For available services, see
  [`emodnet_wfs()`](https://docs.ropensci.org/emodnet.wfs/reference/emodnet_wfs.md).

- service_version:

  **\[deprecated\]** the WFS service version. Now always "2.0.0".

## Value

a tibble containing metadata on each layer available from the service.

## Details

To minimize the number of requests sent to webservices, these functions
use `memoise` to cache results inside the active R session. To clear the
cache, re-start R or run `memoise::forget(emodnet_get_wfs_info)`/
`memoise::forget(emodnet_get_layer_info)`.

## Functions

- `emodnet_get_layer_info()`: Get metadata for specific layers. Requires
  a `wfs` object as input.

- `emodnet_get_wfs_info()`: Get info on all layers from an EMODnet WFS
  service.

- `emodnet_get_all_wfs_info()`: Get metadata on all layers and all
  available services from server.

## Examples

``` r
emodnet_get_wfs_info(service = "bathymetry")
#> ✔ WFS client created successfully
#> ℹ Service: "https://ows.emodnet-bathymetry.eu/wfs"
#> ℹ Version: "2.0.0"
#> # A tibble: 7 × 9
#> # Rowwise: 
#>   data_source service_name service_url    layer_name title abstract class format
#>   <chr>       <chr>        <chr>          <chr>      <chr> <chr>    <chr> <chr> 
#> 1 emodnet_wfs bathymetry   https://ows.e… download_… Bath… "Downlo… WFSF… sf    
#> 2 emodnet_wfs bathymetry   https://ows.e… contours   Dept… "Genera… WFSF… sf    
#> 3 emodnet_wfs bathymetry   https://ows.e… hr_bathym… High… "Layer … WFSF… sf    
#> 4 emodnet_wfs bathymetry   https://ows.e… quality_i… Qual… "Repres… WFSF… sf    
#> 5 emodnet_wfs bathymetry   https://ows.e… sea_names  Sea … "Mainta… WFSF… sf    
#> 6 emodnet_wfs bathymetry   https://ows.e… source_re… Sour… "Covera… WFSF… sf    
#> 7 emodnet_wfs bathymetry   https://ows.e… undersea_… unde… ""       WFSF… sf    
#> # ℹ 1 more variable: layer_namespace <chr>
# Query a wfs object
wfs_bio <- emodnet_init_wfs_client("biology")
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Emodnetbio/wfs"
#> ℹ Version: "2.0.0"
emodnet_get_wfs_info(wfs_bio)
#> # A tibble: 39 × 9
#> # Rowwise: 
#>    data_source service_name service_url   layer_name title abstract class format
#>    <chr>       <chr>        <chr>         <chr>      <chr> <chr>    <chr> <chr> 
#>  1 emodnet_wfs biology      https://geo.… cti_macro… Comm… "Ocean … WFSF… sf    
#>  2 emodnet_wfs biology      https://geo.… mediseh_c… EMOD… "Coral … WFSF… sf    
#>  3 emodnet_wfs biology      https://geo.… mediseh_c… EMOD… "Coral … WFSF… sf    
#>  4 emodnet_wfs biology      https://geo.… mediseh_c… EMOD… "Cymodo… WFSF… sf    
#>  5 emodnet_wfs biology      https://geo.… Species_g… EMOD… "This d… WFSF… sf    
#>  6 emodnet_wfs biology      https://geo.… Species_g… EMOD… "This d… WFSF… sf    
#>  7 emodnet_wfs biology      https://geo.… Species_g… EMOD… "This d… WFSF… sf    
#>  8 emodnet_wfs biology      https://geo.… Species_g… EMOD… "This d… WFSF… sf    
#>  9 emodnet_wfs biology      https://geo.… mediseh_h… EMOD… "Haloph… WFSF… sf    
#> 10 emodnet_wfs biology      https://geo.… mediseh_m… EMOD… "Maërl … WFSF… sf    
#> # ℹ 29 more rows
#> # ℹ 1 more variable: layer_namespace <chr>
# Get info for specific layers from wfs object
layers <- c("mediseh_zostera_m_pnt", "mediseh_posidonia_nodata")
emodnet_get_layer_info(wfs = wfs_bio, layers = layers)
#> # A tibble: 2 × 9
#> # Rowwise: 
#>   data_source service_name    service_url layer_name title abstract class format
#>   <chr>       <chr>           <chr>       <chr>      <chr> <chr>    <chr> <chr> 
#> 1 emodnet_wfs https://geo.vl… biology     mediseh_p… EMOD… "Coastl… WFSF… sf    
#> 2 emodnet_wfs https://geo.vl… biology     mediseh_z… EMOD… "Zoster… WFSF… sf    
#> # ℹ 1 more variable: layer_namespace <chr>
```
