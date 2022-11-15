# FInal-Project-STAT447-846
Explore R packages for better visualization 













# Creating interactive Spatial Maps

# load packages

install.packages("leaflet") 

library(leaflet)


# Plot map of the world

A map can be plotted using addTiles()function as shown in the following examples 

# Map of the world

map <- leaflet() %>%
  addTiles() # use the default base map which is OpenStreetMap tiles
map


# locate Saskatoon on the map of the world

map_saskatoon <- map %>%
  setView(-106.631401, 52.132854, zoom = 10)
map_saskatoon

# Change type of map 

The type of map can be changed using addProviderTiles()function 

map %>% addProviderTiles(providers$Esri.DeLorme) # Esri.DeLorme tiles


# Zoom in on U of S on the map of the world

map_uofs <- leaflet() %>%
  addTiles() %>% 
  addMarkers(lng=-106.631401, lat=52.132854, 
             popup="U of S")
map_uofs


# To add point location to map

Point locations of known places can be added to a map using addMarkers() function. For example let us add "Place Riel Student Centre" with longtude -106.636353° and Latitude 52.130719° 

# Add a point location
map_Marker <- map %>%
  addMarkers(lng=-106.636353, lat=52.130719, popup="Place Riel Student Centre")

map_Marker


# Add a popup window 

More details about the added point location can be added using the addPopups() function

content <- paste(sep = "<br/>",
                 "Place Riel Student Centre",
                 "U of S, Saskatoon",
                 "Canada")

map_Marker %>%
  addPopups(lng=-106.636353, lat=52.130719, content,
            options = popupOptions(closeButton = FALSE))


# Add several point locations in a dataset

Several point locations from a dataset (quakes dataset)with can also be plotted.    

# Load quakes dataset
head(quakes)
str(quakes)

# plot first 30 rows 

data(quakes)

leaflet(data = quakes[1:30,]) %>% addTiles() %>%
  addMarkers(~long, ~lat, popup = ~as.character(mag), label = ~as.character(mag))

