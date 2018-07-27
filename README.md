# Exploratory-Analysis-of-Trump-Texts
Installation of R packages
Packages can be defined as the fundamental unit of sharing code consisting of a bundle of code, data, documentation and tests which are stored in the library. The packages required for text mining of trump.txt are listed in the needed vector and downloaded by using install.packages() and called by library() function.
1. tm- text mining framework in R.
2. SnowballC- function that extracts the stem of each given word in the vector.
3. RColorBrewer – creates color palettes for thematic maps.
4. Ggplot2- creates graphics on the basis of declaring the primitives and the variables to be mapped on the aesthetic.
5. Wordcloud- plots a cloud of words shared across the documents.
6. Biclust- performs biclustering in a data matrix depending on the algorithm (eg- CC, bimax).
7. Cluster- groups data by specified method (eg- hclust, pca).
8. Igraph- performs network analysis and data visualization for large datasets.
9. Fpc- flexible procedure clustering (eg- fixed point clustering, linear regression clustering).
We use vcorpus or a volatile collection of text documents to load the details of the text documents in R by vcorpus() and inspect the loaded texts using inspect() function.

### Pre-processing

To accomplish text mining using numeric data mining algorithms we remove punctuation, stopwords and numbers because they add no value to the analysis. Generally, in pre-processing we use tm_map() function to transform or map our textual data to corpus and then, the function gsub() that helps to replace all matches of the string with the replacement provided and returns the string of same size. 

Here, we use functions tm_map() and gsub() to start with removing punctuations and replace the special characters such as /,@,\\| and \u2028 with white spaces. Then, we proceed with removal of numbers and convert the uppercase letters to lowercase and define the type of document as plain text document. Removing specific words like “english” that are not valuable and stopwords such as and, the, him, her etc. will help us focus better on the main words that are contained in the texts that make a positive or negative impact. Stemming is the process of removal of different variants of the same word for example say, says, run, running etc. and we also combine words that should stay together to make sense for example fake news becomes fake-news for simplicity. The final step of pre-processing is to strip off the extra whitespaces to a single blank space and define the type of our text as a plain text document.

### Data Staging 

We want to get a matrix or a table containing the words after pre-processing the data in the texts with the frequency indicated for each one respectively by using the function DoumentTermMatrix(). The dtm consists of 3659 columns (terms) and 11 rows (text documents) that appeared at least once after pre-processing and 79% of term-document pairs are zeroes. We perform a matrix transpose using TermDocumentMatrix() function on dtm matrix to get a tdm matrix of text data of dimension 3659 by 11  and write it in a csv file called DocumentTermMatrix.csv.

Next we define dtms to remove the sparse terms or low frequency terms by using the RemoveSparseTerms() function and define sparse = 0.2. Since we want terms that appear more than 80% of the time, we defined the sparse = 0.2. We sum the columns of dtms and name the new table as freq to obtain the total frequency of top 20 and lowest 20 terms appearing in all texts by using the head() and tail() functions.

By using the function head() we get lowest 20 frequencies where the first row of the output corresponds to the frequency with which the word appears and second row tells us the number of words corresponding to the frequency. Here, 1638 terms appeared just 1 time and 626 terms appeared 2 times. By using the function tail() we get the top 20 frequencies where the highest used term appeared 428 times in the texts and second highest used term appeared 278 times. The term “will” was used 428 times and “many” was used 101 times in trump’s speeches. We put this freq table in a dataframe wf. 

### Histogram

We load the ggplot2 package using library() function and use ggplot2 to plot a histogram of wf of type “identity” for words vs frequency for terms with frequencies greater than 50 (freq > 50) and at an angle of 45 degrees by angle =45  and 1 unit away from the x axis by specifying hjust= 1 in the theme().

### Wordcloud

A word cloud can be defined as an image which consists of terms in different color and sizes corresponding to their importance or frequency. (i.e Larger words = high frequency of usage)

We load the wordcloud package by using library() function and remove sparse terms to show only words that appeared more than 85% times therefore, sparse=0.15. Then we use the wordcloud() function on freq table and specify maximum words as 100, colors as dark and rotation as 0.2. “Will” and “People” have the largest font because they have the highest frequency according to the histogram plotted.

### Hierarchical Clustering

This is a "bottom up" approach where each observation starts in its own cluster, and pairs of clusters are merged as one moves up the hierarchy. All observations start in one cluster, and splits are performed recursively as one moves down the hierarchy.

Here, we load the cluster package and calculate the Euclidean distances between two nearest points or terms and name it d. Then we use function hclust() and specified the method “euclidean” to display the dendogram with the number of clusters = 6 reflected in the red borders.

### K-means Clustering

This is a popular data mining technique in which the variables are clustered into k groups depending on their mean values. Similar to hierarchial clustering, we calculate the eucliadean distances between terms based on their mean and name it as d. Then we form clusters using kmeans() function and provide the parameters d and clusters = 2. Then, we use clusplot() function to plot or visualize the k-means clusters for better understanding.

The top 3 words “people”, “going” and “will” are grouped in 1 single cluster because of their high frequency and can be termed as first principal component. Other words such as “great”, “country”, “want”, “one” etc are grouped in second cluster because of their comparatively lower frequency and can be termed as second principal component. The graph also states that these two components describe almost 96.18% of the total data. The output of k-means clustering, word cloud, hierachial clustering and histogram go hand in hand.
