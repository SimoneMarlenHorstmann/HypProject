
#### Table of Contents

- [I. Data overview](#data)
- [II. Data Analysis](#ana)




-----------

<h1 id="data"> I. Data overview </h1> 


--------------------------------------------------------------------------------------------------------------------------------------------

<h1 id="data">II. Data Analysis</h1>



<img src="/images/heatmap_ani32_100_100.gif" align="right" width="600px"/>


## I.I Input -  Cloud optical depth (COD) 

### Input data info:
- from satellite images taken above western germany (will be extended to whole germany)
- with a spatial resolution of 2km x 1km and
- time resultion of 5 min
- starting 6am to 4.55pm

Cloud optical depth derived
- by ... algorithm
- combines different channels
- 

<br/><br/>

<br/><br/>




## I.II Output - Irradiance Measurements

### Data Info
- 10-minute station observations of solar and sunshine for Germany
- Version: v24.03
- Publication date: 2024-03-29
- Avaiable from: https://opendata.dwd.de/climate_environment/CDC/observations_germany/climate/10_minutes/solar/historical/

Data used:
GS_10 : sum of global radiation during the previous 10 minutes
- Unit = $J/cm^2$
- Missing_values=- 999 (deleted in preproccessing)
- Quality control procedure applied:  QN = 3 (automatic control and correction)

Quality check and uncertainty assessment routines are explained in Kaspar et al., 2013. In addition to automated tests that check completeness, temporal and spatial consistency and compare them against statistical thresholds (QualiMet software, Spengler, 2002), an additional manual quality control is carried out.

<img src="/images/docs/stations_overview.png" width="1020px"/>



But currently only COD above Juelich:



<img src="/images/docs/Stations_aboveJuelich.png" width="900px"/>

# I.II Combined Data:

<br/><br/>

<img src="/images/docs/mean_cod_heatmap_withstations.png" width="900px"/>
