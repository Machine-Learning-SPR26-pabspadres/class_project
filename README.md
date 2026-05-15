# Class Project

My project explores the ethical compromises of large scale clothing brands in America, answering the hypothesis “is a brand inherently less ethical the larger it is?” by analyzing data about brand social and environmental responsibility. 

## Raw Data 
The raw data from this project comes from multiple sources, mainly tools and databases from human rights associations such as the fashion checker and facility checker from the Clean Clothes Campaign, which provides information on living and actual wages for garment workers. Most of the data for the project is quantitative, whether it is binary or is a normalized score, because I am looking to gather enough data to create a unique score for each brand.

## Data Analysis
To analyze the data and draw the necessary conclusions, I have designed an Ethical Compliance Index, which measures how much a brand aligns with ethically acceptable standards based on their social and environmental impact. The metric is comprised of 6 metrics: Social Transparency, Environmental Impact, Supply Chain Transparency, Human Rights Risk & Responsiveness, Labor Compensation, and Value Distribution Equity. 

## Ethical Compliance Index: 
A normalized score (0-100) that indicates how ethical a brand's practices are, with 100 being the best and 0 being the worst. The index score for each brand is conformed of 6 metrics that are all normalized scores as well in order to maintain consistency and straightforward calculations. 3 metrics are scores directly extracted from trusted sources and 3 are calculated through a formula developed by me through extensive research and machine learning (PCA). 

## Extracted Score Metrics: 
For these metrics, the data extracted from the sources (the already built scores) was simply put directly into a spreadsheet that includes all the brands I am analyzing (32) and each of the sections for the metric scores. 
### Social Transparency: 
Extracted normalized scores from the Fashion Transparency Index by Fashion Revolution, which provides scores from 2023 grading the brand on their public disclosure on social and environmental impact, encompassing both concepts of ethics highlighted in this project, making this metric about overall transparency. 
### Environmental Impact: 
Extracted normalized scores from the What Fuels Fashion analysis by Fashion Revolution, which provides scores from 2025 grading the brand on their disclosure of their climate and energy-related policies, practices and impacts in their operations. 
### Supply Chain Transparency: 
Extracted normalized scores from a dataset from the Supply Chain Transparency Score from the The Clean Clothes Campaign through Wikirate. The original scores were set in a 4 point scale, which wikirate translated to a 10 point scale (1 = 2.5). In order to keep consistency with this project’s 100 point scale, these scores were normalized (1 = 2.5 = 25). 

## Calculated Score Metrics: 
For the calculated score metrics, I first run the extracted raw data through PCA on a jupyter notebook. Once I get my final weighted scores, I input them into my spreadsheet.
### Human Rights Risk & Responsiveness: 
This metric uses data extracted from the Business & Human Rights Centre, which provides data on news and allegations relating to the human rights impact of brands and their response if any. The specific data taken from this source for each brand is:
- HRD Attacks: Threats, violence or harassment towards Human Rights Defenders who are working to stop business-related human rights violations. 
- Response Requests: If there is an allegation with no public record of a brand response towards the allegation, the BHRC sends the brand a request to respond towards the allegation. 
- Response Rate: Tracks how many of the response requests the brand answers.
- Other Allegations: Allegations not related to response requests.
After extracting the data, I ran it through jupyter notebook utilizing pca to calculate weight and scoring metrics for each of these subsections in order to determine how the 4 together compute the total Human Rights Risk & Responsiveness score for each brand. 
I merged HRD Attacks and Other Allegations together in order to build a “Severity Score”. I used PCA to derive weights for different types of human rights violations based on their contribution to variance across brands, replacing subjective weighting schemes with an empirical, data-driven approach.While I calculated this severity sub-score to analyze variation in violation types, it is not part of the computation for the Human Rights Risk & Responsiveness score. 
Prior to analysis, I aligned all variables so that higher values indicated worse performance; specifically, I inverted the response rate so all scores were consistent in their direction.
To derive variable weights, I applied PCA to the standardized dataset. PCA identified the linear combination of variables that identified the greatest variance across observations, determining weights empirically. I I used the first principal component (PC1), which explained the largest share of variance, to extract variable loadings. Absolute loadings were normalized to sum to one, producing a set of data-driven weights.
I then calculated the  raw HRRR score as a weighted sum of the four variables. Finally, I normalized the scores like the rest of my metrics (0-100) and inverted it so that higher values represented a better performance.
This approach ensures a balanced assessment of brand behavior, capturing both risk exposure (allegations and case volume) and accountability (responsiveness), while minimizing subjective bias in the weighting process.

### Labor Compensation
To construct the metric, supplier relationship data was first extracted through Wikirate’s API using Python within a Jupyter Notebook environment. The extraction relied on Wikirate’s “Commons + Supplied By” relationship metric, which aggregates brand supplier disclosures from multiple public sources into a unified supplier relationship database. Through the API, supplier-facility associations tied to each brand included in the analysis were collected alongside facility identifiers, relationship types, and disclosure years.
Once supplier relationships were extracted, supplier profile data was pulled through Wikirate’s company profile endpoints using each facility’s unique Wikirate identifier. This process allowed for the extraction of supplier headquarters locations, which were subsequently normalized into a country-level geographic dataset. The resulting supplier network database consisted of more than 12,000 supplier-brand relationships and over 6,000 unique supplier facilities distributed across multiple production regions.
Country-level wage data was then manually compiled through WageIndicator and the Valuing Impact 2023-2024 dataset. WageIndicator provided the monthly minimum wage per country, with some countries having a standard and national minimum wage, and others differentiating wages depending on industry, profession, and region. In these cases, the lowest wage within production, manual labor or garment work was selected in order to estimate the worst-case scenario.  Valuing Impact’s dataset provided the monthly living wage for countries at different levels based on geographic location within the country, marital status, and dependents. For this analysis, the living wage selected was that of a single worker, with no dependents, and living in an urban area. 
After both datasets were standardized and normalized within the Jupyter Notebook environment, supplier countries were merged with the WageIndicator and Valuing Impact datasets to calculate country-level labor risk scores. To quantify wage-related labor risk, a wage ratio was calculated for each country using the following formula:​
Wage Ratio=Minimum WageLiving Wage
This ratio captures the degree to which statutory wages are capable of meeting estimated living standards within each country. Countries where minimum wages closely matched or exceeded living wages produced ratios closer to 1, indicating lower structural wage risk. Conversely, countries where minimum wages fell substantially below living wages produced lower ratios, indicating greater risk of wage insufficiency for workers.
The wage ratio was then inverted into a country risk score through the following calculation:
Country Risk=1-Wage Ration
Through this transformation, countries with larger gaps between minimum and living wages generated higher risk values, while countries with smaller gaps generated lower risk values. These country-level risk scores were merged onto the supplier network database based on supplier location and aggregated at the brand level through Python-based data processing within the Jupyter Notebook workflow.
To construct the final Labor Compensation score for each brand, average country risk was calculated across each brand’s unique supplier facilities. Supplier facilities were treated as equally weighted due to the lack of publicly available production volume data that would allow for more precise weighting by manufacturing output or sourcing dependence. Brands with insufficient supplier coverage (American Eagle Outfitters) were flagged as low-data observations and excluded from analytical interpretation where appropriate.
Finally, the aggregated country risk was converted into a normalized 0–100 score through the following formula:
Labor Compensation Score=100(1-Average Country Risk)
An important factor to consider is that Wikirate’s database did include data for most brands of the analysis, but not all. Additionally, in some cases, the dataset only included data for parent companies rather than specific brands. In these cases, the scores for a parent company were equally applied to its subsidiary brands in the analysis; for example, Calvin Klein and Tommy Hilfiger hold the same score as they are both part of PVH. In the case of brands whose data was not included in the Wikirate dataset, in order to not dismiss them completely with a score of 0, and as per the instructions of one of my advisors, I applied the minimum score of the dataset (American Eagle Outfitters). I found this to be an efficient solution as American Eagle received this score due to its Low Data status, which would apply to the brands with no data available. Please browse the chart below to better understand how brands were measured.


