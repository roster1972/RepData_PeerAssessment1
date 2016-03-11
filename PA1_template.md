# Reproducible Research: Course Project 1
Robert Osterried  
March 11, 2016  


## Loading and Preprocessing the Data
First, let's load the data (CSV in the working directory) and take a look . . .

```r
data <- read.csv('activity.csv', na.strings = "NA")
names(data)
```

```
## [1] "steps"    "date"     "interval"
```

```r
head(data)
```

```
##   steps       date interval
## 1    NA 2012-10-01        0
## 2    NA 2012-10-01        5
## 3    NA 2012-10-01       10
## 4    NA 2012-10-01       15
## 5    NA 2012-10-01       20
## 6    NA 2012-10-01       25
```

```r
dim(data)
```

```
## [1] 17568     3
```

## What is Mean Total Number of Steps Taken per Day?
Sum the steps for each day and make a histogram:

```r
totalSteps <- aggregate(data[, 1], list(Date=data$date), sum)
hist(totalSteps$x, main = "Total Number of Steps Taken Each Day", xlab = "Total Steps",
     col = "red")
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png)

Mean of total number of steps per day:

```r
mean(totalSteps$x, na.rm = TRUE)
```

```
## [1] 10766.19
```

Median of total number of steps per day:

```r
median(totalSteps$x, na.rm = TRUE)
```

```
## [1] 10765
```

## What is the Average Daily Activity Pattern?

Average the steps for each five-minute interval across all days and make a time series plot:

```r
intervalSteps <- aggregate(data[, 1], list(Interval=data$interval), mean, na.rm=TRUE)
library(lattice)
xyplot(x ~ Interval, intervalSteps, type = "l", xlab = "5-Min Interval", 
       ylab = "Avg. Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)

Determine which 5-minute interval, on average across all days, has the maximum number of steps:

```r
intervalSteps[intervalSteps$x == max(intervalSteps$x),]$Interval
```

```
## [1] 835
```

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
