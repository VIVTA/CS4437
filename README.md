# Predicting the 2015 Canadian Federal Election Using Twitter 
####Vivian Tan
#####Schulich School of Medicine and Dentistry, Western University, Canada
###Abstract
Twitter can be mined to understand and predict public opinion.  We analyzed 48,717 tweets from October 12th to October 18th, leading up to the 2015 Canadian federal election. A total of 52 aggregated tweet features (including tweet, retweet, user, hashtag, link and sentiment counts/proportions) were compared to results from public opinion polls and final election results and selected using LASSO regression. This study aims to: (1) establish which features overall best predict voting share per party; (2) determine which methods used to compute sentiment twitter features best predict voting shares and (3) ascertain if the best predictors vary depending on the type of poll used as the outcome.
###Introduction
The 42nd Canadian federal election was held on October 19th, 2015.  With one of the longest campaigns in Canadian history, the election encouraged voters from across the country to engage in open discussions on national issues.  

The traditional gold standard for public opinion polling is telephone surveys.  However, these are time-consuming, expensive and with dropping response rates, have become increasingly difficult to conduct (Tao & Reis-Smart, 2014).   As a result, the industry has looked for alternate methods of population sampling. Social media can be used to understand and predict public opinions and trends.  One platform is Twitter, a microblog where users can share 140-character “tweets.”

A generalizable method to forecast election results using Twitter has yet to be established. Most of the early work in election predictions based solely on tweet counts are unreliable (O’Leary, 2015).  Using sentiment analysis has been shown to outperform tweet counting, but overall performances have been variable. Past studies using sentiment analysis methods have been criticized for not applying state-of-the-art techniques available in the field (Gayo-Avello, 2013).  Therefore, there is no consensus to which sentiment analysis methods best predict election outcomes. Additionally, there may be other Twitter features that could be better predictors.  

There has also been variability on the type of polls that are used as baseline. Since the type of polling method can influence performance, the choice of poll used in the regression could impact its predictions.  We will determine which Twitter features best predict election outcomes and whether this selection is affected by the polling method used for the dependent variable.  

To our knowledge, no previous studies have looked at election predictions using Twitter in Canada.  As a result, this paper builds on existing literature by extending twitter prediction methods to the Canadian context.  

###Methods
####Data
We examined a total of 48,717 tweets that were posted between October 12th,, 2015 and October 18th, 2015.  Consistent with past studies, we finished data collection the day before the election (Gayo-Avello, 2013).  We collected all tweets that contained at least one Canadian political hashtag (#canpoli, #cdnpoli), Canadian election hashtag (#elxn2015, #elxn42) or one of the 3 major party hashtags (#cpc, #lpc, #ndp) using the application IFTTT.  Our dataset included the features date/time, username, tweet and hyperlink.  

Data collection over a one week period before the election has been used by many studies in the past that conducted similar analyses (Ceron, Curini, Iascus, and Porro, 2013; Metaxas, Mustafarj, and Gayo-Avello, 2011; Tjong Kim Sang and Bos, 2012).  

Pre-processing of tweets included converting all tweets into lowercase, removing duplicates and excluding tweets that were not in the English language.  

We used the daily poll results from EKOS that poll by interactive voice response (http://www.ekospolitics.com), Nanos Research that poll by telephone (http://www.nanosresearch.com) and Eric Grenier’s Poll Tracker that uses weighted poll averages when training our model (Canadian Broadcasting Corporation, 2015).  

####Features
We assessed a variety of tweet features.  The data set was aggregated to generate twitter features which include tweet counts/proportions, retweet counts/proportions, twitter user counts/proportions, hashtags counts/proportions, link counts/proportions for each party and for each day.  See Table 1 for a complete list with definitions.  

We used regular expressions to determine if a tweet mentioned any one of the three major parties (Liberal, Conservatives, NDP). A tweet was classified as Liberal if it included any of the following terms: “lpc”,” lib”, “libs”, “liberal”, “liberals”, “trudeau” or “grits”.  A tweet was classified as Conservative if it included: “cpc”, “cons”, “conservative”, “conservatives”, “harper” or “tories”.  Finally, a tweet was classified as NDP if it included:  “ndp”, “democrat”, “democrats” or “mulcair”.  

![](https://github.com/VIVTA/CS4437/blob/master/fig2.jpg)

