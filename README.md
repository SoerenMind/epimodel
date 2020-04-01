# Epidemics data processing and modelling toolkit

A data library and a toolkit for modelling COVID-19 epidemics.

## Main concepts

* Region database (continents, countries, provinces, GLEAM basins) - codes, names, basic stats.
* All data, including the region database, is stored in epimodel-covid-data repo for asynchronous updates.
* Each region has an ISO-based code, all data is organized in rows by those codes.
* Built on Pandas, storing CSVs and HDF5. Easy loading and export of data groups.
* Supports plain columns and date-series column sets (via column `MultiIndex`).
* Auxiliary `Region` 

## Install

* [Get Poetry](https://python-poetry.org/docs/#installation)
* Clone this repository.
* Install the dependencies and this lib `poetry install` (creates a virtual env by default).
* Clone the [](https://github.com/epidemics/epimodel-covid-data/) repository. (For convenience, the default paths assume it is cloned inside the `epimodel` repo directory.)

## Basic usage

```python
import epimodel
from datetime import date

# Read regions
rds = epimodel.RegionDataSet.from_csv('epimodel-covid-data/regions.csv')
# Add John Hopkins dataset
rds.read_csv('epimodel-covid-data/JH.csv')
# Plan columns are in `rds.data`, dated columns in `rds.series`
print(rds.data.loc['CZ', 'B_Population'])
print(rds.series.loc['CZ', 'JH_Confirmed'][date(2020, 3, 25)])
# Use region attribute access for reading (writing is WIP)
print(cz.Name)
# Find by name or by code
cz = rds['CZ']
cz = rds.find_one_by_name('Czech Republic')
```

## Development

* Use Poetry for dependency management.
* We enforce [black](https://github.com/psf/black) formatting (with the default style).
* Use `pytest` for testing, add tests to your code.
* Use pull requests for both this and the data repository.
