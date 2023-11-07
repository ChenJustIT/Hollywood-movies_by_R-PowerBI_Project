# R-Power-BI-Project
                                          
# Aim: 
To analyze the performance of Hollywood movies 

# Data: 
Title, genre, studio, profitability and ratings for movies released 2007-2012. Source: InformationIsBeautiful.net 

# Download data from this link:  
https://public.tableau.com/app/sample-data/HollywoodsMostProfitableStories.csv

# Data Source:  
HollywoodsMostProfitableStories.csv 
![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/48013f6b-c146-4d38-845f-13066cf2c37f)
 

                                       Step1: Initial Exploratory Analysis

# Load data 
df<- read.csv("https://public.tableau.com/app/sample-data/HollywoodsMostProfitableStories.csv")
 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/3a1260b8-a18c-442e-8e60-3b62cdd58401)

 

# Take a look at the data: 

View(df)

 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/5ebae422-8a8b-4a14-8fb4-9026698c66c3)

# Load library: 
install.packages("tidyverse")
WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

https://cran.rstudio.com/bin/windows/Rtools/
Installing package into ‘C:/Users/solve/AppData/Local/R/win-library/4.3’
(as ‘lib’ is unspecified)
trying URL 'https://cran.rstudio.com/bin/windows/contrib/4.3/tidyverse_2.0.0.zip'
Content type 'application/zip' length 430873 bytes (420 KB)
downloaded 420 KB

package ‘tidyverse’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
C:\Users\solve\AppData\Local\Temp\RtmpApsExq\downloaded_packages

#Import library 
library(tidyverse)
── Attaching core tidyverse packages ───────────────────────── tidyverse 2.0.0 ──
✔ dplyr     1.1.3     ✔ readr     2.1.4
✔ forcats   1.0.0     ✔ stringr   1.5.0
✔ ggplot2   3.4.4     ✔ tibble    3.2.1
✔ lubridate 1.9.3     ✔ tidyr     1.3.0
✔ purrr     1.0.2     
── Conflicts ─────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
ℹ Use the conflicted package to force all conflicts to become errors
Warning message:
package ‘tidyverse’ was built under R version 4.3.2

# Check data types: 
str(df)
 
                                 Step 2: Clean Data 

# Check for missing values:
colSums(is.na(df))
 

  
If we continue to drop the missing values normally by drop function below, we will find that one missing value still exists in the column, Lead. Studio, although it looks like a blank cell in the original data source of the Excel sheet as the other missing values. However, it is a still blank cell when we check them by the view function after the data source is imported on R, but others contain NA. The course that the missing value cannot be found by colSums(is.na(df)) is that it is a blank as “”, not NA as usual.
#so, we will use another function to find number of empty strings
map_int(df, function(x) sum(x == ""))
 
#replace empty string with NA
df[df==""]<-NA
# Check for missing values again:
colSums(is.na(df))
 

#Drop missing values 
df <- na.omit(df)      #or df <- df %>% drop_na();   or we may be able to use subset function


# check to make sure that the rows have been removed 
 colSums(is.na(df))
 
 

                                               Step 3: Exploratory Data Analysis 
# create df1
df1=na.omit(df) 

#Summary Statistics: 
summary(df1)
 
  
  
#scatterplot 
ggplot(df1, aes(x=Lead.Studio, y=Rotten.Tomatoes..)) + geom_point()+ scale_y_continuous(labels = scales::comma)+coord_cartesian(ylim = c(0, 110))+theme(axis.text.x = element_text(angle = 90))

 

 #bar chart 
ggplot(df1, aes(x=Year)) + geom_bar()

 
                                                         Step 4: Export data 
#Export clean data 
write.csv(df1, "clean_df.csv") 

 
                                                                Import this file clean_df into Power BI.
                                    Step 5: Create Power BI Dashboard 

Tips: 
•	Feel free to add more charts apart from the ones mentioned in the next slide.  
•     For the dashboard, the company would like you to use their brand colors which are 
        blue, green and brown. You can use light or dark shades of each color. For example, 
       light blue and dark blue are acceptable. 
       You can combine these colors any way that you like. For example, you can use only 
              blue and green if you want to. 

1.	The average Rotten Tomatoes ratings of each genre
 

2.	The number of movies produced per year 
       

3.	The audience scores for each film  
        
4.	The profitability per studio      
       

5.	The worldwide gross per genre 
                   
6.	Dashboard
 

                  
                                                                                                                           --End
