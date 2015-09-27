---
title       : My shiny web app, a very simple height predictor
subtitle    : Shiny web app for the Coursera Developing Data Products course
author      : Elena Cruz Martin
job         : 
framework   : io2012      # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap,quiz,interactive]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---


## Introduction
* The objective of this project is to build a simple shiny application to put in practice what we have learnt during the course
* My application is quite simple: It will get the height of the two parents as an imput and will 'predict' the expected height for the children
* As the focus here is in the shiny part and not on the prediction model, my prediction function is quite simple (probably too simple), it just calculates the mean of the height of both parents

---

## The ui.R file
* The ui.R file code is as follows: 

```r
shinyUI( pageWithSidebar(
  # Application title 
  headerPanel("Children's height prediction"),
  sidebarPanel(
    h5('We will predict the height of the children considering the height of the...'),
    numericInput('Parent1Input', 'Height for parent 1 (cms)', 170, min = 140, ...
    numericInput('Parent2Input', 'Height for parent 2 (cms)', 170, min = 140,...
    submitButton('Submit')),
  mainPanel(
    h3('Results of prediction for the height of the children:'),
    h4("You\'ve entered the following value for the first parent's height: "),
    verbatimTextOutput('Parent1Input'), 
    h4("You\'ve entered the following value for the second parent's height: "),
    verbatimTextOutput('Parent2Input'),
    h4('Which resulted in a prediction of '), verbatimTextOutput("prediction"), 
    h4("as expected height in cm for the child") ) ))
```

---

## The server.R file
* The server.R is as follows:

```r
childrenHeight <- function(Parent1Input,Parent2Input) mean(c(Parent1Input, Parent2Input))
shinyServer(function(input, output){
  output$Parent1Input<- renderPrint({input$Parent1Input})
  output$Parent2Input <- renderPrint({input$Parent2Input})
  output$prediction <- renderPrint({childrenHeight(input$Parent1Input,input$Parent2Input)
  })
})
```

---

## Behaviour


* When you input a height value for both parents and you click the 'Submit' button, the 'predicted' height of the children (i.e. the mean of the height of both parents) will be calculated.

* Example:

Parent 1 height (in cms) = 175

Parent 2 height (in cms) = 170

Predicted children height = 172.5cms.






