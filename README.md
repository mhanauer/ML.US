# ML.US
# Machine learning for universal screening
# Build an algorithm that predicts mpg from the variables in the data set
mtcars
#install.packages("caret")
library(caret)
#install.packages("mlbench")
library(mlbench)
model <- train(
  mpg ~.,
  tuneLength = 1,
  data = mtcars, method = "ranger",
  trControl = trainControl(method = "cv", number = 5, verboseIter = TRUE),
  # This works with ranger when you use just the regular y ~ . formula
  preProcess = c("knnImpute", "centered", "scaled")
)
model
summary(model)
