# BDAMahaout
BDAMahaout Assignment
Building a Recommender

To demonstrate how to build an analytic job with Mahout on EMR, we’ll build a movie recommender. We will start with ratings given to movie titles by users in the MovieLens data set, which was compiled by the GroupLens team, and will use the “recommenditembased” example to find most-recommended movies for each user.
In the CLI type bellow commands

Get the MovieLens data
wget http://files.grouplens.org/datasets/movielens/ml-1m.zip
unzip ml-1m.zip

Convert ratings.dat, trade “::” for “,”, and take only the first three columns:
cat ml-1m/ratings.dat | sed 's/::/,/g' | cut -f1-3 -d, > ratings.csv
Put ratings file into HDFS:
hadoop fs -put ratings.csv /ratings.csv
Run the recommender job:
mahout recommenditembased --input /ratings.csv --output recommendations --numRecommendations 10 --outputPathForSimilarityMatrix similarity-matrix --similarityClassname SIMILARITY_COSINE
Look for the results in the part-files containing the recommendations:
hadoop fs -ls recommendations
hadoop fs -cat recommendations/part-r-00000 | head



Building a Recommender
Get Twisted, and Klein and Redis modules for Python.
sudo pip3 install twisted
sudo pip3 install klein

sudo pip3 install redis

Install Redis and start up the server.
wget http://download.redis.io/releases/redis-2.8.7.tar.gz tar xzf redis-2.8.7.tar.gz cd redis-2.8.7 make ./src/redis-server &
Build a web service that pulls the recommendations into Redis and responds to queries. Put the above bda.py content into python file.
Start the web service.
twistd -noy your_file_name.py &
Test the web service with user id “37”
curl localhost:8083/37