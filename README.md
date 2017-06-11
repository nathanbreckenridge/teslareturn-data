# teslareturn-data
#Author:Nathan Breckenridge
#Annual continuously compounded return of TSLA stock, calculated from closing prices.Built in R.
# data from Yahoo Finance on 6/11/17

setwd("/Users/nathanbreckenridge/Desktop/R Data")
mydata <- read.csv("Tsladata.csv")
summary(mydata)
str(mydata)
plot(mydata$Adj.Close, type = "l", col = "blue", 
     +      lwd = 2, ylab = "Adjusted close",
     +      main = "Monthly closing price of TSLA")
tsla_prices <- mydata[, "Adj.Close", drop = FALSE]
n <- nrow(mydata)
tsla_ret <- (tsla_prices[2:n, 1] - tsla_prices[1:(n - 1), 1]) / tsla_prices[1:(n - 1), 1]
names(tsla_ret) <- tsla[2:n,1]
head(tsla_ret)
tsla_ccret <- log(tsla_prices[2:n,1]) - log(tsla_prices[1:(n - 1),1])
names(tsla_ccret) <- mydata[2:n,1]
head(tsla_ccret)
head(cbind(tsla_ret, tsla_ccret))
plot(tsla_ret, type = "l", col = "blue", lwd = 2, ylab = "Return", main = "Monthly Returns on TSLA")
abline(h = 0)
legend(x = "bottomright", legend = c("Simple", "CC"), lty = 1, lwd = 2, col = c("blue", "red"))
tsla_gret <- 1 + tsla_ret
tsla_fv <- cumprod(tlsa_gret)
plot(tsla_fv, type = "l", col = "blue", lwd = 2, ylab = "Dollars", main = "FV of $1 invested in TSLA")
tsla_fv <- cumprod(tsla_gret)
