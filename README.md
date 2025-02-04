# ALFAM2-data
The ALFAM2 dataset on ammonia loss from field-applied manure. This repository contains the **"ALFAM2 dataset"**, the code used to generate it from data files submitted by researchers who made the emission measurements, and those original data files. The repository serves at least two purposes: data, progress, and code tracking (for dataset developers) and version control (primarily for dataset users). 

# Quick tips
* Look in [data-output/03](https://github.com/sashahafner/ALFAM2-data/tree/master/data-output/03) for the latest version of the **ALFAM2 dataset**. Typically it makes sense to use the version available in the latest [release](https://github.com/sashahafner/ALFAM2-data/releases), which will also correspond to a [version available through Zenodo](https://zenodo.org/search?page=1&size=20&q=alfam2). 
* For more details on the ALFAM2 project, and access to project products see <http://alfam.dk>
* For a database interface that can be used to subset (filter) by country, application method, or more, use this web app: <https://biotransformers.shinyapps.io/ALFAM2/>. 
* Looking for the ALFAM2 model R package? You want the ALFAM2 repo: <https://github.com/sashahafner/ALFAM2>.
* Zenodo versions can be found [here](https://zenodo.org/search?page=1&size=20&q=alfam2)

# More details
The dataset consists of two files: one with plot- and one with measurement-level observations.
See the `headers` directory [here](https://github.com/sashahafner/ALFAM2-data/tree/master/headers) for variable descriptions.
Files can be merged on the two plot keys or identification codes: `pid` and `pmid`.

Files are saved in a compressed format with the extension `.gz` (gzip) in order to reduce file size.
The easiest way to get the data into R is to read the files directly with `data.table::fread()`.
Alternatively, various utilies can be used to extract (unzip) the files, which are regular comma-separated ASCII text files.

The ALFAM2 data are organized into `uptake` periods: 1 is for the original ALFAM work, 2 for the work described in [this paper](https://doi.org/10.1016/j.agrformet.2017.11.027), and 3 for the current effort to expand the database.
The latest version will always be in the highest number (3 currently).
Earlier versions are saved to facilitate addition of data without rebuilding older dataset versions while maintaining the option for revising data submitted in an earlier uptake period.

See the `Data handling tips` below for more information on working with the data.

# Citations
The best way to refer to this work if you use the data in a publication is to cite the [version available through Zenodo](https://zenodo.org/search?page=1&size=20&q=alfam2).
In addition to a doi, this Zenodo version includes an author list.
Alternatively, individual [releases](https://github.com/sashahafner/ALFAM2-data/releases) can be cited.
In either case, be sure to **note the version number used** in any citation.
If you have used a version not included in a release or a Zenodo dataset, please contact me ([here](https://sites.google.com/hafnerconsulting.com/hafnerconsulting/contact) or [here](https://au.dk/sasha.hafner@bce))and I will create the necessary release or dataset.
Authors may also want to cite (and read!) [this paper](https://doi.org/10.1016/j.agrformet.2017.11.027).
But again, include the dataset version number in any citation.
You can find the dataset version number in the release tags or in a text file here: [data-output/03/data_version.txt](https://github.com/sashahafner/ALFAM2-data/tree/master/data-output/03/data_version.txt).

# References
For a description of the dataset, see this paper: <https://doi.org/10.1016/j.agrformet.2017.11.027>. For the ALFAM2 model for ammonia emission, with parameter estimation based on the ALFAM2 dataset, see this paper: <https://doi.org/10.1016/j.agrformet.2017.11.027>. 

# Data handling tips
The simplest way to load the data in R is with the `fread()` function from the data.table package.

```
idat <- data.table::fread('ALFAM2_interval.csv.gz')
pdat <- data.table::fread('ALFAM2_plot.csv.gz')
```

Once these two data frames (tables) are created, they can be combined (if needed) with `base::merge()` or `data.table::merge()` function.

```
cdat <- merge(idat, pdat, by = c('pid', 'pmid'))
```

(The `by` argument is optional here, but it is good practice to be aware of the columns used for merging.)

In Python, the `read_csv()` function from the pandas package can be used to read the compressed files directly.

```
import pandas as pd

idat = pd.read_csv('ALFAM2_interval.csv.gz')
```

For some more information, see the `analysis` directory.

# Submitting data
To inquire about submitting data to the ALFAM2 dataset, send a message to `sasha.hafner AT bce.au.dk` through email or else used [this form](https://sites.google.com/hafnerconsulting.com/hafnerconsulting/contact?authuser=0).

# Checking data
To check submitted data, find your completed template file in [this list](https://sashahafner.github.io/ALFAM2-data/) and follow the instructions you will see at the top of the linked file.
