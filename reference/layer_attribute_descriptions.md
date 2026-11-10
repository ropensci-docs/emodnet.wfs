# Variables available in a dataset (layer) from a data source (service).

Get layer attribute description

## Usage

``` r
layer_attribute_descriptions(
  wfs = NULL,
  service = NULL,
  service_version = NULL,
  layer
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

## Value

data.frame containing layer attribute descriptions (metadata).

## See also

Attributes metadata:
[`layer_attribute_inspect()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attribute_inspect.md),
[`layer_attributes_get_names()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_get_names.md),
[`layer_attributes_summarise()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_summarise.md),
[`layer_attributes_tbl()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_tbl.md)

## Examples

``` r
layer_attribute_descriptions(
  service = "biology",
  layer = "mediseh_zostera_m_pnt"
)
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Emodnetbio/wfs"
#> ℹ Version: "2.0.0"
#>       name      type minOccurs maxOccurs nillable geometry
#> 1       id   integer         0         1     TRUE    FALSE
#> 2  country character         0         1     TRUE    FALSE
#> 3 the_geom     Point         0         1     TRUE     TRUE
```
