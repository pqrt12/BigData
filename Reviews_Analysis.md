Amazon review data file  
https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Wireless_v1_00.tsv.gz  
is studied in this challenge.

The ETL is done in notebook [challengeETL.ipynb](https://github.com/pqrt12/BigData/blob/master/Challenge_ETL.ipynb). The google colab could be directly launched from Github. To run it successfully, an AWS postgreSQL should be running with four tables created properly. The configuration may be uploaded to the google colab from the local computer when prompted, or manually uploaded, or change the code directly.
The Amazon review file has a total of 9,002,021 records. After some cleaning (remove  records with "na", and with duplicated "review_id"), 9,001,590 records are kept. After some transforming, the data is loaded to postgreSQL tables "review_id_table", "products", "customers", and "vine_table", after about a LONG hour.

The Analysis is done in [challenge_Analysis_new.ipynb](https://github.com/pqrt12/BigData/blob/master/Challenge_Analysis_new.ipynb). beyond the same filtering done in ETL, only the influential opinions ('total_votes' > 10, and 'helpful_votes' > 3) are kept. There are 142,586 'non_vine' reviews with average 'star_rating' 3.45, and 1,047 'vine' reviews with average 'star_rating' 3.88. See the "pySpark Statistics'' in the notebook. After the groupby operations, an aggregated small DataFrame is generated, and it is transformed to a panda dataframe.  
With pandas, we plot both 'vine' and 'non_vine' 'star_rating' distribution. It seems 'non_vine' reviews are more emotional: 5-star reviews count ~48%, 1-star reviews count 26%, they write the reviews either because they are very happy with the products, or upset; in other cases, they just seem not bothered. The 'vine' reviews seem more rational, maybe because they just have to come out to write about it. 
![star_distribute.png](https://github.com/pqrt12/BigData/blob/master/star_distribute.png)  
Another finding is that 'vine' reviews seem to get more 'helpful_votes' and 'total_votes' when their 'star_rating' is higher, while 'non_vine' reviews seem largely flat across all 'star_rating'.  
![helpful_votes.png](https://github.com/pqrt12/BigData/blob/master/helpful_votes.png)
![helpful_votes.png](https://github.com/pqrt12/BigData/blob/master/total_votes.png)  
Overall, the 'vine' reviews are helpful, trustworthy.
