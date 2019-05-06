# Loan Biases
May 2019<br/>
APCOMP 221 Final Project<br/>
Caroline Teicher and Matt Leifer

# Is the US mortgage market racially biased?
Bias: [Should we define it]

# Intro
In 1975, Congress passed the home Mortgage Disclosure Act (HMDA), a federal law that necessitates select financial institutions publish their data pertaining to mortgage and publicize de-identified classifications of borrowers. The Consumer Financial Protection Bureau, a US government agency that oversees consumer protection in the financial sector, provides complimentary access to these public financial records on their website. The databse contains csvs, summary reports, and filtering options for 2007-2017 in the US. The datasets can be filtered by year, location, property, loan type, lender, and applicant. This repository focuses on 2017, the most recent year accessible in the bureau’s repository, New York, our home state.

# Related Works
Human-Centrist Data Scientist, Abe Gong, in a four part Medium post, challenged the alleged biases in the widely accepted COMPAS algorithm, a proprietary algorithm that is used by judges and parole officers to set bail, adjust sentences, and determine terms for parole. In his "Ethics of Power Algorithms" analyses, Gong looked at recidivism by risk score decile, conditional on race. He proved that COMPAS was not biased. This repository adapted his analyses for the housing market utilizing the HMDA 2017 NY data set. However, unlike COMPAS, we found the probabiltiy of loan originated by 2017 income brackets, conditional on race, was biased. There was a <font color="green"> Add Summary Numbers </font>. 


Reseachers have explored discriminatory consumer-Lending practices, comparing the quantifable biases for face-to-face lenders to those of Fintech, algorithmic lending. They proved that face-to-face and Fintech lender charge Latinx/African American borrowers higher interest rates, and Fintech discrimination is a result of a modal shift in discrimination. On the other hand, they noted face-to-face lenders further "negative welfare" by rejecting/accepting minority applications, but algorithmic lending does not discriminate in application rejections.

# Process and Results
The data set, provided by the Consumer Finance Protection Bureau (under custom datasets modify filters by location and year), specific to New York and exclusively for 2017, can be exported in csv format and contains ~440k rows and 78 columns with features such as applicant ethnicity, income, gender, income, and area demographics. The pre-processing notebook contains the cleaning of the data set so that it can be processed for exploratory analyses and logistic regression. The processing notebook contains our analysis and measurable results.

Our results quantified the amount of racial biases across income brackets. 

# Conclusion
The [ HMDA data set](https://www.consumerfinance.gov/data-research/hmda/explore) proves a raically biased lending practices in 2017 in NY state. At the same time, the data set is missing crucial key indicator, observable variables, that impact loan origination status. If we had knowledge of originated loans' interest rates' as well as rate spread, we would be able to explore further portential biases in the price of originated loans for the same income bracket conditional on race. It also would have been more conclusive to analyze loan origination status by credit score and income level, conditional on race. We suspect similar trends would emerge as shown in our analyses. Informatino about loan features would better judge an applicant's creditworthiness. This need for increased scope will be included in the 2018 HMDA data set, which although is not yet available, as a result of the Dodd-Frank Bill will legally require lenders report the following additions for each applicant: Credit score; NMLS Identification of the loan originator, Loan channel, Borrower age. Combined loan-to-value (CLTV) ratio, Borrower's debt-to-income (DTI) ratio, Borrower-paid origination charges, Points and fees, Discount points, Lender credits, Loan term, Prepayment penalties, Non-amortizing loan features, Interest rate and Rate spread for all loans.

Algorithmic fairness incorporates many ethical considerations. It questions whether there should be a focus on equal treatment or equal outcomes. This respository focuses on equal treatment. Racially biased lending practices coupled with a market shift towards algorithmic lending, increases the risk of confirmation bias. This would ensure that unobservable racial biases are prevelant in lending practices, as long as algorithms are trained on observable biases from previous lending practices. 

There must also be a push to report accurate data. Some data in the data set, probably a reporting error/mistake, indicates $99 million loans, many applicants did not report their income, may not have accuratley reported their income, and denial reason(s) are inconsistent and unreliable because it is rarely required and enforced. This is critical for lenders, to ensure they are approving loans for apporpriate applicants, for govenring bodies to best understand and regulate their respective lending markets, and for public officials to guage how to meet the housing needs of communities. We suggest enforcable penalities and fines for innacurate reporitng. 

US Fair Lending Laws do not consider the potential for Big Data variables to illegally discriminate. This is most difficult because of "black-box" algorithms, unobservable variables, and the usage of observable proxies. This may be a result of lenders utilzing an applicant's digital footprint as a proxy for lending probability or social media activity as a proxy for trust in creditworthiness. Moreover, it is troubling to consider the ability for Fair Lending Laws to adapt to face-to-face discirmination, and algorithmic raical biases, as the lending industry is notoriously slow and resistant to adjust its laws. There are also high overhead and inefficent, costs for jurisdictional challenges and procedures. Therefore, we suggest addressing the problem of racially discriminatonary lending practices in the algorithms themselves, rather than invest in highly regulated outcomes. 


# Works Cited
Abe Gong Rebuttal: https://gist.github.com/abegong/7389ed1fe4a7344d49951f6bb3195a2c
https://fivethirtyeight.com/features/technology-is-biased-too-how-do-we-fix-it/ 
https://arxiv.org/pdf/1609.07236.pdf 
https://arxiv.org/pdf/1701.08230.pdf
http://issues.secondarymarketingexec.com/article/what-lies-within-your-hmda-data/
https://faculty.haas.berkeley.edu/morse/research/papers/discrim.pdf
https://www.wired.com/story/your-smartphone-could-decide-whether-youll-get-a-loan/
https://s3.amazonaws.com/cfpb-hmda-public/prod/help/2018-hmda-fig-2018-hmda-rule.pdf
http://www.mortgagecompliancemagazine.com/mortgage-compliance-alphabet-soups/fair-lending-laws/
https://faculty.haas.berkeley.edu/morse/research/papers/discrim.pdf
https://medium.com/artificial-intelligence-policy-laws-and-ethics/encoded-laws-policies-and-virtues-the-offspring-of-artificial-intelligence-and-public-policy-3dfb357faf9
