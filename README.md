# Loan Biases
May 2019<br/>
APCOMP 221 Final Project<br/>
Caroline Teicher and Matt Leifer

#### This repository contains two notebooks, pre-processing.ipynb, and processing.ipynb, which contain documented analyses of the HMDA housing market data. All detailed processes and results are included in the two notebooks. Below is a summary of the project.

# Research Question: Is there racial bias in the mortgage approval process in the US?

## Intro
In 1975, Congress passed the home Mortgage Disclosure Act (HMDA), a federal law that necessitates select financial institutions publish de-identified data each year pertaining to mortgage lending. This law was passed as part of an effort to reveal suspected credit deficiencies in urban neighborhoods that contributed to the deterioration of communities. Determining one’s loan worthiness on the basis race or unobservable variables or proxies for race, is illegal and solidifies racial wealth disparities. Despite the fact that this data has been reported to the government for nearly 45 years and online at least for the past few years, we hypothesize minority applicants, particularly Blacks, are nonetheless systematically denied loan applications at higher rates than non-minority applicants. The difference in approval ratings may be a result of implicit biases that come into play during face-to-face lending. 

The Consumer Financial Protection Bureau, a US government agency that oversees consumer protection in the financial sector, provides complimentary access to these public financial records on their website. The database contains csv, summary reports, and filtering options for 2007-2017 in the US. The datasets can be filtered by year, location, property, loan type, lender, and applicant. Each year, an institution must edit, according to FFIEC regulations, the data and upload pipe delimited text files by March 1. These files are checked for validity, and certified each year on the FFIEC HMDA online platform. 

This repository focuses on 2015 in New York, our home state, and uses this data as a proxy for the national mortgage lending market. Given the fact that New York is one of the most liberal states, it seems reasonable to conclude that if there is a bias in NY State lending it will persist in other similarly liberal states and could be worse in states that have had even more strained racial tensions than New York. The 2015 NY State data only contains over 400,000 records and so doing a more extensive nation-wide, multi-year analysis would likely have required greater computational power than we had at our disposal.  Even if the results to not generalize to the US as a whole, they will still be valid for New York State. 

After conducting some preliminary analysis on the dataset, which suggested that there may be a systematic bias against blacks and African Americans, we further examined this bias by creating a logistic regression model which did not use race as an input to predict the likelihood an applicant with certain qualities would be approved.  If the probabilty of approval predicted by our model differed significantly from the true approval probability, then we would be able to conclude that race (or at least some other factor that is highly correlated with race) can explain the observed discrepancies in approval.  

## Related Works
Human-Centrist Data Scientist, Abe Gong, in a four-part Medium post, challenged the alleged biases in the widely accepted COMPAS algorithm, a proprietary algorithm that is used by judges and parole officers to set bail, adjust sentences, and determine terms for parole. In his "Ethics of Power Algorithms" analyses, Gong looked at recidivism by risk score decile, conditional on race, proving that COMPAS was not biased. This repository adapts his analyses for the housing market utilizing the HMDA 2015 NY data set. However, unlike COMPAS, we found the probability of determining an originated loan, within the context of 2015 income brackets, conditional on race, was biased. 

There has been substantial quantitative and qualitative work looking at lending officers’ commitment to meeting the housing needs of their communities. It is argued that rules and regulations in the mortgage market, in addition to heightening competition in the industry, will increase the number of approved loans and mitigate racial biases. In February 2018, the Trump Administration terminated the regulatory powers of The Office of Fair Lending and Equal Opportunity, which previously had been, and perhaps unsuccessfully, enforcing fines to companies that discriminated against minorities. This shift gives more power to the office of the director to focus on advocacy, coordination, and education.

Researchers have explored discriminatory consumer-lending practices, comparing the quantifiable biases for face-to-face lenders to those of Fintech, algorithmic lending. A UC Berkeley study showed that whether African American or Hispanic prospective homebuyers had their loans approved and constructed algorithmically or via a face-to-face interaction, these racial groups received mortgages that had higher interest rates relative to similar prospective homebuyers who were not of these races. The researchers concluded that because the data used to train these algorithmic lending models were themselves biased, the models used by these algorithmic lenders simply reflected these biases. The origination of conventional conforming mortgages securitized by Government Sponsored Entities (such as Fannie Mae and Freddie Mac) and offered by face-to-face lenders, are a factor of an applicant, an application, and “soft” information as a result of different face-to-face interaction among borrowers. 

## Process and Results
The data set, provided by the Consumer Finance Protection Bureau (under custom datasets with modified filters by location and year), specific to New York and exclusively for 2015, can be exported in csv format and contains ~440k rows and 78 columns with features such as applicant ethnicity, income, gender, and area demographics. The pre-processing notebook contains the cleaning of the data set so that it can be processed for exploratory analyses and run through a logistic regression classifier. The processing notebook contains our analysis and measurable results.

First, we looked at the distribution of applicant incomes, and saw a substantial number of applicants (-1 column) who did not report their income. This is troublesome because an applicant with no income cannot be considered as a data entry in later analyses. We then quantified the amount of racial biases across income brackets. After controlling for income, Asians were -1.83% less likely to get a loan approved relative to whites, and blacks were -14.82% less likely to get a loan approved relative to whites. There is a clear discrimination among originated loan applicants, for each income bracket, conditional on race. In this preliminary exploration, there were spikes in Native American loan origination in the highest income brackets. This was due to a lack of data, where there were 1 or 2 applicants in one of the highest income bracket where we suspect racial biases are not as widespread. There were no noteworthy distinctions in gender biases for each income bracket, conditional on race. If the primary applicant was a female, or male, the frequencies matched that of the gender-aggregate graph. 

Next, as our data set was exclusively a result of face-to-face lending, we trained a logistic regression classifier to imitate the process of algorithmic lending, trained on publicly accessible data, the HMDA NY 2015 data set. Prior to training, we moved all racial proxies which included a maximum of 17 features for each applicant. The classifier outputted the probability of an applicant being rejected for each income bracket, conditional on race, and our visualizations compared the predicted probability as a function of the true probability of acceptance for Asian, Black, and White applicants. The other minority applicant groups were too sparsely populated to consider for this classifer. Each probability was classified as 1 of 10 different possibilities ([0,.1,.2,...,1.0]. 

We can also analyze the fairness of lending by considering the "confusion matrix" of the trained classifier – a confusion matrix is a 2x2 matrix of the classifier's true postive rate (TPR), false positive rate (FPR), false negative rate (FNR), and true negative rate (TNR).  Whites and Asians had almost identical confusion matrices – full details are included in the _processing.ipynb_ notebook. However, looking at the specificity, the classifier was less likely to mistakenly approve a black applicant for a loan (the False Positive Rate for Blacks is 18%, compared to 33% for whites ) and more likely to mistakenly reject a black applicant for a loan (the False Negative Rate for Blacks is 11%, compared to 8% for Whites). The results showed striking racial biases for applicants in the middle probabilities, whereby, under a race-blind application process, if a minority applicant was classified as a 50% chance of receiving an originated loan, they were much less likely to receive that loan than a non-minority applicant who also had a 50% chance of receiving an originated loan. These racial discrepancies were less prevalent on the lowest and highest income brackets, as we suspect those applications are highly predictable.  

## Conclusion and Future Directions
We have shown via the [ HMDA data set](https://www.consumerfinance.gov/data-research/hmda/explore) the difference in loan approval rates between different racial groups is likely due to membership in those groups. However, it is always possible that there is a confounding variable other than race which could explain the discrepancies we observed which is legal to use as part of the approval process. Additionally, our results could be strengthened if we could acquire data that would give us more information about the terms of the loans that were approved. Even if an applicant was approved, if that applicant is paying more for that loan than the applicant's peers, then that could provide further evidence of discrimination.  The dataset we used does provide the interest rate of the approved loan (the column is called "rate spread" in the dataset) but this value was not null only in about 1% of rows and so we were unable to conduct a deeper analysis using it. Knowing originated loans' interest rates' as well as other missing columns, we could have explored further potential biases in the price of originated loans for the same income bracket conditional on race. It also would have been more conclusive to analyze loan origination status by credit score and income level, conditional on race. We suspect similar trends would emerge as shown in our analyses. Information about loan features would better judge an applicant's creditworthiness. 

Fortunately these more granular data will be included in the 2018 HMDA data set.  Although the 2018 data is not yet available, as a result of the Dodd-Frank Bill will legally require lenders report the following additions for each applicant: Credit score, NMLS Identification of the loan originator, Loan channel, Borrower age, Combined loan-to-value (CLTV) ratio, Borrower's debt-to-income (DTI) ratio, Borrower-paid origination charges, Points and fees, Discount points, Lender credits, Loan term, Prepayment penalties, Non-amortizing loan features, Interest rate and Rate spread for all loans. Of course, although releasing additional information about loan applicants can help us better determine whether there are any discriminatory practices, the additional data released may raise privacy concerns. Each applicant will now have more than 61 features published about themselves, which can be easily combined with census data or other national publications. Although this may provide further insights, at the same time, this may also increase the risk of de-identification, exposing sensitive information such as an applicant’s income, credit score, and debt levels.

There must also be a push to report accurate data. Some data in the data set, probably a reporting error/mistake, indicates $99 million loans, many applicants did not report their income, may not have accurately reported their income, and denial reason(s) are inconsistent and unreliable because it is rarely required and enforced, and the denial codes are often ambiguous. There is a lack of data on both the cost and contracting structure of the loan. This is critical for lenders, to ensure they are approving loans for appropriate applicants, for governing bodies to best understand and regulate their respective lending markets, and for public officials to gauge how to meet the housing needs of communities. Any self-reporting data tool is subject to human error, implicit and explicit biases. Because this may cause corrupt data, we suggest enforceable penalties and fines for inaccurate reporting. There is also insufficient information on Hispanic applicants, a commonly marginalized ethnic group.

Algorithmic fairness incorporates questions whether there should be a focus on equal treatment or equal outcomes. This repository focuses on equal treatment and where equal treatment may fail under face-to-face lending as well as automated processes. Racially biased lending practices coupled with a market shift towards algorithmic lending, increases the risk of confirmation bias, and US Fair Lending Laws do not consider the potential for Big Data variables to illegally discriminate. This is most difficult because of "black-box" algorithms, unobservable variables, and the usage of observable proxies. This may be a result of lenders utilizing an applicant's digital footprint as a proxy for lending probability or social media activity as a proxy for trust in creditworthiness. Moreover, it is troubling to consider the ability for Fair Lending Laws to adapt to face-to-face discrimination, and algorithmic racial biases, as the lending industry is notoriously slow and resistant to adjust its laws. There are also high overhead and inefficient, costs for jurisdictional challenges and procedures. Therefore, we suggest addressing the problem of racially discriminatory lending practices in the algorithms themselves, rather than invest in highly regulated outcomes. Additional research in this field could look at discriminating the basis of sex, ethnicity, and religion. It would be valuable to repeat this analysis after the 2018 HMDA data, subject to the new Dodd-Frank regulations, requiring a substantially higher number of demographic features for each applicant. This would reveal if the status of an originated loan is more or less closely tied to racial biases. 

### Works Cited
Abe Gong Rebuttal: https://gist.github.com/abegong/7389ed1fe4a7344d49951f6bb3195a2c

Bartlett, et al. Consumer-Lending Discrimination in the Era of FinTech*. UC Berkeley, Oct. 2018, faculty.haas.berkeley.edu/morse/research/papers/discrim.pdf.

Chessen, Matt. “Encoded Laws, Policies, and Virtues: the Offspring of Artificial Intelligence and Public-Policy...” Medium, Artificial Intelligence Policy, Laws and Ethics, 31 Mar. 2017, medium.com/artificial-intelligence-policy-laws-and-ethics/encoded-laws-policies-and-virtues-the-offspring-of-artificial-intelligence-and-public-policy-3dfb357faf9.

“Fair Lending Laws.” Mortgage Compliance Magazine, www.mortgagecompliancemagazine.com/mortgage-compliance-alphabet-soups/fair-lending-laws/.

Filing Instructions Guide for HMDA Data Collected in 2018. FFIEC, Sept. 2018, s3.amazonaws.com/cfpb-hmda-public/prod/help/2018-hmda-fig-2018-hmda-rule.pdf.

Friedler, Sorelle A., Carlos Scheidegger, and Suresh Venkatasubramanian. "On the (im) possibility of fairness." arXiv preprint arXiv:1609.07236 (2016). https://arxiv.org/pdf/1609.07236.pdf. 

Jan, Tracy. “The Senate Rolls Back Rules Meant to Root out Discrimination by Mortgage Lenders.” The Washington Post, WP Company, 14 Mar. 2018, www.washingtonpost.com/news/wonk/wp/2018/03/14/the-senate-rolls-back-rules-meant-to-root-out-discrimination-by-mortgage-lenders/?noredirect=on&utm_term=.86041577a8a3.

laura_hudson. “Technology Is Biased Too. How Do We Fix It?” FiveThirtyEight, FiveThirtyEight, 20 July 2017, fivethirtyeight.com/features/technology-is-biased-too-how-do-we-fix-it/.

Matsakis, Louise. “Your Smartphone Choice Could Determine If You Get a Loan.” Wired, Conde Nast, 9 May 2018, www.wired.com/story/your-smartphone-could-decide-whether-youll-get-a-loan/.

Sam Corbett-Davies, Emma Pierson, Avi Feller, Sharad Goel, and Aziz Huq. 2017. Algorithmic Decision Making and the Cost of Fairness. In Proceedings of the 23rd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining (KDD '17). ACM, New York, NY, USA, 797-806. DOI: https://doi.org/10.1145/3097983.3098095

“What Lies Within (Your HMDA Data).” Secondary Marketing Executive Issue Library, issues.secondarymarketingexec.com/article/what-lies-within-your-hmda-data/.


 

 

