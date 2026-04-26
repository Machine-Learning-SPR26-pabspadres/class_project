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
### Labor Compensation: still working on this
### Value Distribution Equity: still working on this 

