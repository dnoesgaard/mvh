# mvh (My Virtual Herbarium)

The **`mvh`** R package helps you assemble and organize virtual herbaria. It provides functions to search for specimen metadata and download associated images from the GBIF dataset.

## Installation

To install the package from GitHub, run:

```r
devtools::install_github("tncvasconcelos/mvh")
```

## Usage

### Example 1: Search and Download Specimens

Search up to 8 specimens of the blueberry genus *Vaccinium* from the Ann Arbor, MI area and download the images.

```r
# Search for specimen metadata
metadata <- search_specimen_metadata(
  taxon_name = "Vaccinium",
  coordinates = c(42.28, -83.74),
  limit = 8
)

# Download specimen images
download_specimen_images(
  metadata,
  dir_name = "Vaccinium_in_AnnArbor_example/specimens",
  result_file_name = "Vaccinium_in_AnnArbor_example/result_download"
)
```

![Figure 1: A) Example of a mvh pipeline to search and download up to eight specimens (“limit=8”) of the blueberry genus Vaccinium (Ericaceae) from the Ann Arbor (MI, USA) area (“coordinates = c(42.28, -83.74)”). B) Specimens’ images downloaded as a result of the pipeline. C) Message reminding the user to acknowledge collections where specimens are deposited if they are used in publications.](https://i.imgur.com/Rem46MQ.png)

### Example 2: Search and Plot Specimens

Search up to 100 specimens of *Myrcia splendens* and plot the number of specimens by institution and country.

```r
# Search for specimen metadata
metadata <- search_specimen_metadata(
  taxon_name = "Myrcia splendens",
  limit = 100
)

# Plot data
pdf("plots_for_mvh_ms.pdf", height = 5, width = 10)
par(mfrow = c(1, 2))
plot_specimens_by_institution(metadata)
plot_specimens_by_country(metadata)
dev.off()
```
![Figure 2: Example of a mvh pipeline to search up to 100 specimens (limit=”100”) of the widespread species Myrcia splendens (Myrtaceae) and plot the number of specimens per institution and country.](https://i.imgur.com/5vc7jfJ.png)


## Function Details

- **`search_specimen_metadata`**: 
  - Searches GBIF for specimen records based on taxon and/or geography.
  - Arguments:
    - `taxon_name`: Scientific name of the species.
    - `coordinates`: Latitude and longitude for geography-based searches.
    - `buffer_distance`: Size of the geographic search area.
    - Other `rgbif::occ_search` arguments are supported.

- **`download_specimen_images`**: 
  - Downloads images from URLs provided in the `media_url` column of the metadata.
  - Arguments:
    - `dir_name`: Directory name for saving images.
    - `result_file_name`: Name of the results spreadsheet.
    - `resize`: Resize images to a percentage of the original size (1-100).
    - `timeout_limit`: Time in seconds to wait before a download fails.

### Plotting Functions

The package **`mvh`** also includes two plotting functions to visualize components of the metadata associated with the search:

- **`plot_specimens_by_country`**: Displays a bar plot showing the number of specimens collected in each country.
- **`plot_specimens_by_institution`**: Displays a bar plot showing the number of specimens deposited in each institution, often following herbarium acronyms according to Thiers (continuously updated).

Both functions take the data.frame resulting from the `search_specimen_metadata` function and create bar plots in decreasing order of the number of specimens in each category.

## Acknowledgments

Please remember to acknowledge the collections where the images come from if they are used in publications.

---