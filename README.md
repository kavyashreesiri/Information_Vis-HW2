Kavyashree Sirigere Prakash,CS 725,Spring 2018

Link to Homework-2:
* http://www.cs.odu.edu/~psiriger/cs725/CS725-HW2/

__Homework 2-Writeup__


1. __Clean up country names__   
* There were other countries with issues of spelling.Variations of Country names are listed below are:
        * "Netherlands" which was also spelled as "the netherlands"
        * "England" which was also spelled as "England,UK","England,United Kingdom","England,U.K"
        * "Russia" which also spelled as "Rossija","Russain Federation"
        * "China" which also spelled as "Republic of China"
        * "Canada" which was also spelled as "Canada BIP 6L2"
        * "Scotland" which was also spelled as "Scotland,UK","Scotland,United Kingdom","Scotland,U.K"

    In order to discover these variations,I used various __Methods__ and __Keying functions__ with different parameters.
    There are two methods provided by OpenRefine:
   1. __Key Collision__-This method allows us to cluster many alternative values which have same meaning to have the same key
   2. __Nearest neighbor__

  * __Using Key Collision to find variations__:
    This method provides __3 Keying functions__:
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


   * __Using Nearest neighbor__   
     * This method allots a cluster to any pair of strings that are closer than a certain threshold value  
     * There are two methods provided calculate distance between a pair of strings.
       * They are:
         * Levenshtein Distance- calculates least number of edit operations that are reqiuired to change one string to another
         * PPM-Uses Kolmogrov complexity to estimate 'Similarity' between strings.
    
Below is the Summary of results obtained from Nearset Neighbour method:

| Method        | Distance Function |Radius|Block Chars|Cluster size|Row count| Values in cluster                            | New cell value   |
| :-----------: | :-------------:   |:----:|:--------: |:--------:  |:-------:|--------------------------------| :------------:   |
|Nearest neighbor|Levenshtein|4| |2 |3722|	England(3398 rows),England, UK(324 rows)|England|
|Nearest neighbor|Levenshtein|4| |2  |3124|Scotland(3060 rows),Scotland, UK(64 rows)|Scotland|
|Nearest neighbor|PPM|7.5| |2  |577|Canada B1P 6L2(576 rows),Canada C1A 4P3 Telephone: 902-566-0439 Fax: 902-566-0795(1 rows)|Canada|
|Nearest neighbor|PPM|7.5| |2  |5|Russia(3 rows),Russian Federation(2 rows)|Russia|
|Nearest neighbor|PPM|7.5| |2  |4294|England(3722 rows),England, United Kingdom(572 rows),England|England|
|Nearest neighbor|PPM|7.5| |2  |3140|Scotland(3124 rows)|Scotland, United Kingdom(16 rows)|Scotland|
|Nearest neighbor|PPM|8.0|5 |2  |6|China(4 rows),Republic of China(2 rows)|China|


2. __Clean up values for the endowment__      

 * There were `1111` number of entries that used million or Million
 * There were `19501` number of entries that used billion or Billion

3. __Finding issues in other columns__   










4. __Exploring the data with scatter plots__     

    Yes,there is correlation.As the endowment donation amount incresases for a specific university,Number of students also increase. It shows __positive correlation__.  
    Scatterplot that obtained is: [endowment(x) vs. numStudents(y) 
* http://www.cs.odu.edu/~psiriger/cs725/CS725-HW2/Endowment_vs_numStudents_plot.png

5. __Geocoding names and addresses__   

* I selected 7 rows from numeric log facet applied on numStudents column.
* I obtained 51096 rows from original dataset which had 75043 rows after performing geocoding.

6. __27 Club__
    * I found out that __90 musicians were dead at the age of 27__.  
    Process followed:  
    * Created project "Musicians" in OpenRefine by uploading the dataset.    
    * Created a new column named birthdate that uses the first value it encounters when scanning from birthdate1 to birthdate2 to birthdate3 in each row.  
    * I used the below transform :   
           `forNonBlank(cells.birthdate1.value, v1, v1, forNonBlank(cells.birthdate2.value, v2, v2, forNonBlank(cells.birthdate3.value, v3, v3, null)))`
    * To apply transform,select one of the birthdate column and click on Edit cells,then choose Transform.    
    * 






