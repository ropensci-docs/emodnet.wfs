# Possible values of variables (attributes) in a dataset (layer) from a data source (service).

Get layer attribute values tibble

## Usage

``` r
layer_attributes_tbl(wfs = NULL, service = NULL, service_version = NULL, layer)
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

## Value

tibble of layer attribute (variable) values with geometry column
removed.

## Details

Request excluding spatial information can be significantly faster. Can
be useful for inspecting attribute values and constructing feature
filters for more targeted and faster layer download.

## See also

Attributes metadata:
[`layer_attribute_descriptions()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attribute_descriptions.md),
[`layer_attribute_inspect()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attribute_inspect.md),
[`layer_attributes_get_names()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_get_names.md),
[`layer_attributes_summarise()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_summarise.md)

## Examples

``` r
layer_attributes_tbl(service = "biology", layer = "mediseh_zostera_m_pnt")
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Emodnetbio/wfs"
#> ℹ Version: "2.0.0"
#> # A tibble: 54 × 3
#>    gml_id                      id country
#>    <chr>                    <int> <chr>  
#>  1 mediseh_zostera_m_pnt.1      0 Spagna 
#>  2 mediseh_zostera_m_pnt.2      0 Spagna 
#>  3 mediseh_zostera_m_pnt.3      0 Spagna 
#>  4 mediseh_zostera_m_pnt.4      0 Spagna 
#>  5 mediseh_zostera_m_pnt.5      0 Spagna 
#>  6 mediseh_zostera_m_pnt.6      0 Spagna 
#>  7 mediseh_zostera_m_pnt.7      0 Spagna 
#>  8 mediseh_zostera_m_pnt.8      0 Francia
#>  9 mediseh_zostera_m_pnt.9      0 Italia 
#> 10 mediseh_zostera_m_pnt.10     0 Italia 
#> # ℹ 44 more rows
```
