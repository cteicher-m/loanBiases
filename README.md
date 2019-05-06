# Loan Biases
May 2019<br/>
APCOMP 221 Final Project<br/>
Caroline Teicher and Matt Leifer

#### This repository contains two notebooks, pre-processing, and processing, which contain documented analyses of the HMDA housing market data. All detailed processes and results are included in the two notebooks. Below is a summary of each project phase. 

# Is the US mortgage market racially biased?

## Intro
In 1975, Congress passed the home Mortgage Disclosure Act (HMDA), a federal law that necessitates select financial institutions publish their data pertaining to mortgage and publicize de-identified classifications of borrowers. This was an effort to reveal suspected credit deficiencies in urban neighborhoods that contributed to the deterioration of communities. Determining one’s loan worthiness on the basis race or unobservable variables or proxies for race, is illegal and solidifies racial wealth disparities. We hypothesize minority applicants, particularly African Americans, are systemically denied loan applications at higher rates than non-minority applicants. This may be a result of implicit biases that are a result of face-to-face lending. 

The Consumer Financial Protection Bureau, a US government agency that oversees consumer protection in the financial sector, provides complimentary access to these public financial records on their website. The database contains csv, summary reports, and filtering options for 2007-2017 in the US. The datasets can be filtered by year, location, property, loan type, lender, and applicant. This repository focuses on 2017, the most recent year accessible in the bureau’s repository, New York, our home state. 

## Related Works
Human-Centrist Data Scientist, Abe Gong, in a four-part Medium post, challenged the alleged biases in the widely accepted COMPAS algorithm, a proprietary algorithm that is used by judges and parole officers to set bail, adjust sentences, and determine terms for parole. In his "Ethics of Power Algorithms" analyses, Gong looked at recidivism by risk score decile, conditional on race. He proved that COMPAS was not biased. This repository adapts his analyses for the housing market utilizing the HMDA 2017 NY data set. However, unlike COMPAS, we found the probability of loan originated by 2017 income brackets, conditional on race, was biased. 

There has been substantial quantitative and qualitative work looking at lending officers’ commitment to meeting the housing needs of their communities. It is argued that rules and regulations in the mortgage market, in addition to heightening competition in the industry, will increase the number of approved loans and mitigate racial biases. In February 2018, the Trump Administration terminated the regulatory powers of The Office of Fair Lending and Equal Opportunity, which previously had been, perhaps unsuccessfully, enforcing fines to companies that discriminated against minorities, so that the office of the director, could instead focus on advocacy, coordination and education. 



Researchers have explored discriminatory consumer-Lending practices, comparing the quantifiable biases for face-to-face lenders to those of Fintech, algorithmic lending. A UC Berkeley study proved that face-to-face and Fintech lenders both charge Latinx/African American borrowers similarly higher interest rates, but Fintech discrimination is a result of a modal shift in algorithmic discrimination. The origination of conventional conforming mortgages securitized by Government Sponsored Entities and offered by face-to-face lenders, are a factor of an applicant, an application, and “soft” information as a result of different face-to-face interaction among borrowers. 

## Process and Results
The data set, provided by the Consumer Finance Protection Bureau (under custom datasets modify filters by location and year), specific to New York and exclusively for 2017, can be exported in csv format and contains ~440k rows and 78 columns with features such as applicant ethnicity, income, gender, income, and area demographics. The pre-processing notebook contains the cleaning of the data set so that it can be processed for exploratory analyses and logistic regression. The processing notebook contains our analysis and measurable results.

Our results quantified the amount of racial biases across income brackets. There is a clear discrimination among originated loan applicants, for each income bracket, conditional on race. #Explanation of training test results
#R^2 and analyses 
#Spearman Test

## Conclusion
The [ HMDA data set](https://www.consumerfinance.gov/data-research/hmda/explore) proves a racially biased lending practices in 2017 in NY state. At the same time, the data set is missing crucial key indicator, observable variables, that impact loan origination status. Rate spread is a indication of the cost of one’s loan and can reveal racial biases. However, too many row entries were missing crucial information such as rate spread and applicant income. If we had knowledge of originated loans' interest rates' as well as other missing columns, we would be able to explore further potential biases in the price of originated loans for the same income bracket conditional on race. It also would have been more conclusive to analyze loan origination status by credit score and income level, conditional on race. We suspect similar trends would emerge as shown in our analyses. Information about loan features would better judge an applicant's creditworthiness. This need for increased scope will be included in the 2018 HMDA data set, which although is not yet available, as a result of the Dodd-Frank Bill will legally require lenders report the following additions for each applicant: Credit score, NMLS Identification of the loan originator, Loan channel, Borrower age, Combined loan-to-value (CLTV) ratio, Borrower's debt-to-income (DTI) ratio, Borrower-paid origination charges, Points and fees, Discount points, Lender credits, Loan term, Prepayment penalties, Non-amortizing loan features, Interest rate and Rate spread for all loans. Although these features will reveal deeper patterns of discriminatory lending practices, they increase privacy concerns. Each applicant will have more than 61 features published about themselves, which can be easily combined with census data or other national publications. This may increase the risk of de-identification, exposing sensitive information such as an applicant’s income, credit score, and debt.

Algorithmic fairness incorporates many ethical considerations. It questions whether there should be a focus on equal treatment or equal outcomes. This repository focuses on equal treatment. Racially biased lending practices coupled with a market shift towards algorithmic lending, increases the risk of confirmation bias. This would ensure that unobservable racial biases are prevalent in lending practices, as long as algorithms are trained on observable biases from previous lending practices. 

There must also be a push to report accurate data. Some data in the data set, probably a reporting error/mistake, indicates $99 million loans, many applicants did not report their income, may not have accurately reported their income, and denial reason(s) are inconsistent and unreliable because it is rarely required and enforced, and the denial codes are often ambiguous. This is critical for lenders, to ensure they are approving loans for appropriate applicants, for governing bodies to best understand and regulate their respective lending markets, and for public officials to gauge how to meet the housing needs of communities. We suggest enforceable penalties and fines for inaccurate reporting. 

US Fair Lending Laws do not consider the potential for Big Data variables to illegally discriminate. This is most difficult because of "black-box" algorithms, unobservable variables, and the usage of observable proxies. This may be a result of lenders utilizing an applicant's digital footprint as a proxy for lending probability or social media activity as a proxy for trust in creditworthiness. Moreover, it is troubling to consider the ability for Fair Lending Laws to adapt to face-to-face discrimination, and algorithmic racial biases, as the lending industry is notoriously slow and resistant to adjust its laws. There are also high overhead and inefficient, costs for jurisdictional challenges and procedures. Therefore, we suggest addressing the problem of racially discriminatory lending practices in the algorithms themselves, rather than invest in highly regulated outcomes. Additional research in this field could look at discriminating the basis of sex, ethnicity, and religion. 

### Works Cited
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
https://www.washingtonpost.com/news/wonk/wp/2018/03/14/the-senate-rolls-back-rules-meant-to-root-out-discrimination-by-mortgage-lenders/?noredirect=on&utm_term=.86041577a8a3

