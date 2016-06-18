---
title: "Coursera Data Science Capstone Project MileStone Report"
author: "Kevin Dyke"
date: "29 April 2016"
output: html_document
---

##Aims
Does the link lead to an HTML page describing the exploratory analysis of the training data set?
Has the data scientist done basic summaries of the three files? Word counts, line counts and basic data tables?
Has the data scientist made basic plots, such as histograms to illustrate features of the data?
Was the report written in a brief, concise style, in a way that a non-data scientist manager could appreciate?


## Getting the data 

```{r}
# Download the required datasets and unzip 
if (!file.exists("Coursera-SwiftKey.zip")) {
  download.file("https://d396qusza40orc.cloudfront.net/dsscapstone/dataset/Coursera-SwiftKey.zip")
  unzip("Coursera-SwiftKey.zip")
}
```

```{r,echo=TRUE}
library(stringi)

mb <- 1024 * 1024

blogs <- readLines("final/en_US/en_US.blogs.txt", encoding = "UTF-8", skipNul = TRUE)
news <- readLines("final/en_US/en_US.news.txt", encoding = "UTF-8", skipNul = TRUE)
twitter <- readLines("final/en_US/en_US.twitter.txt", encoding = "UTF-8", skipNul = TRUE)


# Get file sizes
blogsSize <- file.info("final/en_US/en_US.blogs.txt")$size
newsSize <- file.info("final/en_US/en_US.news.txt")$size
twitterSize <- file.info("final/en_US/en_US.twitter.txt")$size

# Get words in files
blogsWords <- stri_count_words(blogs)
newsWords <- stri_count_words(news)
twitterWords <- stri_count_words(twitter)

# Summary of the data sets
df <- data.frame(source = c("blogs", "news", "twitter"),
           file.size.MB = c(blogsSize/mb, newSize/mb, twitterSize/mb),
           numLines = c(length(blogs), length(news), length(twitter)),
           numWords = c(sum(blogsWords), sum(newsWords), sum(twitterWords)),
           meanWords = c(mean(blogsWords), mean(newsWords), mean(twitterWords)))

#colnames(df) <- c("File", "Size (MB", "Num of Lines","Num of Words","Mean Num Of Words")
knitr::kable(df,format="html")df


```



## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r cars}
summary(cars)
```

## Including Plots

You can also embed plots, for example:

```{r pressure, echo=FALSE}
plot(pressure)
```

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
