# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
###   Set working directory to where the data lives.
setwd("H:/BigStegShare/COURSERA/DataScience/ReproducibleData/")

###   Read in data.
FITDATA <- read.csv("activity.csv")
```

## What is mean total number of steps taken per day?

```r
#1:1. calculate sums of steps per day
new1 <- with (FITDATA, tapply(steps, date, sum))

#1:2. plot histogram
plot(new1, type = "h", xaxt = "n", xlab = "Date", ylab = "Total Steps")
axis(1, at=1:length(names(new1)), lab=names(new1))
title(main = "Total Steps Per Day" )
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png)

```r
#1:3. calculate mean and median of total number of steps taken per day
mean(new1, na.rm = TRUE)
```

```
## [1] 10766.19
```

```r
median(new1, na.rm = TRUE)
```

```
## [1] 10765
```

```r
#returns 10766.19 and 10765, respectively.
```

## What is the average daily activity pattern?

```r
#2:1. make a time-series plot of five-min intervals and average steps taken, averaged across all days.
#calculate sums per min interval
#new2 <- with (FITDATA, tapply(steps, interval, sum))
myMeans <- tapply(FITDATA$steps, FITDATA$interval, mean, na.rm = TRUE)

#plot time-series based on intervals with means per interval
plot(names(myMeans), myMeans, type = "l", xlab = "Time interval",ylab = "Average Steps", col = "blue")
title(main = "Average Steps per 5-Minute Interval by Day" )
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)

```r
#interval with max average steps:
myIntervals <- names(myMeans)
newData <- data.frame(as.integer(myIntervals),myMeans)
colnames(newData) <- c("intervals","averageSteps")
newData[max(newData$averageSteps),]$intervals
```

```
## [1] 1705
```


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
