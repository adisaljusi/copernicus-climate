# Reanalysis

Climate reanalysis combines former observations that were recorded with today's weather model. This model also processes overlapping or missing records to generate a consistent time series of climate data.[^1]

## Downloading Datasets

There a two approaches how someone can download the datasets.

1. Downloading via [CDS Copernicus (Climate Data Store)](https://cds.climate.copernicus.eu/cdsapp#!/search?type=dataset) (requires a user account).
2. [CDS API](https://cds.climate.copernicus.eu/api-how-to). There's also an official [Python API](https://github.com/ecmwf/cdsapi)

[^1]: https://climate.copernicus.eu/climate-reanalysis

# Knowledgebase

## Projection of NetCDF files from Copernicus

If you tried to do any plotting or zonal statistics on NetCDF datasets from Copernicus, you may discovered that the projection is based on a regular latitude-longitude grid. If you have not specified the region/area when downloading the dataset, you will quickly realize that the bouding box is `[90, 0, -90, 360]`. You can manually specify the region when downloading the dataset. As a result, you get correct lat/long values without needing to convert the values in the dataset.

For the Python API, there is also a parameter, which you can specify. Here is a sample request.

```python
import cdsapi

c = cdsapi.Client()

c.retrieve(
    "reanalysis-era5-single-levels",
    {
        "product_type": "reanalysis",
        "variable": "2m_temperature",
        "year": "2022",
        "month": "01",
        "day": [
            "01",
        ],
        "time": [
            "00:00",

        ],
        "area": [
            90,
            -180,
            -90,
            180,
        ],
        "format": "netcdf",
    },
    "download.nc",
)
```
