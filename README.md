# Udacity - Communicate Data Findings - 2 Part Project
## by Vince Conca


## Prosper Loan Dataset

The data explored in this exercise concerns Prosper. Prosper is an online peer-to-peer (P2P) lending marketplace, where creditworthy borrowers can request a loan and investors can invest in “notes” (or portions) of each loan\**. The datset contains 113,937 loans with 81 variables on each loan. Definitions for the 81 variables can be found in a downloadable file: [Variable Definitions](ref/prosperLoanDataVariableDefinitions.xlsx) 43 variables contain null values and none contain duplicates. Variable data types are of integer, float, and string.

&emsp; \** from [prosper.com](www.prosper.com)

Primarily, I wanted to explore what impact the main metrics/individual variables have on Prosper's internal risk rating for potential Borrowers. The score ranges from 1 to 11 with 1 being the most risky Borrower and 11 being the least risky. It bears noting that per the definitions of the variables, the rating should only range from 1 to 10, not 1 to 11. Secondarily, I wanted to see how a Borrower's risk rating impacts approved loans through the lens of potential Investors by looking at the relationship between Borrower risk, their loan details, and Investor potential return.

With that in mind, the variables I selected as having an affect on Prosper's risk score were:
* Debt to Income Ratio (DTI)
* Current Delinquencies
* Open Lines of Credit (LOC)
* Revolving Credit Balance
* Monthly Income
* Credit Score

As for how risk score impacts the loans and in turn impacts forecasted Investor return, I used:
* Prosper Risk Score
* APR
* Term
* Loan Amount
* Esitmated Return



## Summary of Findings

I began plotting the main metric I wanted to explore throughout the duration of this project, Prosper risk score. It was a normalized plot with a slight lean towards higher risk with the most common score being a 4. I then plotted each of the variables, one by one, that I selected as having a potential impact to the risk score. I did find a large number of extreme outliers in most of the data. I'm thinking this is due to the nature of the P2P lending model. Not being a financial institution with member accounts, where in order to be a member or have an account one would need to qualify and meet certain conditions up front. For that reason, a traditional lending model (bank/credit union, etc...) would have any significant outliers weeded out before a loan was even applied for.<br />A summary of each variable's investigation is below:

* Debt to Income Ratio (DTI): ~180 outliers removed; any above a DTI of 1 was removed as a max 1:1 DTI is a good representation of a typical potential P2P Borrower. 
* Current Delinquencies: Decided to not use this metric in further analysis; 85% had zero delinquencies and the rest were spread out from 1 to 21, though, a good amount had 1 or 2. I ended up deciding to just omit this metric once I saw the box plot suggested anything over 0 was an outlier.
* Open Lines of Credit (LOC): ~1450 outliers removed; I kept the threshold pretty high on this metric (21 open lines), using the box plot as a guide.
* Revolving Credit Balance: ~1375 outliers removed; again I set the threshold pretty high to ensure the remaining data represented a wide range of Borrowers, but at the same time, keeping it realistic by remvoing the outliers that were extrememly high.
* Monthly Income: ~600 outliers removed; this was a straightforward investigation, it was more of an arbitrary call on my part where to draw the line, I'm more interested in those making, at most, ~\$250k a year and below. So, those removed had exceptionally high incomes.
* Credit Score: No outliers removed as this was a categorical variable with the limits set during data cleaning.

Next, I looked at the Prosper risk score plotted against each of the variables explored in univariate analysis, excluding current delinquencies per the reasoning above.

The greatest impact was monthly income and credit score, which isn't all that surprising. Whenever an individual applies for a loan, income and credit score are typically the first two parameters a financial institution seeks. That said, the impact wasn't as great as I expected. Some borrowers with the lowest credit scores found themselves with the best risk rating and a handful with the highest credit scores found themselves in the riskiest category.

Something that was a bit of an anomaly that I found interesting on almost every variable was the risk score of 11 (remember, per the definitions, 11 should not exist). The score did track with expectation to a certain degree, the values required to receive that score were typically better than the previous scores, but not always as one would think. The requirements seemed far more narrow and in some cases, it seemed the values did not, in fact, need to be all that much better. It seems to me, and this is just speculation, that the risk score of 11 was or is experimental. 

In the final part of my investigation, I looked at Prosper's risk score plotted against all the varialbes together. And lastly, I was able to investigate the secondary question I had; how does the risk score translate not only into the components of an approved loan, but the estimated return on investement for Investors. After all, Prosper is a P2P loan model and Investors are integral to a Borrower receiving a loan.

The mulitvariate exploration essentially confirmed the bivariate analysis. Credit score and Monthly Income did indeed have the most impact to Prosper's risk score. I do want to reiterate that they didn't have an overwhelming impact. Had I been able to plot many of the other 81 variables, I'd imagine the impact correlation would be lessened. Ultimately, I think the variables work together to form the score with a small measure of weight favored to some variables. One thing that did come out of this part of the investigation dealt with the variables themselves; their relationship with each other rather than the risk score. There were some high correlations among the variables such as open lines of credit and revolving credit balance and also open lines of credit and debt to income ratio then also debt to income ratio and monthly income. None of these relationships are surprising and are intuitive, but it was kind of cool to see the interworkings of them via plotting. 


## Key Insights for Presentation

The null hypothesis in this investigation would be no one variable is overly dominant than any other in determining Prosper risk score. This wasn't entirely proven out in the investigation. Credit score and monthly income did have a larger correlation vs the other variables when plotted against risk score. Though, I do not feel the correlations for credit score and monthly income were significant enough to discount the other variables importance. For that reason, the null hypothesis cannot unequivocally be rejected. In summary, the key insight from the primary investigation is no one metric contributed to Prosper's risk score to such a degree that it overwhelmed any other variable, however credit score and monthly income are more significant.

An interesting insight I found was actually in the secondary investigation. The Investor "sales" pitch of Prosper (and other P2P lending companies) is that riskier loans have a chance of bigger payoffs, but may not be paid back; and on the flip side, less risky loans have smaller payoffs, but are more certain to actually pay. This leads potential Investors to weigh their options and believe they are spreading risk around per their investment strategy. However, what I found was the estimated return on investment is really pretty level across all loans. 

The plot containing risk score, APR, and estimated return did indicate riskier loans had larger estimated returns due to a higher return percentage, but when I added loan amount, it indicated that all loan's returns were forecasted to be pretty even, regardless of risk. Higher risk, higher APR, and higher estimated return percentage, were typically on smaller loan amounts and vice versa, lower risk, lower APR, and lower estimated return percentage, were typically on larger loan amounts.    

This, of course, would require a more thorough investigation as to why. It makes sense from a Propser internal business perspective, to create a relatively stable and regular profit for the company, the safest approach would be to have an equal return regardless of loan risk and one way to do that would be to approve larger loans for lower risk/lower APR Borrowers and smaller loans for higher risk/higher APR customers. There may be other reasons beyond Prosper's business model, for example, those deemed lower risk typically have higher incomes and therefore, as a byproduct, lower APR loans would be for larger amounts anyway. One key thing to have handy would be how estimated return is calculated. Also, estimated return is in not actual return, so seeing how the loans ended up paying for Investors, would also be key. But that's a different exploration for a different day! 