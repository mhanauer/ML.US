# ML.US
# Machine learning for universal screening
# Build an algorithm that predicts mpg from the variables in the data set
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
head(mtcars.knn.pred)

model <- train(
  mpg1 ~ ., 
  tuneLength = 1,
  data = mtcars, method = "ranger",
  trControl = trainControl(method = "cv", number = 5, verboseIter = TRUE)
)
model
# Can grab the RMSE and create a coefficent of variation to get the accuracy
summary(model)
