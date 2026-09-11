# Names of variables (attributes) available from a dataset (layer) in a data source (service).

Names of variables (attributes) available from a dataset (layer) in a
data source (service).

## Usage

``` r
layer_attributes_get_names(
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

character vector of layer attribute (variable) names.

## See also

Attributes metadata:
[`layer_attribute_descriptions()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attribute_descriptions.md),
[`layer_attribute_inspect()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attribute_inspect.md),
[`layer_attributes_summarise()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_summarise.md),
[`layer_attributes_tbl()`](https://docs.ropensci.org/emodnet.wfs/reference/layer_attributes_tbl.md)

## Examples

``` r
layer_attributes_get_names(
  service = "biology",
  layer = "mediseh_zostera_m_pnt"
)
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Emodnetbio/wfs"
#> ℹ Version: "2.0.0"
#> [1] "id"       "country"  "the_geom"
```
