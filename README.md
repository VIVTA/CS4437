# Predicting the 2015 Canadian Federal Election Using Twitter 
####Vivian Tan
#####Schulich School of Medicine and Dentistry, Western University, Canada

###Abstract
Twitter can be mined to understand and predict public opinion.  We analyzed 48,717 tweets from October 12th to October 18th, leading up to the 2015 Canadian federal election. A total of 52 aggregated tweet features (including tweet, retweet, user, hashtag, link and sentiment counts/proportions) were compared to results from public opinion polls as well as final election results and selected using LASSO regression. This study aims to: (1) establish which features overall best predict voting share per party; (2) determine which methods used to compute sentiment twitter features best predict voting shares and (3) ascertain if the best predictors vary depending on the type of poll used as the outcome.  

###Introduction
The 42nd Canadian federal election was held on October 19th, 2015.  With one of the longest campaigns in Canadian history, the election encouraged voters from across the country to engage in open discussions on national issues.  

The traditional gold standard for public opinion polling is telephone surveys.  However, these are time-consuming, expensive and with dropping response rates, have become increasingly difficult to conduct (Tao & Reis-Smart, 2014).   As a result, the industry has looked for alternate methods of population sampling. Social media can be used to understand and predict public opinions and trends.  One platform is Twitter, a microblog where users can share 140-character "tweets."

A generalizable method to forecast election results using Twitter has yet to be established. Most of the early work in election predictions based solely on tweet counts are unreliable (O'Leary, 2015).  Using sentiment analysis has been shown to outperform tweet counting, but overall performances have been variable. Past studies using sentiment analysis methods have been criticized for not applying state-of-the-art techniques available in the field (Gayo-Avello, 2013).  Therefore, there is no consensus to which sentiment analysis methods best predict election outcomes. Additionally, there may be other Twitter features that could be better predictors.  

There has also been variability on the type of polls that are used as baseline. Since the type of polling method can influence performance, the choice of poll used in the regression could impact its predictions.  We will determine which Twitter features best predict election outcomes and whether this selection is affected by the polling method used for the dependent variable.  

To our knowledge, no previous studies have looked at election predictions using Twitter in Canada.  As a result, this paper builds on existing literature by extending twitter prediction methods to the Canadian context.  
  
###Methods
####Data
We examined a total of 48,717 tweets that were posted between October 12th, 2015 and October 18th, 2015.  Consistent with past studies, we finished data collection the day before the election (Gayo-Avello, 2013).  We collected all tweets that contained at least one Canadian political hashtag (#canpoli, #cdnpoli), Canadian election hashtag (#elxn2015, #elxn42) or one of the 3 major party hashtags (#cpc, #lpc, #ndp) using the application IFTTT.  Our dataset included the features date/time, username, tweet and hyperlink. Data collection over a one week period before the election has been used by many studies in the past that conducted similar analyses (Ceron, Curini, Iascus, and Porro, 2013; Metaxas, Mustafarj, and Gayo-Avello, 2011; Tjong Kim Sang and Bos, 2012).  

Pre-processing of tweets included converting all tweets into lowercase, removing duplicates and excluding tweets that were not in the English language.  

We used the daily poll results from EKOS that poll by interactive voice response (http://www.ekospolitics.com), Nanos Research that poll by telephone (http://www.nanosresearch.com) and Eric Grenier's Poll Tracker that uses weighted poll averages when training our model (Canadian Broadcasting Corporation, 2015).  

####Features
We assessed a variety of tweet features.  The data set was aggregated to generate twitter features which include tweet counts/proportions, retweet counts/proportions, twitter user counts/proportions, hashtags counts/proportions, link counts/proportions for each party and for each day.  

**Table 1. Twitter features and definitions (for each day)**

Feature    |Definition                              | Formula                                                    
-----------|----------------------------------------|---------------------------------------------------------------------------------------------------
Tweet Count	|Number of tweets that mention a particular party (or candidate from party) |	<sub># of tweets that mention party X</sub>
Tweet Proportion |Percentage of tweets that mention a particular party (or candidate from party) |$\frac{\#oftweetsthatmentionpartyX}{totalnumberoftweets}$	
Retweet Count|	Number of retweets that mention a particular party (or candidate from party)|	<sub># of retweets that mention party</sub>
Retweet Proportion|	Percentage of retweets that mention a particular party (or candidate from party)|$\frac{\#ofretweetsthatmentionpartyX}{totalnumberofretweets}$	
Unique Tweet Count|	Number of tweets that mention a particular party (or candidate from party)|	<sub># of tweets that mention party X</sub>
Unique Tweet Proportion|	Percentage of tweets that mention a particular party (or candidate from party)|$\frac{\#oftweetsthatmentionpartyX}{totalnumberoftweets}$
User Count|	Number of twitter users that mention a particular party (or candidate from party)| <sub># of twitter users that mention party X</sub>
User Proportion| Percentage of twitter users that mention a particular party (or candidate from party)|$\frac{\#oftwitterusersthatmentionpartyX}{totalnumberoftwitterusers}$
Hashtag Count|	Number of tweets with a particular party's hashtag| <sub># of tweets with party X hashtag</sub>
Hashtag Proportion|	Percentage of tweets with a particular party's hashtag out of all tweets|$\frac{\#oftweetswithpartyXhashtag}{totalnumberoftweets}$
Links Count|	Number of tweets that mentions a particular party (or candidate from party) and includes a hyperlink|	<sub># of tweets with a link that mention party X</sub>
Links Proportion|	Percentage of tweets that mentions a particular party (or candidate from party) and includes a hyperlink|$\frac{\#oftweetswithalinkthatmentionpartyX}{totalnumberoftweetswithalink}$
Positive Tweet Count|Number of tweets with a positive sentiment that mention particular party (or candidate from party| <sub># of positive tweets that mention party X</sub>
Positive Tweet Proportion|	Percentage of tweets with a positive sentiment that mention a particular party (or candidate from party) out of all tweets|$\frac{\#ofpositivetweetsthatmentionpartyX}{totalnumberoftweets}$
Positive Tweet Share| Percentage of tweets with a positive sentiment that mention a particular party (or candidate from party) out of all tweets with a positive sentiment|$\frac{\#ofpositivetweetsthatmentionpartyX}{totalnumberofpositivetweets}$
Neutral Tweet Count|	Number of tweets with a neutral sentiment that mention particular party (or candidate from party)| <sub># of neutral tweets that mention party X</sub>
Neutral Tweet Proportion|	Percentage of tweets with a neutral sentiment that mention a particular party (or candidate from party) out of all tweets|$\frac{\#ofneutraltweetsthatmentionpartyX}{totalnumberoftweets}$
Neutral Tweet Share|	Percentage of tweets with a neutral sentiment that mention a particular party (or candidate from party) out of all tweets with a neutral sentiment|$\frac{\#ofneutraltweetsthatmentionpartyX}{totalnumberofneutraltweets}$ 
Negative Tweet Count|	Number of tweets with a negative sentiment that mention particular party (or candidate from party)| <sub># of negative tweets that mention party X</sub>
Negative Tweet Proportion|	Percentage of tweets with a negative sentiment that mention a particular party (or candidate from party) out of all tweets|$\frac{\#ofnegativetweetsthatmentionpartyX}{totalnumberoftweets}$
Negative Tweet Share|	Percentage of tweets with a negative sentiment that mention a particular party (or candidate from party) out of all tweets with a negative sentiment|$\frac{\#ofnegativetweetsthatmentionpartyX}{totalnumberofnegativetweets}$

We used regular expressions to determine if a tweet mentioned any one of the three major parties (Liberal, Conservatives, NDP). A tweet was classified as Liberal if it included any of the following terms: "lpc"," lib", "libs", "liberal", "liberals", "trudeau" or "grits".  A tweet was classified as Conservative if it included: "cpc", "cons", "conservative", "conservatives", "harper" or "tories".  Finally, a tweet was classified as NDP if it included:  "ndp", "democrat", "democrats" or "mulcair".  

In addition, we also examined sentiment where positive counts/proportions/shares, neutral counts/proportions/shares and negative counts/proportions/shares for each party and for each day were computed.  We used the top three sentiment methods (VADER, AFINN, Opinion Lexicon) for 3-class experiments from a recent benchmark comparison (Ribero et al., 2015).  

The Opinion Lexicon by Hu and Liu was used in many early election prediction models using twitter (Gayo-Avello, 2013). Originally used for product reviews, the Opinion Lexicon has 2006 positive words and 4783 negative words including misspellings, slangs and social media mark ups (Hu and Liu, 2004).  We used the python Natural Language Toolkit (NLTK) which returns "positive", "neutral" or "negative" for each string of text.  

AFINN is a sentiment lexicon developed specifically for microblogs, such as Twitter.  It has the ability to recognize obscene words and internet slangs.  Scoring is based on an annotated list of words with scores developed by Finn Arup Nielsen.  Unlike the previous sentiment methods, AFINN returns a polarity score between -5 to 5 indicating the direction as well as the strength of the sentiment, where a score of -5 is "extremely negative" and a score of +5 is "extremely positive." A score of zero that is "neutral" could mean that no charged words were found or the positive and negative words balanced themselves out (Nielsen, 2011).   We used the AFINN implementation from Data Pig Technologies to compute the polarity score for each tweet.  To fit the raw polarity scores into the three classes to calculate the positive, neutral and negative counts/proportions/shares, we categorized tweets with a scores of -5, -4 ,-3, -2 or -1 as "negative", scores of 0 as "neutral" and scores of +5, +4, +3, +2 or +1 as "positive" similar to past studies (Ribero et al., 2015). We also included the average and sum of the AFINN polarity scores for each day and for each party as an aggregated twitter feature.  

Valence Aware Dictionary for Sentiment Reasoning (VADER) is a rule-based sentiment-analysis method created from a validated gold standard lexicon attuned for social media contexts (Hutto and Gilbert, 2014).  We used the python Natural Language Toolkit (NLTK) which returns composite scores ranging from -1 to 1 for each string of text.  To classify into three classes, tweets with composite scores less than -0.05 were categorized as "negative", scores greater or equal to -0.05 and less than or equal to 0.05 were categorized as "neutral" and scores greater than 0.05 were categorized as positive. The average and sum of composite scores for each party and each day were also included as a feature.  

In addition, we also used the built-in sentiment analysis classifier in Mathematica, a symbolic mathematical computation program which returns "positive", "neutral" or "negative" sentiment for each string of text.  

####Analysis
To select for the best predictors out of all the twitter features, we used a lasso (Least Absolute Shrinkage and Selection Operator) regression algorithm in MATLAB.  It imposes a constraint on the coefficient, where the coefficients of non-relevant variables will be set to zero (Tibshirani, 1994).  We used the model with the smallest value of lambda.  Correlation between the Twitter features and the poll results also was calculated.  This will repeated using each type of poll as the dependent variable.  The performance of the model will be assessed by mean squared error (James, Witten, Hastie, Tibshirani, 2013).  

###Results
From October 12th to October 18th, there were 15,875 twitter users who tweeted 48,717 unique tweets with hashtags (#canpoli, #cdnpoli, #elxn2015, #elxn42, cpc, #lpc, #ndp) regarding the 2015 Canadian Federal Election.  

**Figure 1. Retweet (pink) and unique tweet (purple) counts for tweets mentioning the Liberals, Conservatives or NDP from October 12th to October 18th 2015**

![](https://github.com/VIVTA/CS4437/blob/master/fig2.jpg)

Figure 1 shows the total number of tweets, retweets and unique tweets for each party posted from October 12th to October 18th.  The majority of tweets are retweets (in pink) rather than new tweets (purple), with 65% of all tweets in the dataset retweets.  The figure also shows across all 7 days, there were more tweets mentioning the conservative party followed by the liberal party with the least amount of tweets mentioning the NDP.  It is intresting to note that there is a decline in the number of tweets across all three parties on the last day (October 18th) before the election.  This occurence may be related to a new hashtag (#CanadaVotes) not available in our dataset, that was promoted during the CBC election show aired that day.  

As shown in Supplementary Figure 1, 1833 twitter users only posted tweets regarding the Liberals, 3643 twitter users only tweeted regarding Conservatives, 1159 twitter users only tweeted regarding the NDP while 2000 twitter users posted tweets regarding all three parties.  

A comparison of the total number of positive, neutral and negative tweet counts for all four sentiment methods from October 12th to October 18th are shown in Figure 2 for the Liberals, Conservatives and NDP respectively.  Mathematica markedly classifies more tweets as neutral, while VADER classifies more tweets as positive compared to the other sentiment methods across the 7 days.  In addition, the Conservatives were associated with a higher proportion of tweets with a negative sentiment as compared to the other two parties.  This may be influenced by the trending #stopharper and  strategic campaign that was popular during the election period.  

Coefficients and correlation from the lasso regression model are listed in Supplementary Table 1.  The lasso model using poll tracker labels had an intercept of -0.6376, a lambda of 0.0032 and a mean squared error of 0.0308.  The lasso model using NANOS labels had an intercept of -7.0258, a lambda of 0.0037 and a mean squared error of 0.0356.  The lasso model using EKOS had an intercept of 13.1439, a lambda of 0.0034 and a mean squared error if 0.0292.  

The relevant features included in the lasso model differed depending on the type of poll that was used as the dependent variable as visualized in the alluvial digram in Figure 3 and circular dendrogram in Supplementary Figure 2.

**Figure 2. Sentiment tweet counts for tweets mentioning the Liberals, Conservatives and NDP from October 12th to October 18th 2015 using Mathematica (M), Opinion Lexicon (H), AFINN (A) and VADER (V)**

Party                       | Sentiment
----------------------------|------------------     
**Liberal**                 | ![](https://github.com/VIVTA/CS4437/blob/master/3a.jpg)
**Conservative**            | ![](https://github.com/VIVTA/CS4437/blob/master/3b.jpg)
**New Democratic**          | ![](https://github.com/VIVTA/CS4437/blob/master/3c.jpg)

**Figure 3. Flow of the significant twitter features in the Poll Tracker, NANOS and EKOS LASSO models**

<img src="https://github.com/VIVTA/CS4437/blob/master/flow.png" height="600px" width="500px" />  

**Figure 4. Parallel coordinates demonstrating the change in coefficents of twitter features for Poll Tracker, NANOS and EKOS LASSO models**

<img src="https://github.com/VIVTA/CS4437/blob/master/parallel.png" height="600px" width="500px" />

Unique twitter proportion, hashtag count, link proportion, positive proportion (Mathematica), positive proportion (VADER), positive share (Hu), positive share (Mathematica), neutral count (Hu), neutral proportion (VADER), neutral share (AFINN), negative count (AFINN), negative proportion (Hu), negative proportion (Mathematica), negative share (Hu), Negative Share (Mathematica), polarity score average (AFINN) and polarity score sum (VADER) were included in all three lasso regression model.  

Positive count (Hu) and neutral count (VADER) were included in the Poll Tracker and NANOS models, but not the EKOS model.  In addition, user count, link count and positive share (AFINN) were only in the Poll Tracker lasso model. Positive proportion (Hu), positive share (VADER) and negative share (VADER) were included only in the NANOS model and while positive count (Mathematica) and neutral proportion (AFINN) were included only in the EKOS model.  This pattern of varying coefficients is shown in Figure 4 as there were features with large coefficients that were not constant across all three models.

Polarity score average is a better predictor of election success using the AFINN sentiment than VADER, while expressing the polarity score as a sum is a better predictor when using scores based off VADER sentiment than AFINN.  

###Discussion

Our results show which twitter features best predict voting share per party.  We found that the best sentiment method depended on the sentiment feature and demonstrated that the relevant predictors change depending on the type of poll that is used as the dependent variable when training.  

Our study has a number of strengths. To our knowledge, we are the first study to compare and establish the best features of tweets for predicting election voting shares.  Moreover, we are the first to study election predictions in Canada.  

 However, there are several limitations to our study.  Unlike past studies that collected tweets based on the name of the parties or candidates as key words, our data was collected based on hashtags (#canpoli, #cdnpoli, #elxn2015, #elxn42, #cpc, #lpc, #ndp).  As a result, there may have been selection bias as our data collection method would have missed tweets related to the election that did not use one of the specified hashtags.  Although analysis was conducted post-election, data collection occurred in real-time which is consistent with Gayo-Avello's recommendations.   

Another, limitation to our data is that the Twitter demographic is a non-random sample and therefore not representative of the entire voting population.  For example, Twitter users are generally younger with 65% under the age of 25 (Sysomos, 2009).  Since Twitter user characteristics such as age are not available, we could not adjust for the distribution accordingly.  In addition, our dataset did not include user location, therefore it was not possible to make predictions based on political riding.  

Tsakalidis et al. collected data for more than six weeks and found that longer training window sizes tend to have lower mean absolute error.  Although, we only collected and trained data over a one week period before the election, many studies in the past have also used one week of data [Metaxas, Mustafarj, and Gayo-Avello, 2011; Tjong Kim Sang and Bos, 2012; Ceron, Curini, Iascus, and Porro, 2013].  

These results can guide future applications in election prediction using twitter in Canada.  

###References

Canada Broadcasting Corporation. (2015). Eric Grenier's Poll Tracker.  Retrieved from http://www.cbc.ca/news2/interactives/poll-tracker/2015/index.html

Ceron, A., Curini, L., Iacus, S. M., & Porro, G. (2014). Every tweet counts? How sentiment analysis of social media can improve our knowledge of citizens' political preferences with an application to Italy and France. New Media & Society, 16(2), 340-358.

Gayo-Avello, D. (2013). A meta-analysis of state-of-the-art electoral prediction from Twitter data. Social Science Computer Review, 31(6), 649-679.

Hastie, T., James, G., & Witten, D. (2013). Introduction to statistical learning: With applications in R. New York, NY: Springer New York. 

Hu, M., & Liu, B. (2004). Mining and summarizing customer reviews. In Proceedings of the tenth ACM SIGKDD international conference on Knowledge discovery and data mining (pp. 168-177). ACM.

Hutto, C. J., & Gilbert, E. (2014). Vader: A parsimonious rule-based model for sentiment analysis of social media text. In Eighth International AAAI Conference on Weblogs and Social Media.

O'Leary, D. (2015). Twitter Mining for Discovery, Prediction and Causality: Applications and Methodologies.  Intelligent Systems in Accounting, Finance and Management, 22, 227-247.

Metaxas, P. T., Mustafaraj, E., & Gayo-Avello, D. (2011, October). How (not) to predict elections. In Privacy, Security, Risk and Trust (PASSAT) and 2011 IEEE Third Inernational Conference on Social Computing (SocialCom), 2011 IEEE Third International Conference. IEEE Computer Society, Los Alamitos, CA.

Nielsen, F. Å. (2011). A new ANEW: Evaluation of a word list for sentiment analysis in microblogs. arXiv preprint arXiv:1103.2903.

Ribeiro, F., Araújo, M., Gonçalves, P., Benevenuto, F., & André Gonçalves, M. (2015). A Benchmark Comparison of State-of-the-Practice Sentiment Analysis Methods. arXiv preprint, arXiv:1512.01818.

Sang, E. T. K., & Bos, J. (2012, April). Predicting the 2011 dutch senate election results with twitter. Paper presented at the 13th Conference of the European Chapter of the Association for Computational Linguistics. Avignon, France. 

Sysomos. (2009). An In-Depth Look Inside the Twitter World. Retrieved from http://www.sysomos.com/in side-twitter

Tao, S. & Reis-Smart, H. (2014). The Key Cause of Polling Quality Deterioration. Retrieved from Marketing Research Association: http://www.marketingresearch.org /article/key-cause-polling-quality-deterioration

Tibshirani, R. (1996). Regression shrinkage and selection via the lasso. Journal of the Royal Statistical Society, 58(1), 267-288.  

###Appendix

**Supplementary Table 1. Coefficients and correlations for lasso regression of twitter features and poll tracker, NANOS and EKOS poll results**

Twitter Feature             | Poll Tracker | NANOS | EKOS  | Correlation (PT)|
----------------------------|--------------|-------|-------|-----------------|
Tweet Count	                |0             |0	     |0	     |0.5548
Tweet Proportion            |0	           |0	     |0      |0.5592
Retweet Count	              |0	           |0	     |0      |0.5759
Retweet Proportion	        |0	           |0	     |0	     |0.6230
Unique Tweet Count	        |0	           |0	     |0	     |0.4962
Unique Tweet Proportion	    |13.9573	     |39.3438|23.1156|0.5546
User Count	                |0.0011	       |0	     |0	     |0.5444
User Proportion	            |0	           |0	     |0	     |0.5650
Hashtag Count	              |-0.0197	     |-0.0183|-0.0202|0.2126
Hashtag Proportion	        |0	           |0	     |0	     |0.3498
Link Count	                |-0.0048	     |0	     |0	     |0.5164
Link Proportion	            |-140.444	     |-109.8339|-220.255|0.5595
Positive Count (AFINN)	    |0	           |0	     |0	     |0.6230
Positive Count (Hu)	        |-0.0021	     |-0.0113|0	     |0.6411
Positive Count (Mathematica)|0	           |0	     |0.0408 |0.6387
Positive Count (VADER)	    |0	           |0	     |0	     |0.6360
Positive Proportion (AFINN)	|0	           |0	     |0	     |0.7306
Positive Proportion (Hu)	  |0	           |-8.9487|0	     |0.7430
Positive Proportion (Mathematica)|178.0365 |245.3763|255.0275|0.6669
Positive Proportion (VADER) |-4.7619	     |-7.421 |-23.1964|0.7251
Positive Share (Hu)	        |38.8639	     |29.1844|46.1954|0.7249
Positive Share (Mathematica)|3.2281	       |37.569 |92.0859|0.7539
Positive Share (VADER)	    |0	           |24.3897|0	     |0.7654
Positive Share (AFINN)	    |40.591	       |0	     |0	     |0.7245
Neutral Count (AFINN)	      |0	           |0	     |0      |0.5599
Neutral Count (Hu)	        |0.018	       |0.013	 |0.027	 |0.5649
Neutral Count (Mathematica)	|0	           |0	     |0	     |0.5171
Neutral Count (VADER)	      |0.0002	       |0.002	 |0	     |0.5662
Neutral Proportion (AFINN)	|0	           |0	     |4.7309 |0.6105
Neutral Proportion (Hu)	    |0	           |0	     |0	     |0.5706
Neutral Proportion (Mathematica)|0   	     |0	     |0	     |0.5568
Neutral Proportion (VADER)  |374.0039	     |392.8861|268.186|0.5986
Neutral Share (AFINN)	      |35.498	       |14.3298|39.7363|0.6117
Neutral Share (Hu)	        |0	           |0	     |0	     |0.6182
Neutral Share (Mathematica)	|0	           |0	     |0	     |0.5640
Neutral Share (VADER)	      |0	           |0	     |0	     |0.5950
Negative Count (AFINN)	    |0.0619	       |0.0738 |0.0162 |0.4622
Negative Count (Hu)	        |0	           |0	     |0	     |0.4267
Negative Count (Mathematica)|0	           |0	     |0	     |0.4562
Negative Count (VADER)	    |0	           |0	    |0	     |0.4234
Negative Proportion (AFINN)	|0	           |0	     |0	     |0.4819
Negative Proportion (Hu)	  |-256.609	     |-370.0293|-232.2473|0.4437
Negative Proportion (Mathematica)|-395.524 |-363.6325 |-19.3735	|0.5026
Negative Proportion (VADER)	|0	           |0	     |0	     |0.4477
Negative Share (AFINN)	    |0	           |0	     |0	     |0.4982
Negative Share (Hu)	        |-60.8706	     |-73.8953|-50.6668|	0.4523
Negative Share (Mathematica)|30.8514	     |35.815 |13.7605|0.5420
Negative Share (VADER)	    |0	           |-7.0992|0	     |0.4575
Polarity Score Average (AFINN)|-6.0103	   |-2.8055|-45.3275|-0.1899
Polarity Score Average (VADER)|0	         |0	     |0	      |-0.2476
Polarity Score Sum (AFINN)	  |0	         |0	     |0	      |-0.0253
Polarity Score Sum (VADER)	  |0.0265	     |0.0207 |-0.0066	|-0.0496

**Supplmentary Figure 1. Number of unique twitter users tweeting about the Liberals, Conservative and NDP**  
![](https://github.com/VIVTA/CS4437/blob/master/venn.jpg)

**Supplmentary Figure 2. Relationship between relevant twitter features and Poll Tracker, NANOS and EKOS Lasso models**  
![](https://github.com/VIVTA/CS4437/blob/master/twitfeet.png)

**Supplementary Figure 3. Wordclouds for #LPC. #CPC and #NDP**
![](https://github.com/VIVTA/CS4437/blob/master/wordcloud.jpg)

**Supplementary Figure 4. Collage of twitter profile pictures of users who tweeted regarding the election from October 12th to October 18th 2015**

![](https://github.com/VIVTA/CS4437/blob/master/collage.jpg)


