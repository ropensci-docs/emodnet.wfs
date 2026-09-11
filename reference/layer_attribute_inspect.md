# Summary of individual variable (attribute) in a dataset (layer) from a data source (service).

Inspect layer attributes

## Usage

``` r
layer_attribute_inspect(
  wfs = NULL,
  service = NULL,
  service_version = NULL,
  layer,
  attribute
)
```

## Arguments

- wfs:

  A `WFSClient` R6 object with methods for interfacing an OGC Web
  Feature Service. From
  [`emodnet_init_wfs_client()`](https://docs.ropensci.org/emodnet.wfs/reference/emodnet_init_wfs_client.md).

- service:

  the EMODnet OGC WFS service name. For available services, see
  [`emodnet_wfs()`](https://docs.ropensci.org/emodnet.wfs/reference/emodnet_wfs.md).

- service_version:

  **\[deprecated\]** the WFS service version. Now always "2.0.0".

- layer:

  character sting of layer name. To get info on layers, including
  `layer_name` use
  [`emodnet_get_wfs_info()`](https://docs.ropensci.org/emodnet.wfs/reference/emodnet_get_wfs_info.md).

- attribute:

  character string, name of layer attribute (variable). Use
  [`layer_attributes_get_names()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_get_names.md)
  to get layer attribute names.

## Value

Detailed summary of individual attribute (variable). Particularly useful
for inspecting factor or character variable levels or unique values.

## See also

Attributes metadata:
[`layer_attribute_descriptions()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attribute_descriptions.md),
[`layer_attributes_get_names()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_get_names.md),
[`layer_attributes_summarise()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_summarise.md),
[`layer_attributes_tbl()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_tbl.md)

## Examples

``` r
wfs <- emodnet_init_wfs_client(service = "biology")
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Emodnetbio/wfs"
#> ℹ Version: "2.0.0"
layer_attributes_get_names(wfs, layer = "mediseh_zostera_m_pnt")
#> [1] "id"       "country"  "the_geom"
layer_attribute_inspect(
  wfs, layer = "mediseh_zostera_m_pnt",
  attribute = "country"
)
#> # A tibble: 7 × 3
#>   .            n percent
#>   <chr>    <int>   <dbl>
#> 1 Croazia      4  0.0741
#> 2 Francia      1  0.0185
#> 3 Italia      30  0.556 
#> 4 Libia        2  0.0370
#> 5 Slovenia     8  0.148 
#> 6 Spagna       8  0.148 
#> 7 Tunisia      1  0.0185
```
