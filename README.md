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
  preProcess = c("knnImpute", "center", "scale")
)
model
# Can grab the RMSE and create a coefficent of variation to get the accuracy
summary(model)
# Gets the predicted values.  I don't think we actually need this part for the paper
pred = predict(model, mtcars)
summary(pred)
model
