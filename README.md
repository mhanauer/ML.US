# ML.US
# Machine learning for universal screening
# Build an algorithm that predicts mpg from the variables in the data set
# This version can take a new data set and include the pre processing in the caret package
#install.packages("caret")
library(caret)
#install.packages("mlbench")
# This is to create some missing values to see if the pre processing works
library(mlbench)
set.seed(42)
mtcars[sample(1:nrow(mtcars), 10), "hp"] = NA
# Need to create x and y.  X needs to be a matrix or double and y needs to be vector or double to work
x = as.matrix(mtcars[,2:length(mtcars)]); x
y = as.vector(mtcars[, 1]); y
model <- train(
  x = x, y =y, 
  tuneLength = 1,
  method = "ranger",
  trControl = trainControl(method = "cv", number = 5, verboseIter = TRUE),
  preProcess = "knnImpute"
)
model
# Can grab the RMSE and create a coefficent of variation to get the accuracy
summary(model)
