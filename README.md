# Build an algorithm that predicts mpg from the variables in the data set
mtcars
#install.packages("caret")
library(caret)
#install.packages("mlbench")
library(mlbench)

model <- train(
  mpg ~.,
  # Not quite sure what the two does I know it tries the model with different amounts of parameters
  # But not what two does specifically
  tuneLength = 4,
  #  tuneGrid = data.frame(mtry = c(2, 3, 7))
  # This can be used to try out different parameters, but not quite sure how it works still
  data = mtcars, method = "ranger",
  trControl = trainControl(method = "cv", number = 10, verboseIter = TRUE)
)
model
