# Which data sources (services) are available?

Available EMODnet Web Feature Services

## Usage

``` r
emodnet_wfs()
```

## Format

### `emodnet_wfs`

- emodnet_thematic_lot:

  EMODnet disciplinary themes - bathymetry, biology, chemistry, geology,
  human activities, physics and seabed habitats

- service_name:

  Name of the specific service. Use in
  [emodnet_init_wfs_client](https://docs.ropensci.org/emodnet.wfs/reference/emodnet_init_wfs_client.md).

- service_url:

  [Web Feature Service (WFS)](https://www.ogc.org/standards/wfs/) URL
  endpoint for accessing the service.

## Value

Tibble of available EMODnet Web Feature Services

## Examples

``` r
emodnet_wfs()
#> # A tibble: 17 × 3
#>    emodnet_thematic_lot     service_name                             service_url
#>    <chr>                    <chr>                                    <chr>      
#>  1 EMODnet Bathymetry       bathymetry                               https://ow…
#>  2 EMODnet Biology          biology                                  https://ge…
#>  3 EMODnet Biology          biology_occurrence_data                  https://ge…
#>  4 EMODnet Chemistry        chemistry_cdi_data_discovery_and_access… https://ge…
#>  5 EMODnet Chemistry        chemistry_cdi_distribution_observations… https://ge…
#>  6 EMODnet Chemistry        chemistry_contaminants                   https://ge…
#>  7 EMODnet Chemistry        chemistry_marine_litter                  https://ww…
#>  8 EMODnet Geology          geology_coastal_behavior                 https://dr…
#>  9 EMODnet Geology          geology_events_and_probabilities         https://dr…
#> 10 EMODnet Geology          geology_marine_minerals                  https://dr…
#> 11 EMODnet Geology          geology_sea_floor_bedrock                https://dr…
#> 12 EMODnet Geology          geology_seabed_substrate_maps            https://dr…
#> 13 EMODnet Geology          geology_submerged_landscapes             https://dr…
#> 14 EMODnet Human Activities human_activities                         https://ow…
#> 15 EMODnet Physics          physics                                  https://pr…
#> 16 EMODnet Seabed Habitats  seabed_habitats_general_datasets_and_pr… https://ow…
#> 17 EMODnet Seabed Habitats  seabed_habitats_individual_habitat_map_… https://ow…
```
