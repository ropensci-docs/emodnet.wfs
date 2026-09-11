# Get EMODnet WFS datasets (layers)

Performs an WFS getFeature request for layers from a `wfs` object or
specified EMODnet Service. Filtering of layer features can also be
handled via ECQL language filters.

## Usage

``` r
emodnet_get_layers(
  wfs = NULL,
  service = NULL,
  service_version = NULL,
  layers,
  crs = NULL,
  cql_filter = NULL,
  simplify = FALSE,
  reduce_layers = deprecated(),
  ...
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

- layers:

  a character vector of layer names. To get info on layers, including
  `layer_name` use
  [`emodnet_get_wfs_info()`](https://docs.ropensci.org/emodnet.wfs/reference/emodnet_get_wfs_info.md).

- crs:

  integer. EPSG code for the output crs. If `NULL` (default), layers are
  returned with original crs.

- cql_filter:

  character. Features returned can be filtered using valid Extended
  Common Query Language (ECQL) filtering statements
  (<https://docs.geoserver.org/stable/en/user/filter/ecql_reference.html>).
  Should be one of:

  - character string or character vector of length 1. Filter will be
    recycled across all layers requested.

  - character vector of length equal to the length of layers. Filter
    will be matched to layers sequentially. Elements containing `NA` are
    ignored

  - named character vector. Each filter will be applied to the layer
    corresponding to the filter name. Filters with names that do not
    correspond to any layers are ignored. Layers without corresponding
    filters are returned whole.

- simplify:

  whether to reduce output layers to a single `sf` object. This only
  works if the column names are the same.

- reduce_layers:

  **\[deprecated\]** use `simplify`.

- ...:

  additional vendor parameter arguments passed to
  [`ows4R::GetFeature()`](https://docs.geoserver.org/stable/en/user/services/wfs/reference.html#getfeature).
  For example, including `count = 1` returns the first available
  feature. Or `outputFormat = "CSV"` (or `outputFormat = "JSON"`) might
  help downloading bigger datasets.

## Value

If `simplify = FALSE` (default), a list of `sf` objects, one element for
each layer. Any layers for which download was unsuccessful will be NULL.
If `simplify = TRUE`, all layers are reduced (if possible: if all column
names are the same) to a single `sf` containing data for all layers.
`NULL` layers are ignored. `simplify = TRUE` can also be used to return
an `sf` out of a single layer request instead of a list of length 1.

## Big downloads

If a layer is really big (like `"abiotic_observations"` of the
`"biology_occurrence_data"` service), you might consider a combination
of these ideas:

- using
  [`outputFormat = "CSV"`](https://docs.geoserver.org/stable/en/user/services/wfs/reference.html#getfeature);

- filtering using
  [`cql_filters`](https://docs.ropensci.org/emodnet.wfs/articles/ecql_filtering.html)
  or [bounding
  boxes](https://docs.ropensci.org/emodnet.wfs/articles/request-params.html#limit-spatial-extent-using-a-boundary-box)
  (possibly splitting the area of interests into several requests);

- Using [EMODnet's download
  toolbox](https://emodnet.ec.europa.eu/geoviewer/).

## Examples

``` r
# Layers as character vector
emodnet_get_layers(
  service = "biology",
  layers = c("mediseh_zostera_m_pnt", "mediseh_posidonia_nodata")
)
#> Loading ISO 19139 XML schemas...
#> Loading ISO 19115-3 XML schemas...
#> Loading ISO 19139 codelists...
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Emodnetbio/wfs"
#> ℹ Version: "2.0.0"
#> $mediseh_zostera_m_pnt
#> Simple feature collection with 54 features and 3 fields
#> Geometry type: POINT
#> Dimension:     XY
#> Bounding box:  xmin: -4.167154 ymin: 33.07783 xmax: 15.35766 ymax: 45.72451
#> Geodetic CRS:  WGS 84
#> First 10 features:
#>                      gml_id id country                   the_geom
#> 1   mediseh_zostera_m_pnt.1  0  Spagna  POINT (-2.61314 36.71681)
#> 2   mediseh_zostera_m_pnt.2  0  Spagna POINT (-3.846598 36.75127)
#> 3   mediseh_zostera_m_pnt.3  0  Spagna POINT (-3.957785 36.72266)
#> 4   mediseh_zostera_m_pnt.4  0  Spagna POINT (-4.039712 36.74217)
#> 5   mediseh_zostera_m_pnt.5  0  Spagna POINT (-4.100182 36.72331)
#> 6   mediseh_zostera_m_pnt.6  0  Spagna POINT (-4.167154 36.71226)
#> 7   mediseh_zostera_m_pnt.7  0  Spagna POINT (-1.268366 37.55796)
#> 8   mediseh_zostera_m_pnt.8  0 Francia   POINT (4.84864 43.37637)
#> 9   mediseh_zostera_m_pnt.9  0  Italia  POINT (13.71831 45.70017)
#> 10 mediseh_zostera_m_pnt.10  0  Italia  POINT (13.16378 45.72451)
#> 
#> $mediseh_posidonia_nodata
#> Simple feature collection with 465 features and 3 fields
#> Geometry type: MULTICURVE
#> Dimension:     XY
#> Bounding box:  xmin: -2.1798 ymin: 30.26623 xmax: 34.60767 ymax: 45.47668
#> Geodetic CRS:  WGS 84
#> First 10 features:
#>                         gml_id id         km                       the_geom
#> 1   mediseh_posidonia_nodata.1  0 291.503233 MULTICURVE (LINESTRING (27....
#> 2   mediseh_posidonia_nodata.2  0  75.379502 MULTICURVE (LINESTRING (23....
#> 3   mediseh_posidonia_nodata.3  0  38.627764 MULTICURVE (LINESTRING (22....
#> 4   mediseh_posidonia_nodata.4  0 110.344802 MULTICURVE (LINESTRING (19....
#> 5  mediseh_posidonia_nodata.13  0  66.997461 MULTICURVE (LINESTRING (9.1...
#> 6  mediseh_posidonia_nodata.14  0  18.090640 MULTICURVE (LINESTRING (9.7...
#> 7  mediseh_posidonia_nodata.15  0  16.618978 MULTICURVE (LINESTRING (9.8...
#> 8  mediseh_posidonia_nodata.16  0   1.913773 MULTICURVE (LINESTRING (10....
#> 9  mediseh_posidonia_nodata.83  0   2.173447 MULTICURVE (LINESTRING (15....
#> 10 mediseh_posidonia_nodata.84  0   2.817453 MULTICURVE (LINESTRING (15....
#> 


# Usage of cql_filter
emodnet_get_layers(
  service = "biology",
  layers = "mediseh_zostera_m_pnt",
  cql_filter = "country = 'Francia'"
)
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Emodnetbio/wfs"
#> ℹ Version: "2.0.0"
#> $mediseh_zostera_m_pnt
#> Simple feature collection with 1 feature and 3 fields
#> Geometry type: POINT
#> Dimension:     XY
#> Bounding box:  xmin: 4.84864 ymin: 43.37637 xmax: 4.84864 ymax: 43.37637
#> Geodetic CRS:  WGS 84
#>                    gml_id id country                 the_geom
#> 1 mediseh_zostera_m_pnt.8  0 Francia POINT (4.84864 43.37637)
#> 
# Usage of vendor parameter
emodnet_get_layers(
  service = "biology",
  layers = "mediseh_zostera_m_pnt",
  count = 1
)
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Emodnetbio/wfs"
#> ℹ Version: "2.0.0"
#> $mediseh_zostera_m_pnt
#> Simple feature collection with 1 feature and 3 fields
#> Geometry type: POINT
#> Dimension:     XY
#> Bounding box:  xmin: -2.61314 ymin: 36.71681 xmax: -2.61314 ymax: 36.71681
#> Geodetic CRS:  WGS 84
#>                    gml_id id country                  the_geom
#> 1 mediseh_zostera_m_pnt.1  0  Spagna POINT (-2.61314 36.71681)
#> 

# Usage of csv output
data <- emodnet_get_layers(
    service = "biology_occurrence_data",
    layers = "abiotic_observations",
    outputFormat = "CSV"
)
#> ✔ WFS client created successfully
#> ℹ Service: "https://geo.vliz.be/geoserver/Dataportal/wfs"
#> ℹ Version: "2.0.0"
#> Rows: 1000000 Columns: 38
#> ── Column specification ────────────────────────────────────────────────────────
#> Delimiter: ","
#> chr  (13): FID, datatype, season, parametername, parameterunit, dataprovider...
#> dbl  (11): id, latitude, longitude, value, standardparameterid, dataprovider...
#> lgl  (13): aphiaid, depth, lod, loq, class, classunit, classcode, dateprecis...
#> dttm  (1): datetime
#> 
#> ℹ Use `spec()` to retrieve the full column specification for this data.
#> ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
str(data[["abiotic_observations"]])
#> spc_tbl_ [1,000,000 × 38] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
#>  $ FID                : chr [1:1000000] "abiotic_observations.fid--3483df66_1a090e88104_-6c21" "abiotic_observations.fid--3483df66_1a090e88104_-6c20" "abiotic_observations.fid--3483df66_1a090e88104_-6c1f" "abiotic_observations.fid--3483df66_1a090e88104_-6c1e" ...
#>  $ id                 : num [1:1000000] 8.41e+10 8.41e+10 8.41e+10 8.41e+10 8.41e+10 ...
#>  $ aphiaid            : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ latitude           : num [1:1000000] 51.4 51.4 51.4 51.4 51.4 ...
#>  $ longitude          : num [1:1000000] 3.38 3.38 3.38 3.38 3.38 ...
#>  $ depth              : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ datetime           : POSIXct[1:1000000], format: "2012-06-01 11:30:00" "2012-06-01 11:40:00" ...
#>  $ value              : num [1:1000000] 174 167 159 150 142 133 123 113 103 93 ...
#>  $ lod                : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ loq                : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ standardparameterid: num [1:1000000] 9679 9679 9679 9679 9679 ...
#>  $ dataproviderid     : num [1:1000000] 8 8 8 8 8 8 8 8 8 8 ...
#>  $ imisdatasetid      : num [1:1000000] 945 945 945 945 945 945 945 945 945 945 ...
#>  $ dataficheid        : num [1:1000000] 118 118 118 118 118 118 118 118 118 118 ...
#>  $ seriesid           : num [1:1000000] 17365 17365 17365 17365 17365 ...
#>  $ datatype           : chr [1:1000000] "NC" "NC" "NC" "NC" ...
#>  $ class              : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ classunit          : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ classcode          : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ season             : chr [1:1000000] "spring" "spring" "spring" "spring" ...
#>  $ parametername      : chr [1:1000000] "10 minuten gemiddelde waterhoogte in cm+NAP" "10 minuten gemiddelde waterhoogte in cm+NAP" "10 minuten gemiddelde waterhoogte in cm+NAP" "10 minuten gemiddelde waterhoogte in cm+NAP" ...
#>  $ parameterunit      : chr [1:1000000] "cm +NAP" "cm +NAP" "cm +NAP" "cm +NAP" ...
#>  $ dataprovider       : chr [1:1000000] "RWS - Rijkswaterstaat" "RWS - Rijkswaterstaat" "RWS - Rijkswaterstaat" "RWS - Rijkswaterstaat" ...
#>  $ datasettitle       : chr [1:1000000] "MWTL physical monitoring network Westerschelde: Water Levels" "MWTL physical monitoring network Westerschelde: Water Levels" "MWTL physical monitoring network Westerschelde: Water Levels" "MWTL physical monitoring network Westerschelde: Water Levels" ...
#>  $ datafichetitle     : chr [1:1000000] "S-HD-N-001 -  Waterstanden - Getij" "S-HD-N-001 -  Waterstanden - Getij" "S-HD-N-001 -  Waterstanden - Getij" "S-HD-N-001 -  Waterstanden - Getij" ...
#>  $ stationname        : chr [1:1000000] "Cadzand, 2" "Cadzand, 2" "Cadzand, 2" "Cadzand, 2" ...
#>  $ gid                : num [1:1000000] 9 9 9 9 9 9 9 9 9 9 ...
#>  $ seasonid           : num [1:1000000] 2 2 2 2 2 2 2 2 2 2 ...
#>  $ unit               : chr [1:1000000] "cm +NAP" "cm +NAP" "cm +NAP" "cm +NAP" ...
#>  $ category           : chr [1:1000000] "waterstand, golven en stroming" "waterstand, golven en stroming" "waterstand, golven en stroming" "waterstand, golven en stroming" ...
#>  $ the_geom           : chr [1:1000000] "POINT (51.379298 3.376275)" "POINT (51.379298 3.376275)" "POINT (51.379298 3.376275)" "POINT (51.379298 3.376275)" ...
#>  $ valuesign          : chr [1:1000000] "=" "=" "=" "=" ...
#>  $ dateprecision      : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ standard_name      : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ externalid         : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ external_name      : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ scientificname     : logi [1:1000000] NA NA NA NA NA NA ...
#>  $ abmpbm             : logi [1:1000000] NA NA NA NA NA NA ...
#>  - attr(*, "spec")=
#>   .. cols(
#>   ..   FID = col_character(),
#>   ..   id = col_double(),
#>   ..   aphiaid = col_logical(),
#>   ..   latitude = col_double(),
#>   ..   longitude = col_double(),
#>   ..   depth = col_logical(),
#>   ..   datetime = col_datetime(format = ""),
#>   ..   value = col_double(),
#>   ..   lod = col_logical(),
#>   ..   loq = col_logical(),
#>   ..   standardparameterid = col_double(),
#>   ..   dataproviderid = col_double(),
#>   ..   imisdatasetid = col_double(),
#>   ..   dataficheid = col_double(),
#>   ..   seriesid = col_double(),
#>   ..   datatype = col_character(),
#>   ..   class = col_logical(),
#>   ..   classunit = col_logical(),
#>   ..   classcode = col_logical(),
#>   ..   season = col_character(),
#>   ..   parametername = col_character(),
#>   ..   parameterunit = col_character(),
#>   ..   dataprovider = col_character(),
#>   ..   datasettitle = col_character(),
#>   ..   datafichetitle = col_character(),
#>   ..   stationname = col_character(),
#>   ..   gid = col_double(),
#>   ..   seasonid = col_double(),
#>   ..   unit = col_character(),
#>   ..   category = col_character(),
#>   ..   the_geom = col_character(),
#>   ..   valuesign = col_character(),
#>   ..   dateprecision = col_logical(),
#>   ..   standard_name = col_logical(),
#>   ..   externalid = col_logical(),
#>   ..   external_name = col_logical(),
#>   ..   scientificname = col_logical(),
#>   ..   abmpbm = col_logical()
#>   .. )
#>  - attr(*, "problems")=<pointer: 0x559956da8b00> 
```
