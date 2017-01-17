### NOAA-Data-Collection-via-R
#Collecting information from NOAA via R and rnoaa package

install.packages("rnoaa")
install.packages("ghcnd") ##doesn't work for 3.3.1
install.packages("purrr")

library(rnoaa, purrr)

#Station ID is obtained via the website (http://www.ncdc.noaa.gov/cdo-web/search)
#NOTE: FROM rnoaa NOTES THEMSELVES: "Note that NOAA NCDC API calls can take a long time depending on the call.  The NOAA API
#doesn’t perform well with very long timespans, and will time out and make you angry"

#rnoaa_attributes doesn't work. but ncdc_attributes does. This tells me what all the datasetid's are 
#and their relevant flags
vignette("ncdc_attributes", "rnoaa")

For test reference, we are using Chicago.
##Chicago's Station id is US170006
## OHare station is: USW00094846

#helpful hints
ncdc_datacats(limit = 42) ##checks to see what datatpes you can pull

##Checking what datatypeids I can get
types <- ncdc(datasetid = "GHCND",
              locationid = "CITY:US170006",
              token = "EdVgOtsIZpIgAymjONKSSEiCjFWuPeLU",
              startdate = "2015-05-01", enddate = "2015-05-10",
              datatypeid = NULL,
              limit = 1000)

##pulling Chicago weather data
out <- ncdc(datasetid = "GHCND", stationid = c("GHCND:US170006"), 
     startdate = "2015-01-31", enddate = "2015-02-15", 
     datatypeid = c("PRCP", "TMAX", "TMIN", "TAVG", "SNOW") ,
     token = "EdVgOtsIZpIgAymjONKSSEiCjFWuPeLU",
     limit = 1000)
head(out$data, 25)
write.csv(out$data, "2015.12.csv")

chi_test <- ncdc(datasetid = "GHCND", stationid = chi_stations$data$id, 
            startdate = "2015-01-01", enddate = "2015-01-15", 
            datatypeid = c("PRCP", "TMAX", "TMIN", "TAVG") ,
            token = "EdVgOtsIZpIgAymjONKSSEiCjFWuPeLU",
            limit = 1000)
dim(out12$data)
write.csv(out99$data, "2015.1.csv")

outs <- rbind(out12$data, out34$data,
              out56$data, out78$data,
              out91$data, out99$data)

##Testing to see if I can retrive data
##ncdc_stations pulls out a list of location stations, radius can be specified
chi_stations <- ncdc_stations(datasetid='GHCND',
            startdate = '2014-07-30', enddate = '2014-07-31', 
            datatypeid = NULL,
            token = "EdVgOtsIZpIgAymjONKSSEiCjFWuPeLU",
            locationid = "CITY:US170006")
chi_stations$data$id

#another test, why can't I Get data (thought: timeline is too long)
umm <- ncdc(datasetid='GHCND', locationid = 'ZIP:60606', 
            startdate = '2015-08-01', enddate = '2015-08-31',
            token = "EdVgOtsIZpIgAymjONKSSEiCjFWuPeLU" )

#Leaving datatypeid blank so I can see what kinds of datatypes I can get
test <- ncdc(datasetid = "GHCND", stationid = "GHCND:USW00094846", 
     startdate = "2014-08-01", enddate = "2014-08-01", 
     datatypeid = NULL,
     token = "EdVgOtsIZpIgAymjONKSSEiCjFWuPeLU", 
     limit = 500)

#Looking at Normal Daily data, but it only exists until 2010
ncdc(datasetid = "NORMAL_DLY",stationid='GHCND:USW00014895',
     startdate = "2010-01-01", enddate = "2010-01-31", 
     datatypeid = "dly-tmax-normal")
     
 
