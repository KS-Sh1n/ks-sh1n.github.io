---
layout: post
title:  "Data Cleaning"
description: "Master efficient workflows for cleaning real-world, messy data."
categories: learning
read_minutes: 10
is_project_page: false
show_downloads: false
linux_compatible: false
---

# **Table of Contents**

1. Handling Missing Values
2. Scaling and Normalization
3. Parsing Dates
4. Character Encodings
5. Inconsistent Data Entry

* * *

### 문단 복사 붙여넣기용
<p>　</p>

**Forecasting**: most common application of machine learning in the real world.

After finishing this course, you'll know how to:

  - engineer features to model the major time series components (trends, seasons, and cycles),
  - visualize time series with many kinds of time series plots,
  - create forecasting *hybrids* that combine the strengths of complementary models, and
  - adapt machine learning methods to a variety of forecasting tasks.

## **1. Handling Missing Values**

> ### **Take a first look at the data**
```python
# look at the first five rows of the nfl_data file. 
# I can see a handful of missing data already!
nfl_data.head()
```
> ### **How many missing data points do we have?**
```python
# get the number of missing data points per column
missing_values_count = nfl_data.isnull().sum()

# look at the # of missing points in the first ten columns
missing_values_count[0:10]

# how many total missing values do we have?
total_cells = np.product(nfl_data.shape)
total_missing = missing_values_count.sum()

# percent of data that is missing
percent_missing = (total_missing/total_cells) * 100
print(percent_missing)
```

**data intution**: really looking at your data and trying to figure out why it is the way it is and how that will affect your analysis

intution is needed to figure out why the value is missing: 
> **Is this value missing because it wasn't recorded or because it doesn't exist?**

if doesn't exist, probably want to keep as `NaN`
if not recorded, should guess what it might have been based on the other values in that column and row. = **imputation**

> **Tip:** This is a great place to read over the dataset documentation if you haven't already! If you're working with a dataset that you've gotten from another person, you can also try reaching out to them to get more information.

"quick and dirty" techniques that can help you with missing values but will probably also end up removing some useful information or adding some noise to your data.

> ### **Drop Missing Values**

```python
# Delete all rows with at least one missing value.
nfl_data.dropna()
# Delete all columns with at least one missing value.
nfl_data.dropna(axis=1)
```
don't generally recommend for important projects.
It's usually worth it to take the time to go through your data and really look at all the columns with missing values one-by-one to really get to know your dataset.

> ### **Fill Missing Values**

Retrieve small sub-section of the NFL data so that it will print well.

```python
# replace all NA's with 0
subset_nfl_data.fillna(0)

# replace all NA's the value that comes directly after it in the same column,
# then replace all the remaining na's with 0
subset_nfl_data.fillna(method='bfill', axis=0).fillna(0)
```

# More practice

If you're looking for more practice handling missing values:

* Check out [this noteboook](https://www.kaggle.com/alexisbcook/missing-values) on handling missing values using scikit-learn's imputer. 
* Look back at the "Zipcode" column in the `sf_permits` dataset, which has some missing values. How would you go about figuring out what the actual zipcode of each address should be? (You might try using another dataset. You can search for datasets about San Fransisco on the [Datasets listing](https://www.kaggle.com/datasets).) 

* * *

## **2. Scaling and Normalization**
> ### **Transform numeric variables to have helpful properties.**

  - **scaling**: changing the range of your data, while
  - **normalization**: changing the shape of the distribution of your data.

**Scaling**
transforming your data so that it fits within a specific scale, like 0-100 or 0-1.
useful for methods based on measures of how far apart data points are, like SVM or K-NN.
a change of "1" in any numeric feature is given the same importance.

```python
# generate 1000 data points randomly drawn from an exponential distribution
original_data = np.random.exponential(size=1000)

# mix-max scale the data between 0 and 1
scaled_data = minmax_scaling(original_data, columns=[0])

#shape of the data doesn't change, but that instead of ranging from 0 to 8ish, it now ranges from 0 to 1.
```
**Normalization**
normalize your data if you're going to be using a machine learning or statistics technique that assumes your data is normally distributed.
ex) Linear Discriminant Analysis (LDA) and Gaussian naive Bayes.

```python
# normalize the exponential data with boxcox
normalized_data = stats.boxcox(original_data)
```

# (Optional) More practice

Try finding a new dataset and pretend you're preparing to perform a [regression analysis](https://www.kaggle.com/rtatman/the-5-day-regression-challenge). 

[These datasets are a good start!](https://www.kaggle.com/rtatman/datasets-for-regression-analysis)

Pick three or four variables and decide if you need to normalize or scale any of them and, if you think you should, practice applying the correct technique.

* * *

## **3. Parsing Dates**
> ### **Why do I come up with this project?**

> Pandas uses the "object" dtype for storing various types of data types, but most often when you see a column with the dtype "object" it will have strings in it.

If you check the pandas dtype documentation, you'll notice that there's also a specific `datetime64` dtypes.

```python
# check the data type of our date column
landslides['date'].dtype
```

[**strftime**](strftime.org)
There are lots of possible parts of a date, but the most common are %d for day, %m for month, %y for a two-digit year and %Y for a four digit year.

```python
# create a new column, date_parsed, with the parsed dates
landslides['date_parsed'] = pd.to_datetime(landslides['date'], format="%m/%d/%y")
```

### Possible error with multiple date formats?
Sometimes you'll run into an error when there are multiple date formats in a single column. If that happens, you can have pandas try to infer what the right date format should be.
```python
landslides['date_parsed'] = pd.to_datetime(landslides['Date'], infer_datetime_format=True)
```
There are two big reasons not to always have pandas guess the time format.
1. pandas won't always been able to figure out the correct date format, especially if someone has gotten creative with data entry. 2. much slower than specifying the exact format of the dates.

```python
# Now that we have a column of parsed dates, we can extract information like the day of the month that a landslide occurred.

# get the day of the month from the date_parsed column
day_of_month_landslides = landslides['date_parsed'].dt.day
day_of_month_landslides.head()
```
```python
# Length = 24인 string 검색 후 출력
date_lengths = earthquakes.Date.str.len()
date_lengths.value_counts()
indices = np.where([date_lengths == 24])[1]
print('Indices with corrupted data:', indices)
earthquakes.loc[indices]
```

# (Optional) More practice

If you're interested in graphing time series, [check out this tutorial](https://www.kaggle.com/residentmario/time-series-plotting-optional).

You can also look into passing columns that you know have dates in them  the `parse_dates` argument in `read_csv`. (The documention [is here](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html).) Do note that this method can be very slow, but depending on your needs it may sometimes be handy to use.


* * *

## **4. Character Encodings**
> ### **Avoid UnicoodeDecodeErrors when loading CSV files.**

**Character encodings**: specific sets of rules for mapping from raw binary byte strings (0110100001101001) to characters that make up human-readable text ("hi").

**UTF-8** is the standard text encoding. All Python code is in UTF-8 and, ideally, all your data should be as well.
> It's when things aren't in UTF-8 that you run into trouble.

```python
# start with a string
before = "This is the euro symbol: €"

# encode it to a different encoding, replacing characters that raise errors
after = before.encode("utf-8", errors="replace")

# check the type
type(after)
> bytes

# take a look at what the bytes look like
after
> b'This is the euro symbol: \xe2\x82\xac'

# convert it back to utf-8
print(after.decode("utf-8"))
```
"\xe2\x82\xac": euro symbol as if it were an ASCII string.

However, when we try to use a different encoding to map our bytes into a string, we get an error. This is because the encoding we're trying to use doesn't know what to do with the bytes we're trying to pass it. You need to tell Python the encoding that the byte string is actually supposed to be in.

```python
# try to decode our bytes with the ascii encoding
print(after.decode("ascii"))

#> UnicodeDecodeError 
```

> You can think of different encodings as different ways of recording music. You can record the same music on a CD, cassette tape or 8-track. While the music may sound more-or-less the same, you need to use the right equipment to play the music from each recording format. The correct decoder is like a cassette player or a CD player. If you try to play a cassette in a CD player, it just won't work.

We can also run into trouble if we try to use the wrong encoding to map from a string to bytes. Like I said earlier, strings are UTF-8 by default in Python 3, so if we try to treat them like they were in another encoding we'll create problems.

For example, if we try to convert a string to bytes for ASCII using encode(), we can ask for the bytes to be what they would be if the text was in ASCII. Since our text isn't in ASCII, though, there will be some characters it can't handle.
We can automatically replace the characters that ASCII can't handle. If we do that, however, any characters not in ASCII will just be replaced with the unknown character. Then, when we convert the bytes back to a string, the character will be replaced with the unknown character.
The dangerous part about this is that there's not way to tell which character it should have been. That means we may have just made our data unusable!

It's far better to convert all our text to UTF-8 as soon as we can and keep it in that encoding. The best time to convert non UTF-8 input into UTF-8 is when you read in files, which we'll talk about next.

Problem: Some file isn't actually UTF-8. And we don't know **what encoding it actually is** though.

 A way is to use the chardet module to try and automatically guess what the right encoding is. It's not 100% guaranteed to be right, but it's usually faster than just trying to guess.

```python
# look at the first ten thousand bytes to guess the character encoding
with open("../input/kickstarter-projects/ks-projects-201801.csv", 'rb') as rawdata:
    result = chardet.detect(rawdata.read(10000))

# check what the character encoding might be
print(result)

#> {'encoding': 'Windows-1252', 'confidence': 0.73, 'language': ''}
```
chardet is 73% confidence that the right encoding is "Windows-1252".

> **What if the encoding chardet guesses isn't right?** Since chardet is basically just a fancy guesser, sometimes it will guess the wrong encoding. One thing you can try is looking at more or less of the file and seeing if you get a different result and then try that.

```python
# save our file (will be saved as UTF-8 by default!)
kickstarter_2016.to_csv("ks-projects-201801-utf8.csv")
```

### (Optional) More practice

Check out [this dataset of files in different character encodings](https://www.kaggle.com/rtatman/character-encoding-examples). Can you read in all the files with their original encodings and them save them out as UTF-8 files?

If you have a file that's in UTF-8 but has just a couple of weird-looking characters in it, you can try out the [ftfy module](https://ftfy.readthedocs.io/en/latest/#) and see if it helps. 

# Keep going

In the final lesson, learn how to [**clean up inconsistent text entries**](https://www.kaggle.com/alexisbcook/inconsistent-data-entry) in your dataset.

* * *

## **5. Inconsistent Data Entry**
> ### **Efficiently fix typos in your data.**

```python
# get all the unique values in the 'Country' column
countries = professors['Country'].unique()

# sort them alphabetically and then take a closer look
countries.sort()
countries

# make everything lower case
professors['Country'] = professors['Country'].str.lower()

# remove trailing white spaces
professors['Country'] = professors['Country'].str.strip()

# you can fix a good 80% of your text data entry inconsistencies by doing this.
```
**fuzzywuzzy** package: help identify which strings are closest to each other.  Fuzzywuzzy returns a ratio given two strings. The closer the ratio is to 100, the smaller the edit distance between the two strings. Here, we're going to get the ten strings from our list of cities that have the closest distance to "d.i khan".

> **Fuzzy matching**: The process of automatically finding text strings that are very similar to the target string. In general, a string is considered "closer" to another one the fewer characters you'd need to change if you were transforming one string into another. So "apple" and "snapple" are two changes away from each other (add "s" and "n") while "in" and "on" and one change away (rplace "i" with "o"). You won't always be able to rely on fuzzy matching 100%, but it will usually end up saving you at least a little time.

```python
# get the top 10 closest matches to "south korea"
matches = fuzzywuzzy.process.extract("south korea", countries, limit=10, scorer=fuzzywuzzy.fuzz.token_sort_ratio)

# take a look at them
matches
```

It's a good idea to write a general purpose function you can reuse if you think you might have to do a specific task more than once or twice. This keeps you from having to copy and paste code too often, which saves time and can help prevent mistakes.
```python
# function to replace rows in the provided column of the provided dataframe
# that match the provided string above the provided ratio with the provided string
def replace_matches_in_column(df, column, string_to_match, min_ratio = 47):
    # get a list of unique strings
    strings = df[column].unique()
    
    # get the top 10 closest matches to our input string
    matches = fuzzywuzzy.process.extract(string_to_match, strings, 
                                         limit=10, scorer=fuzzywuzzy.fuzz.token_sort_ratio)

    # only get matches with a ratio > 90
    close_matches = [matches[0] for matches in matches if matches[1] >= min_ratio]

    # get the rows of all the close matches in our dataframe
    rows_with_matches = df[column].isin(close_matches)

    # replace all rows with close matches with the input matches 
    df.loc[rows_with_matches, column] = string_to_match
    
    # let us know the function's done
    print("All done!")
```


* * *