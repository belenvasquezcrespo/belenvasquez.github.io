## Welcome to another page

# Origin and Destination of Care Trips
[back](./README.md)

The analysis of the origin and destination of care trips provided valuable insights into travel patterns within Guiuan, Philippine. The study examined the relationships between different regions, including the Urban and Rural Mainland, Calicoan Island, Tuababao Island, Manicani Island, Suluan Island, and Homonhon Island. The findings revealed interesting dynamics, with the Urban Mainland region emerging as a prominent source and recipient of care trips. This region displayed a high volume of care trips, attributed to factors such as population density, infrastructure, facilities, and economic activity. It also highlighted the significance of transportation hubs and markets as major attractors of care trips.

On the other hand, the islands under Guiuan's jurisdiction, such as Tuababao, Manicani, Homonhon, and Calicoan, exhibited fewer care trips, primarily limited to travel within their respective islands. This can be attributed to the scarcity of transportation alternatives and the considerable distance between the islands and the mainland. The lack of critical amenities on the islands also contributed to the restricted mobility of the local population, requiring them to travel to the mainland for essential tasks and access to facilities and services.

## Origin-destination of care by region
![Branching](/assets/projects-img/origin-destination-region.png)

### Chord Diagram with R Studio - Region
```r
# Load the circlize package
library(circlize)

# Create sample data
data <- matrix(c(22, 0, 1, 0, 0, 8, 0, 0, 0, 0, 0, 1, 0, 0, 71, 0, 2, 38, 0, 0, 0, 3, 0, 2, 0, 0, 0, 0, 30, 0, 7, 5, 32, 6, 8, 233), nrow = 6,
   dimnames = list(c("Caliocan I.", "Homonhon I.", "Rural M.", "Manicani I.", "Tubabao I.", "Urban M."), 
                   c("Caliocan I.", "Homonhon I.", "Rural M.", "Manicani I.", "Tubabao I.", "Urban M.")))

# Add self-links
diag(data) <- diag(data) / 2

# Create the chord diagram
chordDiagram(data, grid.col = 1:6, self.link = 1)

# Customize the chord diagram
## Gap between features
circos.par(gap.after = c( "Urban M." = 30, "Rural M."= 15, "Caliocan I."= 15, "Homonhon I."= 15, 
                          "Manicani I."= 15, "Tubabao I."= 15))
## Features order
chordDiagram(data, order = c("Urban M.", "Rural M.", "Caliocan I.", 
                             "Homonhon I.", "Tubabao I.", "Manicani I."))
## Features color
chordDiagram(data, grid.col = c("Urban M." = "#343779", "Rural M." = "#FC7643", 
                               "Caliocan I." = "#33A9AC", "Homonhon I." = "#DA2A47", "Manicani I." = "#A5CF61", 
                               "Tubabao I." = "#E9C46A", self.link = 1))

# Saving the plot (high definition)
dev.copy(jpeg,'plot.png', width=8, height=8, units="in", res=500)
dev.off()

# Reset chord diagram
circos.clear()
```

At the barangay level, a detailed analysis unveiled complex patterns of care-related travel. Concentration of care trips was observed in the urban area, particularly in barangays Pob. 4, Pob. 6, and Pob. 8, which also served as the top receivers of care trips. Trips within the same barangay were predominantly for daily living activities, while connections with other barangays were mainly for visiting relatives and school-related travel. Pob. 6 stood out for its dependence on the transportation terminal and market, where grocery shopping was the primary activity.

Interestingly, the study identified a shift in the perception of the urban area as a cohesive entity, referred to collectively as "Poblacion" by the respondents. This suggests a growing interconnectedness and blurring of boundaries between individual barangays within the urban area, likely influenced by urbanization and increased interactions between different parts of the city.

## Origin-destination of care by barangay (neighborhood)
![Branching](/assets/projects-img/origin-destination-barangay.png)

### Chord Diagram with R Studio - Barangay (neighborhood)
```r

# Load the circlize package
library(circlize)

# Create sample data
data_urb <- matrix(c(30, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 5, 0, 0, 0, 0, 0, 3, 
                 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 
                 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 18, 0, 0, 
                 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 
                 0, 0, 0, 0, 2, 0, 4, 0, 0, 0, 0, 0, 0, 0, 1, 0, 18, 0, 0, 0, 0, 
                 0, 0, 0, 0, 0, 0, 0, 3, 0, 0, 0, 0, 0, 0, 0, 4, 0, 0, 0, 0, 0, 0, 
                 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 
                 3, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 
                 0, 0, 0, 0, 0, 0, 0, 20, 1, 0, 5, 0, 0, 0, 3, 5, 0, 0, 1, 0, 0, 0, 0, 
                 0, 0, 0, 1, 4, 1, 2, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 
                 0, 0, 0, 0, 0, 0, 0, 0, 0, 3, 0, 2, 2, 3, 0, 0, 0, 0, 5, 5, 1, 26, 1, 
                 3, 6, 11, 26, 6, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 2, 
                 5, 0, 8, 0, 0, 0, 8, 0, 0, 0, 0, 0, 0, 0, 6, 2, 2, 0, 2, 11, 0, 0, 
                 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 4, 0, 2, 0, 0, 0, 0, 0, 
                 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 2, 0, 11, 0, 0, 0, 2, 0, 0, 0, 2, 1, 
                 2, 0, 14, 0, 0, 7, 3, 11, 3, 4, 129, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 
                 0, 0, 0, 0, 0, 0, 0, 0, 0, 11), nrow = 19,
               dimnames = list(c("Campoyong", "Hollywood", "Lupok", "Pob. 1", "Pob. 10", "Pob. 11",
                                 "Pob. 12", "Pob. 2", "Pob. 3", "Pob. 4", "Pob. 4A", "Pob. 5", "Pob. 6",
                                 "Pob. 7", "Pob. 8", "Pob. 9", "Pob. 9A", "Rural", "Salug"), 
                               c("Campoyong", "Hollywood", "Lupok", "Pob. 1", "Pob. 10", "Pob. 11",
                                 "Pob. 12", "Pob. 2", "Pob. 3", "Pob. 4", "Pob. 4A", "Pob. 5", "Pob. 6",
                                 "Pob. 7", "Pob. 8", "Pob. 9", "Pob. 9A", "Rural", "Salug")))

# Add self-links
diag(data_urb) <- diag(data_urb) / 2

# Create the chord diagram without order and specific colors
chordDiagram(data_urb, grid.col = 1:19, self.link = 1)


# Customize the chord diagram
## Gap between features

circos.par(gap.after = c( "Campoyong" = 5, "Hollywood" = 5, "Lupok" = 5, "Pob. 1" = 5, "Pob. 10" = 5, "Pob. 11" = 5,
                          "Pob. 12" = 15, "Pob. 2" = 5, "Pob. 3" = 5, "Pob. 4" = 5, "Pob. 4A" = 5, "Pob. 5" = 5, "Pob. 6" = 5,
                          "Pob. 7" = 5, "Pob. 8" = 5, "Pob. 9" = 5, "Pob. 9A" = 5, "Rural" = 15, "Salug" = 5))

## Features color

chordDiagram(data_urb, order = c("Hollywood", "Lupok", "Campoyong", "Salug", "Pob. 1", "Pob. 2", "Pob. 3", "Pob. 4", "Pob. 4A", "Pob. 5", "Pob. 6",
                                 "Pob. 7", "Pob. 8", "Pob. 9", "Pob. 9A", "Pob. 10", "Pob. 11",
                             "Pob. 12", "Rural"), grid.col = c("Rural" = "#FC7643", "Pob. 6" = "#343779", "Pob. 9A" = "#E9C46A", 
                                                               "Pob. 5" = "#33A9AC", "Pob. 8" = "#A5CF61", "Salug" = "#DA2A47", 
                                                               "Pob. 1" = "#B1816C", "Campoyong" = "#8C0303", "Pob. 5A" = "#6089b5",
                                                               "Pob. 4" = "#8E44AD",  "Pob. 10" = "#FED700", "Pob. 12" = "#F39C12",
                                                               "Pob. 2" = "#B9324C", "Pob. 11" = "#FCE205", "Pob. 2" = "#702963",
                                                               "Pob. 7" = "#1034A6", "Pob. 4A" = "#1E90FF", "Lupok" = "red", "Pob. 3" = "purple",
                                                               "Pob. 9" = "#1cd3a2",
                                                             
                                                               self.link = 1))


# Reset chord diagram
circos.clear()
```

Overall, the origin and destination analysis shed light on the spatial dynamics of care-related travel in Guiuan, highlighting the importance of the Urban Mainland region, the challenges faced by island communities, and the complex patterns of travel within and between barangays.

[back](./README.md)


[back](./README.md)
