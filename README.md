# CloseOut Reserve

A model is presented to calculate the monthly Close-Out Reserve of the structured interest rate derivatives. Products cover vanilla swaptions, Bermudan swaptions, callable swaps, callable exotics, variable notional swaptions, cap and floor and Treasury bond options. 

We can price all kinds of options and get the corresponding Vegas based on the above volatility matrices. Let us consider an option (vanilla or non-vanilla). Given a swaption term, an underlying term and a strike price, if we change the volatility from the above volatility cubic, we can get one Vega by using the definition of Vega. 

Given a M× N Vega matrix obtained from the above methods and a same-sized M×N Volatility Spread matrix, the option Close-Out Reserve can be calculated. However, Broker only offers a smaller-sized quoted bid/offer Volatility Spread matrix, which usually has a minimal dimension of 4×4. 

In order to calculate the Option Close-Out Reserve, the M×N Vega matrix has to be transformed into a smaller-sized 4×4 matrix, and then the netted positions of this smaller-sized matrix are applied to the quoted bid/offer spread. We have used bilinear projection to transform the Vega matrix. Let us review the algorithm of the bilinear projection. Given M× N Volatility Spread matrix, we will transfer it to be a 4× 4 Volatility Spread matrix and calculate the total Close-Out reserve.

Firstly, for each column, we project the value at the underlying term=1M, 3M, 6M and 1Y into the value at the underlying term=1Y, the value at the underlying term= 5Y into the value at the underlying term=5Y, the value at the underlying term=10Y into the value at the underlying term=10Y, the value at the underlying term= 20Y, 25Y and 30Y into the value at the underlying term=20 Y. 

Secondly, we proportionally project the value at the underlying term= 2Y, 3Y, 4Y to 1Y and 5Y. Similarly, we do the same operations for years between 5Y and 10Y, and years between 10Y and 20Y.

Broker only offers quoted bid/offer Volatility Spread matrix of USD. We propose to use these spreads for the CAD Close-Out Reserve calculation until in the future a more appropriate source comes up. 

It has been determined that the CAD bid/offer matrix will be calculated as a multiple of the USD matrix. The multiple will be updated where necessary and will be based on the relationship between observable market quotes of CAD and USD. Currently the CAD bid/offer spread is 2.5 times the USD.

We use the bilinear projection based on the following reasons: (1) the bilinear projection is a standard market
methodology based on practical conventions; (2) The bilinear projection matrix nicely absorbs most of the information embedded in the original matrix. The summation of each column in the new matrix is equal to the summation of each column in the old matrix. It is a same case for each row.

Reference:

https://finpricing.com/curveVolList.html
