# Hollywood-movies_by_R-PowerBI
                                          
## Aim: 
To analyze the performance of Hollywood movies 

## Source: 
InformationIsBeautiful.net 

## You can download data from this link:  
https://public.tableau.com/app/sample-data/HollywoodsMostProfitableStories.csv

## Data:  
**It is an Excel sheet, HollywoodsMostProfitableStories.csv, for movies released between 2007 and 2012**

![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/48013f6b-c146-4d38-845f-13066cf2c37f)
 
# Step1: Initial Exploratory Analysis by R

## Load data 
df<- read.csv("https://public.tableau.com/app/sample-data/HollywoodsMostProfitableStories.csv")
 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/3a1260b8-a18c-442e-8e60-3b62cdd58401)

 

## Take a look at the data: 

View(df)

 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/5ebae422-8a8b-4a14-8fb4-9026698c66c3)

## Load library: 
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

## Import library 
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

## Check data types: 
str(df)

 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/28936e2a-c244-4a6c-8c90-284774877b1d)

#  Step 2: Clean Data 

## Check for missing values:
colSums(is.na(df))
 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/4bf8a342-5369-461f-a677-488e7298ceb5)

  
### During this process, we should realise that missing values include both blank values and Null values. The function "map_int" can find both kinds and the blank value should be replaced with NA before all the missing values can be dropped together. 

## Use the function to find all missing values
map_int(df, function(x) sum(x == ""))
![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/2b4e4eb5-395c-46e9-9872-8f86542e6702)

## Replace empty string with NA
df[df==""]<-NA

## Check for missing values again:
colSums(is.na(df))
 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/2ef066ef-a010-4e77-a529-1b4193ab5539)

## Drop missing values 
df <- na.omit(df)      #or df <- df %>% drop_na();   or we may be able to use subset function

## Check to make sure that the rows have been removed 
 colSums(is.na(df))
![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/3774c77e-203a-4fe6-aa09-63b4c751630a)
 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/e776de51-6c5d-416b-bc2f-33d8d6d26b16)

 

# Step 3: Exploratory Data Analysis 

## Create df1
df1=na.omit(df) 

## Summary Statistics: 
summary(df1)

![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/a0e6e1d2-6e2d-40c9-8c9f-396e4828ef68)
  
## Scatterplot 
ggplot(df1, aes(x=Lead.Studio, y=Rotten.Tomatoes..)) + geom_point()+ scale_y_continuous(labels = scales::comma)+coord_cartesian(ylim = c(0, 110))+theme(axis.text.x = element_text(angle = 90))

![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/fc516ba1-3d98-42ea-9ee1-c5617fb1f842)

 ## Bar chart 
ggplot(df1, aes(x=Year)) + geom_bar()

![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/9b0f659a-38ab-437c-8c95-8ddfc6e0590d)

 
# Step 4: Export data 

## Export clean data 
write.csv(df1, "clean_df.csv") 

![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/acece8a5-6478-4e18-85f5-925d6efd64eb)

 
 **Now I import this file clean_df into Power BI to go to the next step 5.**

# Step 5: Create Power BI Dashboard 

## Tips: 
### For the dashboard, the company would like you to use their brand colors which are blue, green and brown. You can use light or dark shades of each color. For example, light blue and dark blue are acceptable. You can combine these colors any way that you like. For example, you can use only blue and green if you want to. 
  

## 1.	The average Rotten Tomatoes ratings of each genre
 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/9605de70-d47a-4548-bf9b-df048d6ea5f4)

## 2.	The number of movies produced per year 
  ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/c3359c69-f0e9-4383-937e-b327a748aec8)
 
## 3.	The audience scores for each film  
  ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/301bf56a-4c60-4591-ba5d-5160a185e6f5)
     
## 4.	The profitability per studio      
  ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/f30ae7ee-5ace-4714-9d8e-8ed414d4edd1)
    
## 5.	The worldwide gross per genre 
  ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/cc2057b2-c39b-453e-8dc3-7141e79e4ba0)

### I format all the visuals above by such as Shadow Effect, data labels, adjusting the sizes of the fonts, and choosing the correct aggregations and the colors allowed.

###  Lastly, it is a dashboard with a background image, containing all the visuals above and a Gauge, showing ‘The average and the maximum Rotten Tomatoes ratings’. You can click the different parts of one of the visuals to filter the other visuals, and the corresponding number will show in the Gauge as well**
                
## 6.	Dashboard
 ![image](https://github.com/ChenJustIT/R-Power-BI-Project/assets/150026038/c0c0d221-b7cd-4666-b7e3-aa31aeb6d97e)


# --End
