# mnist

MNIST data for use with deepNN R package (or indeed any other package for that matter!)

library(deepNN)

download_mnist("mnist.RData")

load("mnist.RData") # loads objects train_set, truth, test_set and test_truth

net <- network( dims = c(784,16,16,10),
                activ=list(ReLU(),ReLU(),softmax()))

netwts <- train(dat=train_set,
                truth=truth,
                net=net,
                eps=0.001,
                tol=0.8, # normally would use a higher tol here e.g. 0.95
                loss=multinomial(),
                batchsize=100)
                
pred <- NNpredict(  net=net,
                    param=netwts$opt,
                    newdata=test_set,
                    newtruth=test_truth,
                    record=TRUE,
                    plot=TRUE)
