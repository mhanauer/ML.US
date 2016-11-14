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
# Do the preprocessing outside the function, because it won't work inside the function
mtcars.knn = preProcess(mtcars, method = c("knnImpute")); mtcars_knn
#install.packages("RANN")
library(RANN)
mtcars.knn.pred =  predict(mtcars_knn, mtcars)
# Changed the name to mpg1 so it is different from the mtcars pacakge
fix(mtcars.knn.pred)
mtcars.knn.pred.df = as.data.frame(mtcars.knn.pred)
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
