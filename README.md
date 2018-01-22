Kavyashree Sirigere Prakash,CS 725,Spring 2018

Link to Homework-2:
* http://www.cs.odu.edu/~psiriger/cs725/CS725-HW2/

** H3 Homework 2-Writeup**

** Tutorial **
1.Clean up country names
------------------------
Therer were other countries with issues of spelling.Variations of Country names are listed below are:
* "Netherlands" which was also spelled as "the netherlands"
* "England" which was also spelled as "England,UK","England,United Kingdom","England,U.K"
* "Russia" which also spelled as "Rossija","Russain Federation"
* "China" which also spelled as "Republic of China"
* "Canada" which was also spelled as "Canada BIP 6L2"
* "Scotland" which was also spelled as "Scotland,UK","Scotland,United Kingdom","Scotland,U.K"

In order to discover these variations,I used various **Methods** and **Keying functions** with different parameters.
There are two methods provided by OpenRefine:
1. Key Collision-This method allows us to cluster many alternative values which have same meaning to have the same key
2. Nearest neighbor

1. Using Key Collision to find variations:
    This method provides **3 Keying functions**:
    * __Fingerprint__
        * This method follows the process that produces a key from string value of variety of contexts
        * But,this method did not give any results for this dataset.            
    * __N-gram fingerprint__
        * Here, n-grams(number of characters in the string) is specified to cluster the tokens
        * `Results` : For 1-gram fingerprint of "Netherlands" is "the Netherlands" (n-gram=1)
    * __Phonetic Fingerprint__
        * This method converts tokens into the way they are pronounced
        * It  is very helpful to find variations of country names as poeple spell names differently.
        * But,the both original name of country and converted token will have same key shared among them which results in alloting the cluster to bth.
        * __Cologne-phonetic__
            * This method encodes a string into a Cologne Phonetic value(in German language).  
            * `Results` :In two rows,Russia was pronounced as "Rossija"
        * __Metaphone3__
            * It encodes a string into the specific English phonetic 
            * `Results` :United States was spelled as "United States of America"
            
__Summary of the above operations:__

| Method        | Keying Function               |Cluster size   |Row count   | Values in cluster                            | New cell value   |
| :-----------: | :-------------------------:   |:----------:   | :--------: |----------------------------------------------| :------------:   |
|Key collision  | Ngram-fingerprint,n-gram=1    | 2             | 4          | Netherlands(2 rows),	the Netherlands(2 rows) | Netherlands      |
|Key collision  | Cologne-phonetic              | 2             | 3          | Rossija(2 rows),Russia(1 rows)               | Russia           |
|Key collision  | Metaphone3                    | 2             | 46046      | United States(45431 rows),United States of America(615 rows)|United States|


2. Using Nearest neighbor
    







