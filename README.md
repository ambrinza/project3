# Project 3

## Purpose of the Repository

The purpose of this repository is to contain all of the code we need for our project 3 for ST558. In this project, we are concerned with reading in data,
creating summaries of the data, and fitting models to the data and finally comparing those models. We will be doing so in an automated fashion and creating
different reports for each channel of data. The data in this case is from an online news popularity data set.

## R Packages Used
The below packages were used in this work:

```
library(tidyverse)
library(ggplot2)
library(caret)
library(leaps)
library(rmarkdown)
```
    
## Links to the Generated Analyses
The analysis for [Lifestyle articles is available here](data_channel_is_lifestyle.html).  
The analysis for [Business articles is available here](data_channel_is_bus.html).  
The analysis for [Social Media articles is available here](data_channel_is_socmed.html).  
The analysis for [Technology articles is available here](data_channel_is_tech.html).  
The analysis for [World articles is available here](data_channel_is_world.html).  
The analysis for [Entertainment articles is available here](data_channel_is_entertainment.html).  


## Code Used to Create Analyses
```
# In this section we will automate the code to create a file per channel
# First need to pull all the different channel options
df <- read_csv("data/OnlineNewsPopularity.csv", show_col_types = FALSE)
cols_list <- colnames(df)
channels <- cols_list[startsWith(cols_list, "data_channel_is")]
#create filenames
output_file <- paste0(channels, ".html")
#create a list for each channel
params <- lapply(channels, FUN = function(x){list(channel = x)})

#put into a data frame 
reports <- tibble(output_file, params)

# Now need to knit
apply(reports, MARGIN = 1, 
            FUN = function(x){
                render(input = "project3-code.Rmd", output_file = x[[1]], params = x[[2]])
                })
```
