# Moderna & AbbVie: Dynamic Covariance

Today, let's look at dynamic covariance for biotech diversification and weighting, building on our previous post on [GARCH models for Moderna](https://crawstat.com/2021/01/20/moderna-modeling-volatility-with-garch/). Picking assets with negative covariance, meaning their prices move in opposite directions, is important for diversification. Unlike traditional covariance, dynamic covariance using GARCH gives us a more accurate picture of covariance by taking into account the time-varying aspect (clustering) of volatility. It's also handy in portfolio selection. 

To demonstrate, let's build a simplified version of a portfolio of just two stocks, Moderna (ticker: MRNA) and AbbVie (ticker: ABBV), though, in reality, we'd aim for more diversification. You could apply the same approach to a broader portfolio in any sector you'd like. Let's first take a look at the two companies and my rationale for choosing them. 

Moderna is built upon a novel mRNA platform and has a newly commercialized product (e.g., Covid vaccine) with multiple phase 2 drugs in its [pipeline](https://www.modernatx.com/pipeline) across its core prophylactic vaccine business (e.g., CMV) and exploratory areas (e.g., cancer vaccines, VEFG regenerative therapy). While MRNA has yet to show profitability or positive cash flows, the commercialization of its covid vaccine was a major step in validating its novel mRNA platform and delivery mechanism as a path for future success. Given Moderna's profile and risks, let's try to balance it with a more established, diversified company    

AbbVie is an established, diversified pharma with a range of established [products](https://www.abbvie.com/our-science/products.html) in many therapeutic areas, a healthy phase 2 and 3 [pipeline](https://www.abbvie.com/our-science/pipeline.html), biosimilar competition, and consistently positive EBITDA and FCF. Another key reason I chose it is simply that I've been following it closely for many years and am familiar with it. 

Dynamic covariance = correlation of standardized residuals x conditional volatility 1 x conditional volatility 2: 

cov1,2 = ρstandardized residuals  *  𝜎1 *  𝜎2

We can use dynamic covariance to generate portfolio variance for different asset weights: 

𝜎2portfolio =  (w21𝜎21) + (w22𝜎22) + (2w1w2cov1,2)

Let's generate dynamic covariance by specifying and fitting GARCH models for MRNA and ABBV, selecting the optimal GARCH model, deriving conditional volatility and standardized residuals and correlation between standardized residuals, calculating dynamic covariance, and, lastly, seeing how portfolio variance changes with different asset weights. 

