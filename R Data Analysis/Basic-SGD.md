y = th0 + th1*x)/(1 + th2*exp(th3*x))

The basic SGD algorithm is used to estimate the parameters of this model.

```
learning_rate <- 0.05
th0 <- 1
th1 <- -1
th2 <- 1
th3 <- 1

m <- 100
threshold <- 10e-5

# Define quadratic loss function
loss_func <- expression((y - (th0 + th1*x)/(1 + th2*exp(th3*x)))^2)

# Partial derivatives of loss function with respect to thetas
deriv_th <- deriv(loss_func, c("th0", "th1", "th2", "th3"))

# Initial starting point for loss function
niters.store <- 0

dat <- data.frame(x,y)

# Basic SGD Algorithm
for (i in 1:100000){
  thetas <- c(th0, th1, th2, th3)
  
  # Sample mini batch of m inputs, sample x and its corresponding y
  batch_index <- sample(1:1000, m)
  batch <- dat[batch_index,]
  batch_x <- batch$x
  batch_y <- batch$y
  
  # Loss function evaluated
  loss <- eval(loss_func, list(x = x, y = y, th0 = thetas[1], th1 = thetas[2], th2 = thetas[3], th3 = thetas[4]))
  
  # Set g equal to zero
  g <- c(0,0,0,0)
  
  for (j in 1:m){
    # Find and evaluate gradient
    gradient_th <- eval(deriv_th, list(x = batch_x[j], y = batch_y[j], th0 = thetas[1], th1 = thetas[2], th2 = thetas[3], th3 = thetas[4]))
    
    # Compute gradient estimate
    g <- g + 1/m * attr(gradient_th, "gradient")
    
    # Apply update
    thetas <- thetas - learning_rate * g
  }
  th0 <- thetas[1]
  th1 <- thetas[2]
  th2 <- thetas[3]
  th3 <- thetas[4]
  
  # New loss function
  loss_new <- eval(loss_func, list(x = x, y = y, th0 = th0, th1 = th1, th2 = th2, th3 = th3))
  
  # Keep track of number of iterations
  niters.store <- niters.store + 1
  
  if (abs(sum(loss_new) - sum(loss))/sum(loss) < threshold){
    break
  }
}
```
