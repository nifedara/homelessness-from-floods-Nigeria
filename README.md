# homelessness-from-floods-Nigeria

![Largest Homelessness from Flood in Nigeria](https://github.com/user-attachments/assets/39feb1dc-82a3-4778-9c87-e6348fa37c4c)

## About ##

This visualises 10 of the floods that rendered the most people homeless between 2000 and 2018 in Nigeria.


### 🔨 Analysis/Mapping tool 🔨 ###
QGIS (https://qgis.org/)

## 👩🏾‍💻 Data Sources 👩🏾‍💻 ##
1. Geocoded global disaster dataset: Geocoded Disasters (GDIS) dataset
2. Nigeria disaster dataset: Climate Knowledge Portal (World Bank)
3. Country: Natural Earth Data


## 🔨 How to Recreate 🔨 ##
Note: Assumes you have QGIS downloaded

### - Get the data required: ###
1. Download the 10m Admin_0_countries vector from:

```
https://www.naturalearthdata.com/downloads/10m-cultural-vectors/
```

2. Download the Nigeria disaster (2000-2018) from:

```
https://climateknowledgeportal.worldbank.org/
```

3. Download the geocoded global disaster (1960-2018) from:

```
https://www.earthdata.nasa.gov/data/catalog/sedac-ciesin-sedac-pend-gdis-1.00
```
### - Import the data: ###
#### - The countries vector: ####
- Load the admin_0_countries vector into QGIS
- From the toolbar, click `Select Features by Values`, and enter country as `Nigeria`
- Right-click on the admin_0_countries layer and save `Selected Features As`
- Remove the old layer (with all the countries), leaving the new layer with just `Nigeria`

#### - The global disaster dataset: ####
- Import the global disaster data as (Delimited Text - with Point coordinates). This dataset has all the global disasters with location coordinates
- From the toolbar, click `Select Features by Values`, enter country as `Nigeria`, year as `2000` (Greater than or equal to) and disaster type as `Flood`
- We did the above since this visualisation is only for floods in Nigeria between 2000 and 2018.
- Save the selected features and remove the old layer (the global disasters layer)
- This dataset now has the floods in Nigeria, but it doesn't have the impact values (e.g the number of people affected)

#### - The Nigeria disaster dataset: ####
- This dataset has the disaster impact but no coordinates
- Import this data as (Delimited Text - with No geometry). This loads it as a table only
- This dataset has a field that is the same as the global dataset, which is the disaster number (disasterno) field. This field is called DisNo in this dataset and disasterno in the global set, but both hold the same value
- The disaster number field of this dataset also varies in that it carries the country code (ISO3) as a suffix to the actual disaster number
- Use the `Left` function in `Field calculator` to remove the suffix `NGA`, making a new field `disasterno` that rhymes with the other dataset
 
#### - JOIN both datasets: ####
- We will join both datasets by field attribute, which can be found in the Processing Toolbar
- Join them on the common field, `disasterno`
- Now, we have one table that has all we need

#### - Handle duplicates: ####
- Using `Delete duplicates by attribute`, remove records with duplicate `disasterno`, as it can skew the result

#### - Symbology: ####
