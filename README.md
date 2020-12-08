
This morning we will practice **for loops**.  For loops are a fundamental skill all programmers need to master.  They allow us to move cycle through each item of an iterable.  

An iterable is:

> An object capable of returning its members one at a time. Examples of iterables include all sequence types (such as list, str, and tuple) and some non-sequence types like dict...

> Iterables can be used in a for loop and in many other places where a sequence is needed (zip(), map(), …).

[source](https://docs.python.org/3/glossary.html)

For this exercise, you will import a dataset about air quality in Brooklyn.  The data was gathered using the [Open Air Quality API](https://openaq.org/#/?_k=7pqqwf).  

The data is stored in two lists each filled with 10000 items. 

  - `measurements` holds daily measures of pm25 (particulate matter) readings in µg/m3.  
  - `dates` holds the corresponding timestamps of when a measurement was taken.
  


```python
# Run this cell with no changes
import pickle
import numpy as np
import pandas as pd

with open('data/brooklyn.p','rb') as read_file:
    dates, measurements = pickle.load(read_file)
```

The indices align.  In other words, `dates[0]` holds the timestamp for `measurements[0]`.


```python
len(dates) == len(measurements)
```

The short-term standard (24-hour or daily average) is 35 micrograms per cubic meter of air (µg/m3) 
[source](https://www.health.ny.gov/environmental/indoors/air/pmq_a.htm)

# Task 1

> Using a `for loop`, count how often Brooklyn air quality is above the safe level.



```python
# your code here
```

# Task 2

> Using a for loop, find the maximum measurement of pm25 in the dataset.



```python
# Your answer here
max_pm25 = None
```


```python
# Run this cell. 
assert(max_pm25==max(measurements))

# If you assigned the incorrect value to the max_pm variable, you will receive an error message
print('Correct')
```

# Task 3

> Using a for loop, find the minimum measurement of pm25



```python
# your code here

min_pm25 = None
```


```python
# Check here
assert(min_pm25 == min(measurements))
print('Correct')
```

# Task 4

Each date in the dates list is a Timestamp object.


```python
type(dates[0])
```

For each date, we can find the day of the week by calling the method day_name like so:

`date.day_name()`

With a for loop, create a list of the names of the days of the week for every entry.


```python
# Your code here
day_of_week = None

```


```python
assert(day_of_week[0] == 'Thursday')
print('Correct')
```

# Task 5

The `zip` built-in function allows us to iterate through two lists at the same time. 


```python
zip?
```

Using a for loop and zip, create a dictionary using a for loop whose key is the date and value is the pm25 measurement.



```python
# Your code here
date_measurement = None


```


```python
assert(date_measurement[list(date_measurement.keys())[0]] == 1.6)
print('Correct')
```

# Task 6
Find the average reading on each day of the week using whatever technique you care to choose.


```python
# Your code here
```


```python

```

# Bonus
Unlike lists and tuples, dictionaries are not ordered.  However, there are ways to sort dictionaries. Google how to sort a dictionary, and find the dates of the top 5 worst air-quality readings in Brooklyn.


```python
# Your code here
airquality_sorted = None
```


```python
assert(list(airquality_sorted.values())) == [55.4, 54.7, 53.3, 47.5, 44]
print('Correct')
```


```python

```
