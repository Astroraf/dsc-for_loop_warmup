
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




    True



The short-term standard (24-hour or daily average) is 35 micrograms per cubic meter of air (µg/m3) 
[source](https://www.health.ny.gov/environmental/indoors/air/pmq_a.htm)

# Task 1

> Using a `for loop`, count how often Brooklyn air quality is above the safe level.



```python
# your code here
```


```python
#__SOLUTION__
# Using a for loop, count how often the Brooklyn Air Quality is above the safe level

count = 0
for measurement in measurements:
    if measurement >= 35:
        count += 1
        
count
```




    12



# Task 2

> Using a for loop, find the maximum measurement of pm25 in the dataset.



```python
# Your answer here
max_pm = None
```


```python
#__SOLUTION__

max_pm25 = 0

for measurement in measurements:
    if measurement > max_pm25:
        max_pm25 = measurement


```


```python
# Run this cell. 
assert(max_pm25==max(measurements))

# If you assigned the incorrect value to the max_pm variable, you will receive an error message
print('Correct')
```

    Correct


# Task 3

> Using a for loop, find the minimum measurement of pm25



```python
# your code here

min_pm25 = None
```


```python
#__SOLUTION__
# Find the minimum reading of pm25
min_pm25 = max_pm25

for measurement in measurements:
    if measurement < min_pm25:
        min_pm25 = measurement


```


```python
# Check here
assert(min_pm25 == min(measurements))
print('Correct')
```

    Correct


# Task 4

Each date in the dates list is a Timestamp object.


```python
type(dates[0])
```




    pandas._libs.tslibs.timestamps.Timestamp



For each date, we can find the day of the week by calling the method day_name like so:

`date.day_name()`

With a for loop, create a list of the names of the days of the week for every entry.


```python
# Your code here
day_of_week = None

```


```python
#__SOLUTION__
day_of_week = []

for date in dates:
    day_of_week.append(date.day_name())

```


```python
assert(day_of_week[0] == 'Thursday')
print('Correct')
```

    Correct


# Task 5

The `zip` built-in function allows us to iterate through two lists at the same time. 


```python
zip?
```


    [0;31mInit signature:[0m [0mzip[0m[0;34m([0m[0mself[0m[0;34m,[0m [0;34m/[0m[0;34m,[0m [0;34m*[0m[0margs[0m[0;34m,[0m [0;34m**[0m[0mkwargs[0m[0;34m)[0m[0;34m[0m[0;34m[0m[0m
    [0;31mDocstring:[0m     
    zip(*iterables) --> A zip object yielding tuples until an input is exhausted.
    
       >>> list(zip('abcdefg', range(3), range(4)))
       [('a', 0, 0), ('b', 1, 1), ('c', 2, 2)]
    
    The zip object yields n-length tuples, where n is the number of iterables
    passed as positional arguments to zip().  The i-th element in every tuple
    comes from the i-th iterable argument to zip().  This continues until the
    shortest argument is exhausted.
    [0;31mType:[0m           type
    [0;31mSubclasses:[0m     



Using a for loop and zip, create a dictionary using a for loop whose key is the date and value is the pm25 measurement.



```python
# Your code here
date_measurement = None


```


```python
#__SOLUTION__

date_measurement = {}

for date, pm25 in zip(dates, measurements):
    date_measurement[date] = pm25

date_measurement
```




    {Timestamp('2019-06-27 21:00:00+0000', tz='UTC'): 1.6,
     Timestamp('2019-06-27 22:00:00+0000', tz='UTC'): 0.7,
     Timestamp('2019-06-27 23:00:00+0000', tz='UTC'): 1.6,
     Timestamp('2019-06-28 00:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-06-28 01:00:00+0000', tz='UTC'): 4.2,
     Timestamp('2019-06-28 02:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-06-28 03:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-06-28 04:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-06-28 05:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-06-28 06:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-06-28 07:00:00+0000', tz='UTC'): 5.9,
     Timestamp('2019-06-28 08:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-06-28 09:00:00+0000', tz='UTC'): 6.4,
     Timestamp('2019-06-28 10:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-06-28 11:00:00+0000', tz='UTC'): 3.6,
     Timestamp('2019-06-28 12:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-06-28 13:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-06-28 14:00:00+0000', tz='UTC'): 6.1,
     Timestamp('2019-06-28 15:00:00+0000', tz='UTC'): 7.4,
     Timestamp('2019-06-28 16:00:00+0000', tz='UTC'): 8,
     Timestamp('2019-06-28 17:00:00+0000', tz='UTC'): 6.9,
     Timestamp('2019-06-28 18:00:00+0000', tz='UTC'): 7.6,
     Timestamp('2019-06-28 19:00:00+0000', tz='UTC'): 10.8,
     Timestamp('2019-06-28 20:00:00+0000', tz='UTC'): 5.3,
     Timestamp('2019-06-28 21:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-06-28 22:00:00+0000', tz='UTC'): 2.9,
     Timestamp('2019-06-28 23:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-06-29 00:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-06-29 01:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-06-29 02:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-06-29 03:00:00+0000', tz='UTC'): 7.4,
     Timestamp('2019-06-29 04:00:00+0000', tz='UTC'): 10,
     Timestamp('2019-06-29 05:00:00+0000', tz='UTC'): 11,
     Timestamp('2019-06-29 06:00:00+0000', tz='UTC'): 10.5,
     Timestamp('2019-06-29 07:00:00+0000', tz='UTC'): 13.7,
     Timestamp('2019-06-29 08:00:00+0000', tz='UTC'): 16.4,
     Timestamp('2019-06-29 09:00:00+0000', tz='UTC'): 16.6,
     Timestamp('2019-06-29 10:00:00+0000', tz='UTC'): 16.4,
     Timestamp('2019-06-29 11:00:00+0000', tz='UTC'): 17.2,
     Timestamp('2019-06-29 12:00:00+0000', tz='UTC'): 16.2,
     Timestamp('2019-06-29 13:00:00+0000', tz='UTC'): 13.6,
     Timestamp('2019-06-29 14:00:00+0000', tz='UTC'): 12.6,
     Timestamp('2019-06-29 15:00:00+0000', tz='UTC'): 7.8,
     Timestamp('2019-06-29 16:00:00+0000', tz='UTC'): 4.1,
     Timestamp('2019-06-29 17:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-06-29 18:00:00+0000', tz='UTC'): 8.9,
     Timestamp('2019-06-29 19:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-06-29 20:00:00+0000', tz='UTC'): 8.9,
     Timestamp('2019-06-29 21:00:00+0000', tz='UTC'): 13.5,
     Timestamp('2019-06-29 22:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-06-29 23:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-06-30 00:00:00+0000', tz='UTC'): 4.6,
     Timestamp('2019-06-30 01:00:00+0000', tz='UTC'): 2.7,
     Timestamp('2019-06-30 02:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-06-30 03:00:00+0000', tz='UTC'): 2.8,
     Timestamp('2019-06-30 04:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-06-30 05:00:00+0000', tz='UTC'): 4.1,
     Timestamp('2019-06-30 06:00:00+0000', tz='UTC'): 3.7,
     Timestamp('2019-06-30 07:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-06-30 08:00:00+0000', tz='UTC'): 3.1,
     Timestamp('2019-06-30 09:00:00+0000', tz='UTC'): 3.7,
     Timestamp('2019-06-30 10:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-06-30 11:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-06-30 12:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-06-30 13:00:00+0000', tz='UTC'): -0.3,
     Timestamp('2019-06-30 14:00:00+0000', tz='UTC'): 1.4,
     Timestamp('2019-06-30 15:00:00+0000', tz='UTC'): 1.2,
     Timestamp('2019-06-30 16:00:00+0000', tz='UTC'): 4.6,
     Timestamp('2019-06-30 17:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-06-30 18:00:00+0000', tz='UTC'): 3.1,
     Timestamp('2019-06-30 19:00:00+0000', tz='UTC'): 7.8,
     Timestamp('2019-06-30 20:00:00+0000', tz='UTC'): -1.9,
     Timestamp('2019-06-30 21:00:00+0000', tz='UTC'): 0,
     Timestamp('2019-06-30 22:00:00+0000', tz='UTC'): 1.1,
     Timestamp('2019-06-30 23:00:00+0000', tz='UTC'): 1.8,
     Timestamp('2019-07-01 00:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-07-01 01:00:00+0000', tz='UTC'): 0.9,
     Timestamp('2019-07-01 02:00:00+0000', tz='UTC'): -0.4,
     Timestamp('2019-07-01 03:00:00+0000', tz='UTC'): -0.8,
     Timestamp('2019-07-01 04:00:00+0000', tz='UTC'): -1.5,
     Timestamp('2019-07-01 05:00:00+0000', tz='UTC'): -1.1,
     Timestamp('2019-07-01 06:00:00+0000', tz='UTC'): -0.8,
     Timestamp('2019-07-01 07:00:00+0000', tz='UTC'): -0.7,
     Timestamp('2019-07-01 08:00:00+0000', tz='UTC'): -0.5,
     Timestamp('2019-07-01 09:00:00+0000', tz='UTC'): -0.4,
     Timestamp('2019-07-01 10:00:00+0000', tz='UTC'): 0.3,
     Timestamp('2019-07-01 11:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-07-01 12:00:00+0000', tz='UTC'): 2.1,
     Timestamp('2019-07-01 13:00:00+0000', tz='UTC'): 2.1,
     Timestamp('2019-07-01 14:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-01 15:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-01 16:00:00+0000', tz='UTC'): 1.8,
     Timestamp('2019-07-01 17:00:00+0000', tz='UTC'): 3.2,
     Timestamp('2019-07-01 18:00:00+0000', tz='UTC'): 3.2,
     Timestamp('2019-07-01 19:00:00+0000', tz='UTC'): 3.6,
     Timestamp('2019-07-01 20:00:00+0000', tz='UTC'): 2.1,
     Timestamp('2019-07-01 21:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-01 22:00:00+0000', tz='UTC'): 1,
     Timestamp('2019-07-01 23:00:00+0000', tz='UTC'): 2.7,
     Timestamp('2019-07-02 00:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-07-02 01:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-07-02 02:00:00+0000', tz='UTC'): 3.6,
     Timestamp('2019-07-02 05:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-07-02 06:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-02 10:00:00+0000', tz='UTC'): 3,
     Timestamp('2019-07-02 11:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-07-02 14:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-02 16:00:00+0000', tz='UTC'): 4.2,
     Timestamp('2019-07-02 17:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-02 22:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-02 23:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-07-03 00:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-07-03 01:00:00+0000', tz='UTC'): 10.3,
     Timestamp('2019-07-03 02:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-07-03 03:00:00+0000', tz='UTC'): 11.1,
     Timestamp('2019-07-03 04:00:00+0000', tz='UTC'): 8.1,
     Timestamp('2019-07-03 05:00:00+0000', tz='UTC'): 7.6,
     Timestamp('2019-07-03 06:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-07-03 07:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-07-03 08:00:00+0000', tz='UTC'): 6.3,
     Timestamp('2019-07-03 09:00:00+0000', tz='UTC'): 8.5,
     Timestamp('2019-07-03 10:00:00+0000', tz='UTC'): 13.1,
     Timestamp('2019-07-03 11:00:00+0000', tz='UTC'): 10.7,
     Timestamp('2019-07-03 12:00:00+0000', tz='UTC'): 10.9,
     Timestamp('2019-07-03 13:00:00+0000', tz='UTC'): 13,
     Timestamp('2019-07-03 14:00:00+0000', tz='UTC'): 13.9,
     Timestamp('2019-07-03 15:00:00+0000', tz='UTC'): 13.3,
     Timestamp('2019-07-03 16:00:00+0000', tz='UTC'): 13.8,
     Timestamp('2019-07-03 17:00:00+0000', tz='UTC'): 12.8,
     Timestamp('2019-07-03 18:00:00+0000', tz='UTC'): 11.8,
     Timestamp('2019-07-03 19:00:00+0000', tz='UTC'): 14.2,
     Timestamp('2019-07-03 20:00:00+0000', tz='UTC'): 16,
     Timestamp('2019-07-03 21:00:00+0000', tz='UTC'): 16,
     Timestamp('2019-07-03 22:00:00+0000', tz='UTC'): 13.7,
     Timestamp('2019-07-03 23:00:00+0000', tz='UTC'): 15.5,
     Timestamp('2019-07-04 00:00:00+0000', tz='UTC'): 18.6,
     Timestamp('2019-07-04 01:00:00+0000', tz='UTC'): 19.8,
     Timestamp('2019-07-04 02:00:00+0000', tz='UTC'): 18.3,
     Timestamp('2019-07-04 03:00:00+0000', tz='UTC'): 22.3,
     Timestamp('2019-07-04 04:00:00+0000', tz='UTC'): 29.3,
     Timestamp('2019-07-04 05:00:00+0000', tz='UTC'): 30,
     Timestamp('2019-07-04 06:00:00+0000', tz='UTC'): 36.1,
     Timestamp('2019-07-04 07:00:00+0000', tz='UTC'): 34.6,
     Timestamp('2019-07-04 08:00:00+0000', tz='UTC'): 25.2,
     Timestamp('2019-07-04 09:00:00+0000', tz='UTC'): 18.2,
     Timestamp('2019-07-04 10:00:00+0000', tz='UTC'): 20.7,
     Timestamp('2019-07-04 11:00:00+0000', tz='UTC'): 15,
     Timestamp('2019-07-04 12:00:00+0000', tz='UTC'): 9.7,
     Timestamp('2019-07-04 13:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-07-04 14:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-07-04 15:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-04 16:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-07-04 17:00:00+0000', tz='UTC'): 2.7,
     Timestamp('2019-07-04 18:00:00+0000', tz='UTC'): -0.1,
     Timestamp('2019-07-04 19:00:00+0000', tz='UTC'): 1,
     Timestamp('2019-07-04 20:00:00+0000', tz='UTC'): 12.1,
     Timestamp('2019-07-04 21:00:00+0000', tz='UTC'): 14.1,
     Timestamp('2019-07-04 22:00:00+0000', tz='UTC'): 19.1,
     Timestamp('2019-07-04 23:00:00+0000', tz='UTC'): 18,
     Timestamp('2019-07-05 00:00:00+0000', tz='UTC'): 28.4,
     Timestamp('2019-07-05 01:00:00+0000', tz='UTC'): 47.5,
     Timestamp('2019-07-05 02:00:00+0000', tz='UTC'): 54.7,
     Timestamp('2019-07-05 03:00:00+0000', tz='UTC'): 40.8,
     Timestamp('2019-07-05 05:00:00+0000', tz='UTC'): 12.6,
     Timestamp('2019-07-05 06:00:00+0000', tz='UTC'): 8.1,
     Timestamp('2019-07-05 07:00:00+0000', tz='UTC'): 8.8,
     Timestamp('2019-07-05 08:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-07-05 09:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-05 10:00:00+0000', tz='UTC'): 6.7,
     Timestamp('2019-07-05 11:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-07-05 12:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-07-05 13:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-07-05 14:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-05 15:00:00+0000', tz='UTC'): 5.4,
     Timestamp('2019-07-05 16:00:00+0000', tz='UTC'): 5.9,
     Timestamp('2019-07-05 17:00:00+0000', tz='UTC'): 7.6,
     Timestamp('2019-07-05 18:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-07-05 20:00:00+0000', tz='UTC'): -3.7,
     Timestamp('2019-07-05 22:00:00+0000', tz='UTC'): -2.7,
     Timestamp('2019-07-06 03:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-06 05:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-07-06 10:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-06 11:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-07-06 12:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-07-06 17:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-06 18:00:00+0000', tz='UTC'): 5.3,
     Timestamp('2019-07-06 19:00:00+0000', tz='UTC'): 0.6,
     Timestamp('2019-07-06 20:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-07-06 21:00:00+0000', tz='UTC'): -1.7,
     Timestamp('2019-07-06 22:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-06 23:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-07-07 00:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-07-07 01:00:00+0000', tz='UTC'): -0.2,
     Timestamp('2019-07-07 02:00:00+0000', tz='UTC'): 1.9,
     Timestamp('2019-07-07 03:00:00+0000', tz='UTC'): 2.2,
     Timestamp('2019-07-07 04:00:00+0000', tz='UTC'): 2.2,
     Timestamp('2019-07-07 05:00:00+0000', tz='UTC'): 3.5,
     Timestamp('2019-07-07 07:00:00+0000', tz='UTC'): 0.3,
     Timestamp('2019-07-07 08:00:00+0000', tz='UTC'): 1.2,
     Timestamp('2019-07-07 09:00:00+0000', tz='UTC'): 2,
     Timestamp('2019-07-07 10:00:00+0000', tz='UTC'): 2.2,
     Timestamp('2019-07-07 11:00:00+0000', tz='UTC'): 3.7,
     Timestamp('2019-07-07 12:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-07-07 13:00:00+0000', tz='UTC'): 6.4,
     Timestamp('2019-07-07 14:00:00+0000', tz='UTC'): 8.2,
     Timestamp('2019-07-07 15:00:00+0000', tz='UTC'): 10,
     Timestamp('2019-07-07 16:00:00+0000', tz='UTC'): 11.5,
     Timestamp('2019-07-07 17:00:00+0000', tz='UTC'): 10.4,
     Timestamp('2019-07-07 18:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-07 19:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-07-07 20:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-07 21:00:00+0000', tz='UTC'): 6.3,
     Timestamp('2019-07-07 22:00:00+0000', tz='UTC'): 7.4,
     Timestamp('2019-07-07 23:00:00+0000', tz='UTC'): 6.9,
     Timestamp('2019-07-08 00:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-07-08 01:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-08 02:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-08 03:00:00+0000', tz='UTC'): 3.7,
     Timestamp('2019-07-08 04:00:00+0000', tz='UTC'): 4.4,
     Timestamp('2019-07-08 05:00:00+0000', tz='UTC'): 1.5,
     Timestamp('2019-07-08 06:00:00+0000', tz='UTC'): 2,
     Timestamp('2019-07-08 07:00:00+0000', tz='UTC'): 1.4,
     Timestamp('2019-07-08 08:00:00+0000', tz='UTC'): 2.3,
     Timestamp('2019-07-08 09:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-07-08 10:00:00+0000', tz='UTC'): 1.9,
     Timestamp('2019-07-08 11:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-07-08 12:00:00+0000', tz='UTC'): 2,
     Timestamp('2019-07-08 13:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-07-08 14:00:00+0000', tz='UTC'): 1.8,
     Timestamp('2019-07-08 15:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-07-08 16:00:00+0000', tz='UTC'): 0,
     Timestamp('2019-07-08 17:00:00+0000', tz='UTC'): -3.1,
     Timestamp('2019-07-08 18:00:00+0000', tz='UTC'): 0.2,
     Timestamp('2019-07-08 19:00:00+0000', tz='UTC'): 1.8,
     Timestamp('2019-07-08 20:00:00+0000', tz='UTC'): 2.8,
     Timestamp('2019-07-08 21:00:00+0000', tz='UTC'): 3.5,
     Timestamp('2019-07-08 22:00:00+0000', tz='UTC'): 5.7,
     Timestamp('2019-07-08 23:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-07-09 00:00:00+0000', tz='UTC'): 6.9,
     Timestamp('2019-07-09 01:00:00+0000', tz='UTC'): 8.3,
     Timestamp('2019-07-09 02:00:00+0000', tz='UTC'): 6.5,
     Timestamp('2019-07-09 03:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-07-09 04:00:00+0000', tz='UTC'): 4.6,
     Timestamp('2019-07-09 05:00:00+0000', tz='UTC'): 8,
     Timestamp('2019-07-09 06:00:00+0000', tz='UTC'): 9.8,
     Timestamp('2019-07-09 07:00:00+0000', tz='UTC'): 7.6,
     Timestamp('2019-07-09 08:00:00+0000', tz='UTC'): 9.7,
     Timestamp('2019-07-09 09:00:00+0000', tz='UTC'): 10.9,
     Timestamp('2019-07-09 10:00:00+0000', tz='UTC'): 12.4,
     Timestamp('2019-07-09 11:00:00+0000', tz='UTC'): 11.7,
     Timestamp('2019-07-09 12:00:00+0000', tz='UTC'): 8.4,
     Timestamp('2019-07-09 13:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-07-09 14:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-07-09 15:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-09 16:00:00+0000', tz='UTC'): 3.5,
     Timestamp('2019-07-09 17:00:00+0000', tz='UTC'): 1.2,
     Timestamp('2019-07-09 18:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-07-09 19:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-09 20:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-07-09 21:00:00+0000', tz='UTC'): 9,
     Timestamp('2019-07-09 22:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-09 23:00:00+0000', tz='UTC'): 8.3,
     Timestamp('2019-07-10 00:00:00+0000', tz='UTC'): 12.4,
     Timestamp('2019-07-10 01:00:00+0000', tz='UTC'): 15.2,
     Timestamp('2019-07-10 02:00:00+0000', tz='UTC'): 13.7,
     Timestamp('2019-07-10 03:00:00+0000', tz='UTC'): 13.5,
     Timestamp('2019-07-10 04:00:00+0000', tz='UTC'): 10.7,
     Timestamp('2019-07-10 05:00:00+0000', tz='UTC'): 11,
     Timestamp('2019-07-10 06:00:00+0000', tz='UTC'): 10.9,
     Timestamp('2019-07-10 07:00:00+0000', tz='UTC'): 14.1,
     Timestamp('2019-07-10 08:00:00+0000', tz='UTC'): 15.5,
     Timestamp('2019-07-10 09:00:00+0000', tz='UTC'): 14.5,
     Timestamp('2019-07-10 10:00:00+0000', tz='UTC'): 15.5,
     Timestamp('2019-07-10 11:00:00+0000', tz='UTC'): 11.6,
     Timestamp('2019-07-10 12:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-10 13:00:00+0000', tz='UTC'): 8.8,
     Timestamp('2019-07-10 14:00:00+0000', tz='UTC'): 9.8,
     Timestamp('2019-07-10 15:00:00+0000', tz='UTC'): 9.2,
     Timestamp('2019-07-10 16:00:00+0000', tz='UTC'): 9.4,
     Timestamp('2019-07-10 17:00:00+0000', tz='UTC'): 12.7,
     Timestamp('2019-07-10 18:00:00+0000', tz='UTC'): 11.4,
     Timestamp('2019-07-10 19:00:00+0000', tz='UTC'): 13.8,
     Timestamp('2019-07-10 20:00:00+0000', tz='UTC'): 11.4,
     Timestamp('2019-07-10 21:00:00+0000', tz='UTC'): 10.7,
     Timestamp('2019-07-10 22:00:00+0000', tz='UTC'): 11.7,
     Timestamp('2019-07-10 23:00:00+0000', tz='UTC'): 11,
     Timestamp('2019-07-11 00:00:00+0000', tz='UTC'): 12.2,
     Timestamp('2019-07-11 01:00:00+0000', tz='UTC'): 14.7,
     Timestamp('2019-07-11 02:00:00+0000', tz='UTC'): 12.5,
     Timestamp('2019-07-11 03:00:00+0000', tz='UTC'): 10.8,
     Timestamp('2019-07-11 04:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-07-11 05:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-07-11 06:00:00+0000', tz='UTC'): 8.8,
     Timestamp('2019-07-11 07:00:00+0000', tz='UTC'): 8.1,
     Timestamp('2019-07-11 08:00:00+0000', tz='UTC'): 9,
     Timestamp('2019-07-11 09:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-07-11 10:00:00+0000', tz='UTC'): 4.4,
     Timestamp('2019-07-11 11:00:00+0000', tz='UTC'): -0.1,
     Timestamp('2019-07-11 12:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-07-11 13:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-11 14:00:00+0000', tz='UTC'): 7.5,
     Timestamp('2019-07-11 15:00:00+0000', tz='UTC'): 7.5,
     Timestamp('2019-07-11 16:00:00+0000', tz='UTC'): 3,
     Timestamp('2019-07-11 17:00:00+0000', tz='UTC'): 1.2,
     Timestamp('2019-07-11 18:00:00+0000', tz='UTC'): 0.8,
     Timestamp('2019-07-11 19:00:00+0000', tz='UTC'): 0.6,
     Timestamp('2019-07-11 20:00:00+0000', tz='UTC'): -2.2,
     Timestamp('2019-07-11 21:00:00+0000', tz='UTC'): -2.2,
     Timestamp('2019-07-11 22:00:00+0000', tz='UTC'): 0,
     Timestamp('2019-07-11 23:00:00+0000', tz='UTC'): 0,
     Timestamp('2019-07-12 00:00:00+0000', tz='UTC'): 1.2,
     Timestamp('2019-07-12 01:00:00+0000', tz='UTC'): -4.9,
     Timestamp('2019-07-12 02:00:00+0000', tz='UTC'): -2.7,
     Timestamp('2019-07-12 04:00:00+0000', tz='UTC'): -0.9,
     Timestamp('2019-07-12 05:00:00+0000', tz='UTC'): -0.2,
     Timestamp('2019-07-12 06:00:00+0000', tz='UTC'): -1.9,
     Timestamp('2019-07-12 07:00:00+0000', tz='UTC'): -0.4,
     Timestamp('2019-07-12 08:00:00+0000', tz='UTC'): -0.5,
     Timestamp('2019-07-12 09:00:00+0000', tz='UTC'): 0.9,
     Timestamp('2019-07-12 10:00:00+0000', tz='UTC'): 2.1,
     Timestamp('2019-07-12 11:00:00+0000', tz='UTC'): 2.9,
     Timestamp('2019-07-12 12:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-07-12 13:00:00+0000', tz='UTC'): 5.4,
     Timestamp('2019-07-12 14:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-12 17:00:00+0000', tz='UTC'): -4.7,
     Timestamp('2019-07-12 18:00:00+0000', tz='UTC'): -4.6,
     Timestamp('2019-07-12 19:00:00+0000', tz='UTC'): -4.5,
     Timestamp('2019-07-12 20:00:00+0000', tz='UTC'): -3.4,
     Timestamp('2019-07-12 21:00:00+0000', tz='UTC'): -2.8,
     Timestamp('2019-07-12 22:00:00+0000', tz='UTC'): -2.8,
     Timestamp('2019-07-12 23:00:00+0000', tz='UTC'): -2.1,
     Timestamp('2019-07-13 00:00:00+0000', tz='UTC'): -0.2,
     Timestamp('2019-07-13 01:00:00+0000', tz='UTC'): 0.3,
     Timestamp('2019-07-13 02:00:00+0000', tz='UTC'): 0.5,
     Timestamp('2019-07-13 03:00:00+0000', tz='UTC'): 0.1,
     Timestamp('2019-07-13 04:00:00+0000', tz='UTC'): 0.6,
     Timestamp('2019-07-13 05:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-13 06:00:00+0000', tz='UTC'): 2,
     Timestamp('2019-07-13 07:00:00+0000', tz='UTC'): 2.9,
     Timestamp('2019-07-13 08:00:00+0000', tz='UTC'): 3.4,
     Timestamp('2019-07-13 09:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-07-13 10:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-07-13 11:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-07-13 12:00:00+0000', tz='UTC'): 4.4,
     Timestamp('2019-07-13 13:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-07-13 14:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-07-13 15:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-07-13 16:00:00+0000', tz='UTC'): 2.6,
     Timestamp('2019-07-13 17:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-07-13 18:00:00+0000', tz='UTC'): 3.1,
     Timestamp('2019-07-13 19:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-07-13 20:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-13 21:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-07-13 22:00:00+0000', tz='UTC'): 5.4,
     Timestamp('2019-07-13 23:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-07-14 00:00:00+0000', tz='UTC'): 10.4,
     Timestamp('2019-07-14 01:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-07-14 02:00:00+0000', tz='UTC'): 5.3,
     Timestamp('2019-07-14 03:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-07-14 05:00:00+0000', tz='UTC'): 4.6,
     Timestamp('2019-07-14 06:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-07-14 07:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-07-14 08:00:00+0000', tz='UTC'): 8.3,
     Timestamp('2019-07-14 09:00:00+0000', tz='UTC'): 8.8,
     Timestamp('2019-07-14 10:00:00+0000', tz='UTC'): 10.5,
     Timestamp('2019-07-14 11:00:00+0000', tz='UTC'): 10.3,
     Timestamp('2019-07-14 12:00:00+0000', tz='UTC'): 9.2,
     Timestamp('2019-07-14 13:00:00+0000', tz='UTC'): 8.1,
     Timestamp('2019-07-14 14:00:00+0000', tz='UTC'): 8.1,
     Timestamp('2019-07-14 15:00:00+0000', tz='UTC'): 7.9,
     Timestamp('2019-07-14 16:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-07-14 17:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-07-14 18:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-07-14 19:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-07-14 20:00:00+0000', tz='UTC'): 2.7,
     Timestamp('2019-07-14 21:00:00+0000', tz='UTC'): 1.5,
     Timestamp('2019-07-14 22:00:00+0000', tz='UTC'): 1.9,
     Timestamp('2019-07-14 23:00:00+0000', tz='UTC'): 2.9,
     Timestamp('2019-07-15 00:00:00+0000', tz='UTC'): 3.5,
     Timestamp('2019-07-15 01:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-07-15 02:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-07-15 03:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-07-15 04:00:00+0000', tz='UTC'): 1.8,
     Timestamp('2019-07-15 05:00:00+0000', tz='UTC'): -0.1,
     Timestamp('2019-07-15 06:00:00+0000', tz='UTC'): 0.1,
     Timestamp('2019-07-15 07:00:00+0000', tz='UTC'): 1.2,
     Timestamp('2019-07-15 08:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-07-15 09:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-07-15 10:00:00+0000', tz='UTC'): 3,
     Timestamp('2019-07-15 11:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-07-15 12:00:00+0000', tz='UTC'): 3.4,
     Timestamp('2019-07-15 13:00:00+0000', tz='UTC'): 1.8,
     Timestamp('2019-07-15 14:00:00+0000', tz='UTC'): -0.3,
     Timestamp('2019-07-15 15:00:00+0000', tz='UTC'): 0,
     Timestamp('2019-07-15 16:00:00+0000', tz='UTC'): 0.7,
     Timestamp('2019-07-15 17:00:00+0000', tz='UTC'): 1.5,
     Timestamp('2019-07-15 18:00:00+0000', tz='UTC'): 2.2,
     Timestamp('2019-07-15 19:00:00+0000', tz='UTC'): 2.2,
     Timestamp('2019-07-15 20:00:00+0000', tz='UTC'): 2.7,
     Timestamp('2019-07-15 21:00:00+0000', tz='UTC'): 2.2,
     Timestamp('2019-07-15 22:00:00+0000', tz='UTC'): 2.6,
     Timestamp('2019-07-15 23:00:00+0000', tz='UTC'): 2.1,
     Timestamp('2019-07-16 00:00:00+0000', tz='UTC'): 2.9,
     Timestamp('2019-07-16 01:00:00+0000', tz='UTC'): 4.6,
     Timestamp('2019-07-16 02:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-07-16 03:00:00+0000', tz='UTC'): 6.9,
     Timestamp('2019-07-16 04:00:00+0000', tz='UTC'): 8.7,
     Timestamp('2019-07-16 05:00:00+0000', tz='UTC'): 4.6,
     Timestamp('2019-07-16 06:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-07-16 07:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-07-16 08:00:00+0000', tz='UTC'): 6.1,
     Timestamp('2019-07-16 09:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-07-16 10:00:00+0000', tz='UTC'): 9.2,
     Timestamp('2019-07-16 11:00:00+0000', tz='UTC'): 8.7,
     Timestamp('2019-07-16 12:00:00+0000', tz='UTC'): 12.4,
     Timestamp('2019-07-16 13:00:00+0000', tz='UTC'): 8.2,
     Timestamp('2019-07-16 14:00:00+0000', tz='UTC'): 7.7,
     Timestamp('2019-07-16 15:00:00+0000', tz='UTC'): 8.3,
     Timestamp('2019-07-16 16:00:00+0000', tz='UTC'): 8.1,
     Timestamp('2019-07-16 17:00:00+0000', tz='UTC'): 8,
     Timestamp('2019-07-16 18:00:00+0000', tz='UTC'): 9.2,
     Timestamp('2019-07-16 19:00:00+0000', tz='UTC'): 11.7,
     Timestamp('2019-07-16 20:00:00+0000', tz='UTC'): 11.1,
     Timestamp('2019-07-16 21:00:00+0000', tz='UTC'): 10.5,
     Timestamp('2019-07-16 22:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-07-16 23:00:00+0000', tz='UTC'): 11.1,
     Timestamp('2019-07-17 00:00:00+0000', tz='UTC'): 11.6,
     Timestamp('2019-07-17 01:00:00+0000', tz='UTC'): 12.1,
     Timestamp('2019-07-17 02:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-07-17 03:00:00+0000', tz='UTC'): 10.4,
     Timestamp('2019-07-17 04:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-17 05:00:00+0000', tz='UTC'): 6.5,
     Timestamp('2019-07-17 06:00:00+0000', tz='UTC'): 8.3,
     Timestamp('2019-07-17 07:00:00+0000', tz='UTC'): 7.2,
     Timestamp('2019-07-17 08:00:00+0000', tz='UTC'): 11.2,
     Timestamp('2019-07-17 09:00:00+0000', tz='UTC'): 11.7,
     Timestamp('2019-07-17 10:00:00+0000', tz='UTC'): 14.2,
     Timestamp('2019-07-17 11:00:00+0000', tz='UTC'): 12.4,
     Timestamp('2019-07-17 12:00:00+0000', tz='UTC'): 15.3,
     Timestamp('2019-07-17 13:00:00+0000', tz='UTC'): 17.7,
     Timestamp('2019-07-17 14:00:00+0000', tz='UTC'): 17.9,
     Timestamp('2019-07-17 15:00:00+0000', tz='UTC'): 17.9,
     Timestamp('2019-07-17 16:00:00+0000', tz='UTC'): 18.8,
     Timestamp('2019-07-17 17:00:00+0000', tz='UTC'): 17.4,
     Timestamp('2019-07-17 19:00:00+0000', tz='UTC'): 12.7,
     Timestamp('2019-07-17 20:00:00+0000', tz='UTC'): 12.7,
     Timestamp('2019-07-17 21:00:00+0000', tz='UTC'): 12.6,
     Timestamp('2019-07-17 22:00:00+0000', tz='UTC'): 12.9,
     Timestamp('2019-07-17 23:00:00+0000', tz='UTC'): 14.8,
     Timestamp('2019-07-18 00:00:00+0000', tz='UTC'): 12.5,
     Timestamp('2019-07-18 01:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-18 02:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-18 03:00:00+0000', tz='UTC'): -1.6,
     Timestamp('2019-07-18 04:00:00+0000', tz='UTC'): -1.8,
     Timestamp('2019-07-18 05:00:00+0000', tz='UTC'): 0.1,
     Timestamp('2019-07-18 06:00:00+0000', tz='UTC'): 3.1,
     Timestamp('2019-07-18 07:00:00+0000', tz='UTC'): -0.8,
     Timestamp('2019-07-18 08:00:00+0000', tz='UTC'): 0.9,
     Timestamp('2019-07-18 09:00:00+0000', tz='UTC'): 1.6,
     Timestamp('2019-07-18 10:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-07-18 11:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-18 12:00:00+0000', tz='UTC'): 9.6,
     Timestamp('2019-07-18 13:00:00+0000', tz='UTC'): 11.6,
     Timestamp('2019-07-18 14:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-07-18 15:00:00+0000', tz='UTC'): 8.8,
     Timestamp('2019-07-18 16:00:00+0000', tz='UTC'): 11.5,
     Timestamp('2019-07-18 17:00:00+0000', tz='UTC'): 11.2,
     Timestamp('2019-07-18 18:00:00+0000', tz='UTC'): 7.6,
     Timestamp('2019-07-18 19:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-18 20:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-07-18 21:00:00+0000', tz='UTC'): 2.9,
     Timestamp('2019-07-18 22:00:00+0000', tz='UTC'): -0.1,
     Timestamp('2019-07-18 23:00:00+0000', tz='UTC'): 0.4,
     Timestamp('2019-07-19 00:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-07-19 01:00:00+0000', tz='UTC'): 2.8,
     Timestamp('2019-07-19 02:00:00+0000', tz='UTC'): 1.5,
     Timestamp('2019-07-19 03:00:00+0000', tz='UTC'): 1.8,
     Timestamp('2019-07-19 04:00:00+0000', tz='UTC'): 2.1,
     Timestamp('2019-07-19 05:00:00+0000', tz='UTC'): 0.9,
     Timestamp('2019-07-19 06:00:00+0000', tz='UTC'): 0.4,
     Timestamp('2019-07-19 07:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-07-19 08:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-07-19 09:00:00+0000', tz='UTC'): 6.4,
     Timestamp('2019-07-19 10:00:00+0000', tz='UTC'): 11.1,
     Timestamp('2019-07-19 11:00:00+0000', tz='UTC'): 7.6,
     Timestamp('2019-07-19 12:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-19 13:00:00+0000', tz='UTC'): 9.8,
     Timestamp('2019-07-19 14:00:00+0000', tz='UTC'): 12.3,
     Timestamp('2019-07-19 15:00:00+0000', tz='UTC'): 11.5,
     Timestamp('2019-07-19 16:00:00+0000', tz='UTC'): 11.5,
     Timestamp('2019-07-19 17:00:00+0000', tz='UTC'): 9.7,
     Timestamp('2019-07-19 18:00:00+0000', tz='UTC'): 10,
     Timestamp('2019-07-19 19:00:00+0000', tz='UTC'): 10.8,
     Timestamp('2019-07-19 20:00:00+0000', tz='UTC'): 14.1,
     Timestamp('2019-07-19 21:00:00+0000', tz='UTC'): 16.2,
     Timestamp('2019-07-19 22:00:00+0000', tz='UTC'): 9.6,
     Timestamp('2019-07-19 23:00:00+0000', tz='UTC'): 14.7,
     Timestamp('2019-07-20 00:00:00+0000', tz='UTC'): 17.2,
     Timestamp('2019-07-20 01:00:00+0000', tz='UTC'): 19.5,
     Timestamp('2019-07-20 02:00:00+0000', tz='UTC'): 18.2,
     Timestamp('2019-07-20 03:00:00+0000', tz='UTC'): 15.9,
     Timestamp('2019-07-20 04:00:00+0000', tz='UTC'): 16.9,
     Timestamp('2019-07-20 05:00:00+0000', tz='UTC'): 17,
     Timestamp('2019-07-20 06:00:00+0000', tz='UTC'): 18.1,
     Timestamp('2019-07-20 07:00:00+0000', tz='UTC'): 18.5,
     Timestamp('2019-07-20 08:00:00+0000', tz='UTC'): 18.9,
     Timestamp('2019-07-20 09:00:00+0000', tz='UTC'): 19.7,
     Timestamp('2019-07-20 10:00:00+0000', tz='UTC'): 23,
     Timestamp('2019-07-20 11:00:00+0000', tz='UTC'): 19.8,
     Timestamp('2019-07-20 12:00:00+0000', tz='UTC'): 17,
     Timestamp('2019-07-20 13:00:00+0000', tz='UTC'): 12,
     Timestamp('2019-07-20 14:00:00+0000', tz='UTC'): 12.8,
     Timestamp('2019-07-20 15:00:00+0000', tz='UTC'): 10.9,
     Timestamp('2019-07-20 16:00:00+0000', tz='UTC'): 14.3,
     Timestamp('2019-07-20 17:00:00+0000', tz='UTC'): 7.2,
     Timestamp('2019-07-20 18:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-07-20 19:00:00+0000', tz='UTC'): 6.9,
     Timestamp('2019-07-20 20:00:00+0000', tz='UTC'): 7.6,
     Timestamp('2019-07-20 21:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-20 22:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-07-20 23:00:00+0000', tz='UTC'): 10.8,
     Timestamp('2019-07-21 00:00:00+0000', tz='UTC'): 13,
     Timestamp('2019-07-21 01:00:00+0000', tz='UTC'): 17.7,
     Timestamp('2019-07-21 02:00:00+0000', tz='UTC'): 16.5,
     Timestamp('2019-07-21 03:00:00+0000', tz='UTC'): 17.5,
     Timestamp('2019-07-21 04:00:00+0000', tz='UTC'): 23.2,
     Timestamp('2019-07-21 05:00:00+0000', tz='UTC'): 20.6,
     Timestamp('2019-07-21 06:00:00+0000', tz='UTC'): 19.8,
     Timestamp('2019-07-21 07:00:00+0000', tz='UTC'): 20.1,
     Timestamp('2019-07-21 08:00:00+0000', tz='UTC'): 18.4,
     Timestamp('2019-07-21 09:00:00+0000', tz='UTC'): 16.9,
     Timestamp('2019-07-21 10:00:00+0000', tz='UTC'): 20.6,
     Timestamp('2019-07-21 11:00:00+0000', tz='UTC'): 13.8,
     Timestamp('2019-07-21 12:00:00+0000', tz='UTC'): 13.9,
     Timestamp('2019-07-21 13:00:00+0000', tz='UTC'): 9.9,
     Timestamp('2019-07-21 14:00:00+0000', tz='UTC'): 10.7,
     Timestamp('2019-07-21 15:00:00+0000', tz='UTC'): 13.1,
     Timestamp('2019-07-21 16:00:00+0000', tz='UTC'): 10.3,
     Timestamp('2019-07-21 17:00:00+0000', tz='UTC'): 12.3,
     Timestamp('2019-07-21 18:00:00+0000', tz='UTC'): 11.2,
     Timestamp('2019-07-21 19:00:00+0000', tz='UTC'): 10.8,
     Timestamp('2019-07-21 20:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-07-21 21:00:00+0000', tz='UTC'): 7.7,
     Timestamp('2019-07-21 22:00:00+0000', tz='UTC'): 15.5,
     Timestamp('2019-07-21 23:00:00+0000', tz='UTC'): 14.4,
     Timestamp('2019-07-22 00:00:00+0000', tz='UTC'): 12.8,
     Timestamp('2019-07-22 01:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-07-22 02:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-22 03:00:00+0000', tz='UTC'): 10.6,
     Timestamp('2019-07-22 04:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-07-22 05:00:00+0000', tz='UTC'): 3.5,
     Timestamp('2019-07-22 06:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-22 07:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-07-22 08:00:00+0000', tz='UTC'): 1.5,
     Timestamp('2019-07-22 09:00:00+0000', tz='UTC'): 4.6,
     Timestamp('2019-07-22 10:00:00+0000', tz='UTC'): 6.4,
     Timestamp('2019-07-22 11:00:00+0000', tz='UTC'): 7.1,
     Timestamp('2019-07-22 12:00:00+0000', tz='UTC'): 11.3,
     Timestamp('2019-07-22 13:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-07-22 14:00:00+0000', tz='UTC'): 6.7,
     Timestamp('2019-07-22 17:00:00+0000', tz='UTC'): -1.9,
     Timestamp('2019-07-22 18:00:00+0000', tz='UTC'): 0.6,
     Timestamp('2019-07-22 19:00:00+0000', tz='UTC'): 0.7,
     Timestamp('2019-07-22 20:00:00+0000', tz='UTC'): 3.4,
     Timestamp('2019-07-22 21:00:00+0000', tz='UTC'): 6.9,
     Timestamp('2019-07-22 23:00:00+0000', tz='UTC'): -1.3,
     Timestamp('2019-07-23 00:00:00+0000', tz='UTC'): -2.8,
     Timestamp('2019-07-23 01:00:00+0000', tz='UTC'): -0.9,
     Timestamp('2019-07-23 02:00:00+0000', tz='UTC'): -2.9,
     Timestamp('2019-07-23 03:00:00+0000', tz='UTC'): -2.2,
     Timestamp('2019-07-23 04:00:00+0000', tz='UTC'): -2.8,
     Timestamp('2019-07-23 05:00:00+0000', tz='UTC'): 0.2,
     Timestamp('2019-07-23 06:00:00+0000', tz='UTC'): -0.6,
     Timestamp('2019-07-23 07:00:00+0000', tz='UTC'): 0.3,
     Timestamp('2019-07-23 08:00:00+0000', tz='UTC'): -3.7,
     Timestamp('2019-07-23 09:00:00+0000', tz='UTC'): -4.5,
     Timestamp('2019-07-23 10:00:00+0000', tz='UTC'): -3.5,
     Timestamp('2019-07-23 11:00:00+0000', tz='UTC'): -2.8,
     Timestamp('2019-07-23 12:00:00+0000', tz='UTC'): -0.6,
     Timestamp('2019-07-23 13:00:00+0000', tz='UTC'): -0.9,
     Timestamp('2019-07-23 14:00:00+0000', tz='UTC'): -2.3,
     Timestamp('2019-07-23 15:00:00+0000', tz='UTC'): -1.9,
     Timestamp('2019-07-23 16:00:00+0000', tz='UTC'): -3,
     Timestamp('2019-07-23 17:00:00+0000', tz='UTC'): -0.4,
     Timestamp('2019-07-23 18:00:00+0000', tz='UTC'): -0.2,
     Timestamp('2019-07-23 19:00:00+0000', tz='UTC'): -1.8,
     Timestamp('2019-07-23 20:00:00+0000', tz='UTC'): -1.5,
     Timestamp('2019-07-23 21:00:00+0000', tz='UTC'): -1.8,
     Timestamp('2019-07-23 22:00:00+0000', tz='UTC'): -1,
     Timestamp('2019-07-23 23:00:00+0000', tz='UTC'): 0,
     Timestamp('2019-07-24 00:00:00+0000', tz='UTC'): -1.2,
     Timestamp('2019-07-24 01:00:00+0000', tz='UTC'): -0.6,
     Timestamp('2019-07-24 02:00:00+0000', tz='UTC'): -1.6,
     Timestamp('2019-07-24 03:00:00+0000', tz='UTC'): -0.9,
     Timestamp('2019-07-24 04:00:00+0000', tz='UTC'): -0.8,
     Timestamp('2019-07-24 05:00:00+0000', tz='UTC'): -2.1,
     Timestamp('2019-07-24 06:00:00+0000', tz='UTC'): -0.1,
     Timestamp('2019-07-24 11:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-07-24 12:00:00+0000', tz='UTC'): 0.3,
     Timestamp('2019-07-24 13:00:00+0000', tz='UTC'): 0,
     Timestamp('2019-07-24 14:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-07-24 15:00:00+0000', tz='UTC'): 2.3,
     Timestamp('2019-07-24 16:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-07-24 17:00:00+0000', tz='UTC'): 3.5,
     Timestamp('2019-07-24 18:00:00+0000', tz='UTC'): 2.6,
     Timestamp('2019-07-24 19:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-07-24 20:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-07-24 21:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-24 22:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-24 23:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-07-25 00:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-25 01:00:00+0000', tz='UTC'): 7.4,
     Timestamp('2019-07-25 02:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-07-25 03:00:00+0000', tz='UTC'): 5.6,
     Timestamp('2019-07-25 04:00:00+0000', tz='UTC'): 5.9,
     Timestamp('2019-07-25 05:00:00+0000', tz='UTC'): 5.5,
     Timestamp('2019-07-25 06:00:00+0000', tz='UTC'): 7.7,
     Timestamp('2019-07-25 07:00:00+0000', tz='UTC'): 10.8,
     Timestamp('2019-07-25 08:00:00+0000', tz='UTC'): 11.7,
     Timestamp('2019-07-25 09:00:00+0000', tz='UTC'): 11.2,
     Timestamp('2019-07-25 10:00:00+0000', tz='UTC'): 5.7,
     Timestamp('2019-07-25 11:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-07-25 12:00:00+0000', tz='UTC'): 4.1,
     Timestamp('2019-07-25 13:00:00+0000', tz='UTC'): 3.7,
     Timestamp('2019-07-25 14:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-07-25 15:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-07-25 18:00:00+0000', tz='UTC'): 4.1,
     Timestamp('2019-07-25 19:00:00+0000', tz='UTC'): 5.3,
     Timestamp('2019-07-25 20:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-07-25 21:00:00+0000', tz='UTC'): 7.8,
     Timestamp('2019-07-25 22:00:00+0000', tz='UTC'): 6.4,
     Timestamp('2019-07-25 23:00:00+0000', tz='UTC'): 2.6,
     Timestamp('2019-07-26 00:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-07-26 01:00:00+0000', tz='UTC'): 6.1,
     Timestamp('2019-07-26 02:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-07-26 03:00:00+0000', tz='UTC'): 4.1,
     Timestamp('2019-07-26 04:00:00+0000', tz='UTC'): 6.1,
     Timestamp('2019-07-26 05:00:00+0000', tz='UTC'): 8.4,
     Timestamp('2019-07-26 06:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-26 07:00:00+0000', tz='UTC'): 8.7,
     Timestamp('2019-07-26 08:00:00+0000', tz='UTC'): 9,
     Timestamp('2019-07-26 09:00:00+0000', tz='UTC'): 10.8,
     Timestamp('2019-07-26 10:00:00+0000', tz='UTC'): 10.2,
     Timestamp('2019-07-26 11:00:00+0000', tz='UTC'): 13.1,
     Timestamp('2019-07-26 12:00:00+0000', tz='UTC'): 8.7,
     Timestamp('2019-07-26 13:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-07-26 14:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-26 15:00:00+0000', tz='UTC'): 5.4,
     Timestamp('2019-07-26 16:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-07-26 18:00:00+0000', tz='UTC'): 5.6,
     Timestamp('2019-07-26 19:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-07-26 20:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-07-26 21:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-07-26 22:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-07-26 23:00:00+0000', tz='UTC'): 5.3,
     Timestamp('2019-07-27 00:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-07-27 01:00:00+0000', tz='UTC'): 11.7,
     Timestamp('2019-07-27 02:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-07-27 03:00:00+0000', tz='UTC'): 5.9,
     Timestamp('2019-07-27 04:00:00+0000', tz='UTC'): 6.3,
     Timestamp('2019-07-27 05:00:00+0000', tz='UTC'): 10.1,
     Timestamp('2019-07-27 06:00:00+0000', tz='UTC'): 7.9,
     Timestamp('2019-07-27 07:00:00+0000', tz='UTC'): 7.4,
     Timestamp('2019-07-27 08:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-07-27 09:00:00+0000', tz='UTC'): 11.5,
     Timestamp('2019-07-27 10:00:00+0000', tz='UTC'): 9.7,
     Timestamp('2019-07-27 11:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-07-27 12:00:00+0000', tz='UTC'): 7.1,
     Timestamp('2019-07-27 13:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-07-27 14:00:00+0000', tz='UTC'): 6.7,
     Timestamp('2019-07-27 15:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-07-27 16:00:00+0000', tz='UTC'): 10.9,
     Timestamp('2019-07-27 17:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-07-27 18:00:00+0000', tz='UTC'): 5.7,
     Timestamp('2019-07-27 19:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-07-27 20:00:00+0000', tz='UTC'): -0.4,
     Timestamp('2019-07-27 21:00:00+0000', tz='UTC'): 3.6,
     Timestamp('2019-07-27 22:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-07-27 23:00:00+0000', tz='UTC'): 3.7,
     Timestamp('2019-07-28 00:00:00+0000', tz='UTC'): 7.2,
     Timestamp('2019-07-28 01:00:00+0000', tz='UTC'): 7.5,
     Timestamp('2019-07-28 02:00:00+0000', tz='UTC'): 4.6,
     Timestamp('2019-07-28 03:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-28 04:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-07-28 05:00:00+0000', tz='UTC'): 4.2,
     Timestamp('2019-07-28 06:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-07-28 07:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-07-28 08:00:00+0000', tz='UTC'): 8,
     Timestamp('2019-07-28 09:00:00+0000', tz='UTC'): 9,
     Timestamp('2019-07-28 10:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-28 11:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-07-28 12:00:00+0000', tz='UTC'): 8.8,
     Timestamp('2019-07-28 13:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-28 14:00:00+0000', tz='UTC'): 10.2,
     Timestamp('2019-07-28 15:00:00+0000', tz='UTC'): 10.6,
     Timestamp('2019-07-28 16:00:00+0000', tz='UTC'): 6.5,
     Timestamp('2019-07-28 17:00:00+0000', tz='UTC'): 6.7,
     Timestamp('2019-07-28 18:00:00+0000', tz='UTC'): 7.7,
     Timestamp('2019-07-28 19:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-28 20:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-07-28 21:00:00+0000', tz='UTC'): 10.5,
     Timestamp('2019-07-28 22:00:00+0000', tz='UTC'): 10.6,
     Timestamp('2019-07-28 23:00:00+0000', tz='UTC'): 11.7,
     Timestamp('2019-07-29 00:00:00+0000', tz='UTC'): 12.3,
     Timestamp('2019-07-29 01:00:00+0000', tz='UTC'): 13.8,
     Timestamp('2019-07-29 02:00:00+0000', tz='UTC'): 12.3,
     Timestamp('2019-07-29 03:00:00+0000', tz='UTC'): 9.4,
     Timestamp('2019-07-29 04:00:00+0000', tz='UTC'): 2.7,
     Timestamp('2019-07-29 05:00:00+0000', tz='UTC'): 1.1,
     Timestamp('2019-07-29 06:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-07-29 07:00:00+0000', tz='UTC'): 2.8,
     Timestamp('2019-07-29 08:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-07-29 09:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-07-29 10:00:00+0000', tz='UTC'): 7.2,
     Timestamp('2019-07-29 11:00:00+0000', tz='UTC'): 14.6,
     Timestamp('2019-07-29 12:00:00+0000', tz='UTC'): 16.3,
     Timestamp('2019-07-29 13:00:00+0000', tz='UTC'): 16.2,
     Timestamp('2019-07-29 14:00:00+0000', tz='UTC'): 16.9,
     Timestamp('2019-07-29 15:00:00+0000', tz='UTC'): 14.9,
     Timestamp('2019-07-29 16:00:00+0000', tz='UTC'): 15.7,
     Timestamp('2019-07-29 17:00:00+0000', tz='UTC'): 14.7,
     Timestamp('2019-07-29 18:00:00+0000', tz='UTC'): 19.5,
     Timestamp('2019-07-29 19:00:00+0000', tz='UTC'): 19,
     Timestamp('2019-07-29 20:00:00+0000', tz='UTC'): 16.9,
     Timestamp('2019-07-29 21:00:00+0000', tz='UTC'): 14.5,
     Timestamp('2019-07-29 22:00:00+0000', tz='UTC'): 16.6,
     Timestamp('2019-07-29 23:00:00+0000', tz='UTC'): 13.8,
     Timestamp('2019-07-30 00:00:00+0000', tz='UTC'): 16.4,
     Timestamp('2019-07-30 01:00:00+0000', tz='UTC'): 19.6,
     Timestamp('2019-07-30 02:00:00+0000', tz='UTC'): 20,
     Timestamp('2019-07-30 03:00:00+0000', tz='UTC'): 21.4,
     Timestamp('2019-07-30 04:00:00+0000', tz='UTC'): 23.3,
     Timestamp('2019-07-30 05:00:00+0000', tz='UTC'): 20,
     Timestamp('2019-07-30 06:00:00+0000', tz='UTC'): 20.9,
     Timestamp('2019-07-30 07:00:00+0000', tz='UTC'): 22.1,
     Timestamp('2019-07-30 08:00:00+0000', tz='UTC'): 20.4,
     Timestamp('2019-07-30 09:00:00+0000', tz='UTC'): 18.8,
     Timestamp('2019-07-30 10:00:00+0000', tz='UTC'): 18.7,
     Timestamp('2019-07-30 11:00:00+0000', tz='UTC'): 20.5,
     Timestamp('2019-07-30 12:00:00+0000', tz='UTC'): 21.1,
     Timestamp('2019-07-30 14:00:00+0000', tz='UTC'): 18.6,
     Timestamp('2019-07-30 15:00:00+0000', tz='UTC'): 18.2,
     Timestamp('2019-07-30 16:00:00+0000', tz='UTC'): 16.8,
     Timestamp('2019-07-30 17:00:00+0000', tz='UTC'): 19,
     Timestamp('2019-07-30 19:00:00+0000', tz='UTC'): 5.3,
     Timestamp('2019-07-30 20:00:00+0000', tz='UTC'): 5.3,
     Timestamp('2019-07-30 21:00:00+0000', tz='UTC'): 7.1,
     Timestamp('2019-07-30 22:00:00+0000', tz='UTC'): 8.2,
     Timestamp('2019-07-30 23:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-07-31 00:00:00+0000', tz='UTC'): 10.6,
     Timestamp('2019-07-31 01:00:00+0000', tz='UTC'): 9.8,
     Timestamp('2019-07-31 02:00:00+0000', tz='UTC'): 8.7,
     Timestamp('2019-07-31 03:00:00+0000', tz='UTC'): 8.5,
     Timestamp('2019-07-31 04:00:00+0000', tz='UTC'): 8.3,
     Timestamp('2019-07-31 05:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-07-31 06:00:00+0000', tz='UTC'): 6.9,
     Timestamp('2019-07-31 07:00:00+0000', tz='UTC'): 8.7,
     Timestamp('2019-07-31 08:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-07-31 09:00:00+0000', tz='UTC'): 10.5,
     Timestamp('2019-07-31 10:00:00+0000', tz='UTC'): 10,
     Timestamp('2019-07-31 11:00:00+0000', tz='UTC'): 8.2,
     Timestamp('2019-07-31 12:00:00+0000', tz='UTC'): 9.9,
     Timestamp('2019-07-31 13:00:00+0000', tz='UTC'): 13.3,
     Timestamp('2019-07-31 14:00:00+0000', tz='UTC'): 13,
     Timestamp('2019-07-31 15:00:00+0000', tz='UTC'): 14.4,
     Timestamp('2019-07-31 16:00:00+0000', tz='UTC'): 12.1,
     Timestamp('2019-07-31 17:00:00+0000', tz='UTC'): 10.9,
     Timestamp('2019-07-31 18:00:00+0000', tz='UTC'): 10.2,
     Timestamp('2019-07-31 20:00:00+0000', tz='UTC'): 1.8,
     Timestamp('2019-07-31 21:00:00+0000', tz='UTC'): 2.6,
     Timestamp('2019-07-31 22:00:00+0000', tz='UTC'): 5.4,
     Timestamp('2019-08-01 01:00:00+0000', tz='UTC'): 6.3,
     Timestamp('2019-08-01 02:00:00+0000', tz='UTC'): 8.2,
     Timestamp('2019-08-01 03:00:00+0000', tz='UTC'): 12.8,
     Timestamp('2019-08-01 04:00:00+0000', tz='UTC'): 8.5,
     Timestamp('2019-08-01 05:00:00+0000', tz='UTC'): 12.8,
     Timestamp('2019-08-01 06:00:00+0000', tz='UTC'): 12.3,
     Timestamp('2019-08-01 07:00:00+0000', tz='UTC'): 7.4,
     Timestamp('2019-08-01 08:00:00+0000', tz='UTC'): 3.4,
     Timestamp('2019-08-01 09:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-08-01 10:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-08-01 11:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-08-01 12:00:00+0000', tz='UTC'): 1.7,
     Timestamp('2019-08-01 16:00:00+0000', tz='UTC'): -2.8,
     Timestamp('2019-08-01 17:00:00+0000', tz='UTC'): -1,
     Timestamp('2019-08-01 18:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-08-01 19:00:00+0000', tz='UTC'): 1.4,
     Timestamp('2019-08-01 20:00:00+0000', tz='UTC'): 2.8,
     Timestamp('2019-08-01 21:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-08-01 22:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-08-01 23:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-08-02 00:00:00+0000', tz='UTC'): 3.5,
     Timestamp('2019-08-02 01:00:00+0000', tz='UTC'): 2,
     Timestamp('2019-08-02 02:00:00+0000', tz='UTC'): 2.3,
     Timestamp('2019-08-02 03:00:00+0000', tz='UTC'): 3.5,
     Timestamp('2019-08-02 04:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-08-02 05:00:00+0000', tz='UTC'): 7.1,
     Timestamp('2019-08-02 06:00:00+0000', tz='UTC'): 7.4,
     Timestamp('2019-08-02 07:00:00+0000', tz='UTC'): 8.4,
     Timestamp('2019-08-02 08:00:00+0000', tz='UTC'): 8.3,
     Timestamp('2019-08-02 09:00:00+0000', tz='UTC'): 11.3,
     Timestamp('2019-08-02 10:00:00+0000', tz='UTC'): 11.2,
     Timestamp('2019-08-02 11:00:00+0000', tz='UTC'): 8.7,
     Timestamp('2019-08-02 12:00:00+0000', tz='UTC'): 8.2,
     Timestamp('2019-08-02 13:00:00+0000', tz='UTC'): 11.4,
     Timestamp('2019-08-02 14:00:00+0000', tz='UTC'): 11.4,
     Timestamp('2019-08-02 15:00:00+0000', tz='UTC'): 8.5,
     Timestamp('2019-08-02 16:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-08-02 17:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-08-02 18:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-08-02 19:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-08-02 20:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-08-02 21:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-08-02 22:00:00+0000', tz='UTC'): 1.9,
     Timestamp('2019-08-02 23:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-08-03 00:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-08-03 01:00:00+0000', tz='UTC'): 4.4,
     Timestamp('2019-08-03 02:00:00+0000', tz='UTC'): 3.7,
     Timestamp('2019-08-03 03:00:00+0000', tz='UTC'): 3.6,
     Timestamp('2019-08-03 04:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-08-03 05:00:00+0000', tz='UTC'): 4.2,
     Timestamp('2019-08-03 06:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-08-03 07:00:00+0000', tz='UTC'): 3.4,
     Timestamp('2019-08-03 08:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-08-03 09:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-08-03 10:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-08-03 11:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-08-03 12:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-08-03 13:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-08-03 14:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-08-03 15:00:00+0000', tz='UTC'): 4.4,
     Timestamp('2019-08-03 16:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-08-03 17:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-08-03 18:00:00+0000', tz='UTC'): 3.4,
     Timestamp('2019-08-03 19:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-08-03 20:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-08-03 21:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-08-03 22:00:00+0000', tz='UTC'): 3.4,
     Timestamp('2019-08-03 23:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-08-04 00:00:00+0000', tz='UTC'): 5.4,
     Timestamp('2019-08-04 01:00:00+0000', tz='UTC'): 4.4,
     Timestamp('2019-08-04 02:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-08-04 03:00:00+0000', tz='UTC'): 2.1,
     Timestamp('2019-08-04 04:00:00+0000', tz='UTC'): -0.5,
     Timestamp('2019-08-04 05:00:00+0000', tz='UTC'): 1.1,
     Timestamp('2019-08-04 06:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-08-04 07:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-08-04 08:00:00+0000', tz='UTC'): 2.2,
     Timestamp('2019-08-04 09:00:00+0000', tz='UTC'): 5.9,
     Timestamp('2019-08-04 10:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-08-04 11:00:00+0000', tz='UTC'): 4.2,
     Timestamp('2019-08-04 12:00:00+0000', tz='UTC'): 2.3,
     Timestamp('2019-08-04 13:00:00+0000', tz='UTC'): 0.1,
     Timestamp('2019-08-04 14:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-08-04 15:00:00+0000', tz='UTC'): 2.6,
     Timestamp('2019-08-04 16:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-08-04 17:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-08-04 18:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-08-04 19:00:00+0000', tz='UTC'): 5.9,
     Timestamp('2019-08-04 20:00:00+0000', tz='UTC'): 8,
     Timestamp('2019-08-04 21:00:00+0000', tz='UTC'): 10.4,
     Timestamp('2019-08-04 22:00:00+0000', tz='UTC'): 10.4,
     Timestamp('2019-08-04 23:00:00+0000', tz='UTC'): 10.1,
     Timestamp('2019-08-05 00:00:00+0000', tz='UTC'): 12.7,
     Timestamp('2019-08-05 01:00:00+0000', tz='UTC'): 13.9,
     Timestamp('2019-08-05 02:00:00+0000', tz='UTC'): 7.8,
     Timestamp('2019-08-05 03:00:00+0000', tz='UTC'): 8.9,
     Timestamp('2019-08-05 04:00:00+0000', tz='UTC'): 11,
     Timestamp('2019-08-05 05:00:00+0000', tz='UTC'): 9.4,
     Timestamp('2019-08-05 06:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-08-05 07:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-08-05 08:00:00+0000', tz='UTC'): 2.1,
     Timestamp('2019-08-05 09:00:00+0000', tz='UTC'): 3.6,
     Timestamp('2019-08-05 10:00:00+0000', tz='UTC'): 5.4,
     Timestamp('2019-08-05 11:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-08-05 12:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-08-05 13:00:00+0000', tz='UTC'): 3.7,
     Timestamp('2019-08-05 14:00:00+0000', tz='UTC'): 2.8,
     Timestamp('2019-08-05 15:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-08-05 16:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-08-05 17:00:00+0000', tz='UTC'): 4.2,
     Timestamp('2019-08-05 18:00:00+0000', tz='UTC'): 2.3,
     Timestamp('2019-08-05 19:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-08-05 20:00:00+0000', tz='UTC'): 7,
     Timestamp('2019-08-05 21:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-08-05 22:00:00+0000', tz='UTC'): 6.4,
     Timestamp('2019-08-05 23:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-08-06 00:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-08-06 01:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-08-06 02:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-08-06 03:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-08-06 04:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-08-06 05:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-08-06 06:00:00+0000', tz='UTC'): 6.1,
     Timestamp('2019-08-06 07:00:00+0000', tz='UTC'): 5.7,
     Timestamp('2019-08-06 08:00:00+0000', tz='UTC'): 6.4,
     Timestamp('2019-08-06 09:00:00+0000', tz='UTC'): 6.1,
     Timestamp('2019-08-06 10:00:00+0000', tz='UTC'): 9.1,
     Timestamp('2019-08-06 11:00:00+0000', tz='UTC'): 10.5,
     Timestamp('2019-08-06 12:00:00+0000', tz='UTC'): 11.4,
     Timestamp('2019-08-06 13:00:00+0000', tz='UTC'): 11.7,
     Timestamp('2019-08-06 14:00:00+0000', tz='UTC'): 12.8,
     Timestamp('2019-08-06 15:00:00+0000', tz='UTC'): 12.4,
     Timestamp('2019-08-06 16:00:00+0000', tz='UTC'): 10.5,
     Timestamp('2019-08-06 17:00:00+0000', tz='UTC'): 5.6,
     Timestamp('2019-08-06 18:00:00+0000', tz='UTC'): 8.6,
     Timestamp('2019-08-06 19:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-08-06 20:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-08-06 21:00:00+0000', tz='UTC'): 6,
     Timestamp('2019-08-06 22:00:00+0000', tz='UTC'): 6.6,
     Timestamp('2019-08-06 23:00:00+0000', tz='UTC'): 7.9,
     Timestamp('2019-08-07 00:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-08-07 01:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-08-07 02:00:00+0000', tz='UTC'): 4.3,
     Timestamp('2019-08-07 03:00:00+0000', tz='UTC'): 4.1,
     Timestamp('2019-08-07 04:00:00+0000', tz='UTC'): 7,
     Timestamp('2019-08-07 05:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-08-07 06:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-08-07 07:00:00+0000', tz='UTC'): 5.6,
     Timestamp('2019-08-07 08:00:00+0000', tz='UTC'): 6.4,
     Timestamp('2019-08-07 09:00:00+0000', tz='UTC'): 8.1,
     Timestamp('2019-08-07 10:00:00+0000', tz='UTC'): 8,
     Timestamp('2019-08-07 11:00:00+0000', tz='UTC'): 9.4,
     Timestamp('2019-08-07 12:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-08-07 13:00:00+0000', tz='UTC'): 2.7,
     Timestamp('2019-08-07 14:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-08-07 15:00:00+0000', tz='UTC'): 7.4,
     Timestamp('2019-08-07 16:00:00+0000', tz='UTC'): 8.4,
     Timestamp('2019-08-07 17:00:00+0000', tz='UTC'): 7,
     Timestamp('2019-08-07 18:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-08-07 19:00:00+0000', tz='UTC'): 0.2,
     Timestamp('2019-08-07 20:00:00+0000', tz='UTC'): 11,
     Timestamp('2019-08-07 21:00:00+0000', tz='UTC'): -0.2,
     Timestamp('2019-08-07 22:00:00+0000', tz='UTC'): 5.4,
     Timestamp('2019-08-07 23:00:00+0000', tz='UTC'): 9.5,
     Timestamp('2019-08-08 00:00:00+0000', tz='UTC'): 3.3,
     Timestamp('2019-08-08 01:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-08-08 02:00:00+0000', tz='UTC'): 5.6,
     Timestamp('2019-08-08 03:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-08-08 04:00:00+0000', tz='UTC'): 1.9,
     Timestamp('2019-08-08 05:00:00+0000', tz='UTC'): 1.3,
     Timestamp('2019-08-08 06:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-08-08 07:00:00+0000', tz='UTC'): 5.9,
     Timestamp('2019-08-08 08:00:00+0000', tz='UTC'): 5.9,
     Timestamp('2019-08-08 09:00:00+0000', tz='UTC'): 6.1,
     Timestamp('2019-08-08 10:00:00+0000', tz='UTC'): 8.1,
     Timestamp('2019-08-08 11:00:00+0000', tz='UTC'): 9.3,
     Timestamp('2019-08-08 12:00:00+0000', tz='UTC'): 9.4,
     Timestamp('2019-08-08 13:00:00+0000', tz='UTC'): 8.3,
     Timestamp('2019-08-08 14:00:00+0000', tz='UTC'): 10.3,
     Timestamp('2019-08-08 15:00:00+0000', tz='UTC'): 6.3,
     Timestamp('2019-08-08 16:00:00+0000', tz='UTC'): 10.6,
     Timestamp('2019-08-08 17:00:00+0000', tz='UTC'): 7,
     Timestamp('2019-08-08 18:00:00+0000', tz='UTC'): 7.3,
     Timestamp('2019-08-08 19:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-08-08 20:00:00+0000', tz='UTC'): 7,
     Timestamp('2019-08-08 21:00:00+0000', tz='UTC'): 6.8,
     Timestamp('2019-08-08 22:00:00+0000', tz='UTC'): 9.6,
     Timestamp('2019-08-08 23:00:00+0000', tz='UTC'): 10.7,
     Timestamp('2019-08-09 00:00:00+0000', tz='UTC'): 5.3,
     Timestamp('2019-08-09 01:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-08-09 02:00:00+0000', tz='UTC'): 4.4,
     Timestamp('2019-08-09 03:00:00+0000', tz='UTC'): 4.8,
     Timestamp('2019-08-09 04:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-08-09 05:00:00+0000', tz='UTC'): 6.1,
     Timestamp('2019-08-09 06:00:00+0000', tz='UTC'): 7.9,
     Timestamp('2019-08-09 07:00:00+0000', tz='UTC'): 6.9,
     Timestamp('2019-08-09 08:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-08-09 09:00:00+0000', tz='UTC'): 5,
     Timestamp('2019-08-09 10:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-08-09 11:00:00+0000', tz='UTC'): 4,
     Timestamp('2019-08-09 12:00:00+0000', tz='UTC'): 3,
     Timestamp('2019-08-09 13:00:00+0000', tz='UTC'): 4.5,
     Timestamp('2019-08-09 14:00:00+0000', tz='UTC'): 2.6,
     Timestamp('2019-08-09 15:00:00+0000', tz='UTC'): 2,
     Timestamp('2019-08-09 16:00:00+0000', tz='UTC'): 4.2,
     Timestamp('2019-08-09 17:00:00+0000', tz='UTC'): 5.7,
     Timestamp('2019-08-09 18:00:00+0000', tz='UTC'): 2.4,
     Timestamp('2019-08-09 19:00:00+0000', tz='UTC'): 5.8,
     Timestamp('2019-08-09 20:00:00+0000', tz='UTC'): 6.2,
     Timestamp('2019-08-09 21:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-08-09 22:00:00+0000', tz='UTC'): 5.7,
     Timestamp('2019-08-09 23:00:00+0000', tz='UTC'): 4.7,
     Timestamp('2019-08-10 00:00:00+0000', tz='UTC'): 3.6,
     Timestamp('2019-08-10 01:00:00+0000', tz='UTC'): 5.1,
     Timestamp('2019-08-10 02:00:00+0000', tz='UTC'): 3.9,
     Timestamp('2019-08-10 03:00:00+0000', tz='UTC'): 5.2,
     Timestamp('2019-08-10 04:00:00+0000', tz='UTC'): 4.9,
     Timestamp('2019-08-10 05:00:00+0000', tz='UTC'): 3.8,
     Timestamp('2019-08-10 06:00:00+0000', tz='UTC'): 2.5,
     Timestamp('2019-08-10 07:00:00+0000', tz='UTC'): 0.8,
     Timestamp('2019-08-10 08:00:00+0000', tz='UTC'): 1.9,
     Timestamp('2019-08-10 09:00:00+0000', tz='UTC'): 2.8,
     Timestamp('2019-08-10 10:00:00+0000', tz='UTC'): 2.7,
     Timestamp('2019-08-10 11:00:00+0000', tz='UTC'): 2.8,
     Timestamp('2019-08-10 12:00:00+0000', tz='UTC'): 2.3,
     Timestamp('2019-08-10 13:00:00+0000', tz='UTC'): 0,
     Timestamp('2019-08-10 14:00:00+0000', tz='UTC'): 0.1,
     Timestamp('2019-08-10 15:00:00+0000', tz='UTC'): 0.9,
     Timestamp('2019-08-10 16:00:00+0000', tz='UTC'): -0.4,
     ...}




```python
assert(date_measurement[list(date_measurement.keys())[0]] == 1.6)
print('Correct')
```

    Correct


# Task 6
Find the average reading on each day of the week using whatever technique you care to choose.


```python
# Your code here
```


```python

```


```python
#__SOLUTION__

for week_day in set(day_of_week):
    
    day_cumulative = 0
    count = 0
    
    for day, measurement in zip(day_of_week, measurements):
        if week_day == day:
            day_cumulative += measurement
            count += 1
    
    print(week_day, day_cumulative/count)
```

    Sunday 6.031232876712325
    Wednesday 5.821192528735631
    Tuesday 5.342183098591558
    Friday 5.607234617985123
    Saturday 5.411336599020287
    Monday 5.555672268907566
    Thursday 6.100790229885051


# Bonus
Unlike lists and tuples, dictionaries are not ordered.  However, there are ways to sort dictionaries. Google how to sort a dictionary, and find the dates of the top 5 worst air-quality readings in Brooklyn.


```python
# Your code here
airquality_sorted = None
```


```python
#__SOLUTION__
# Choose whichever method you would like to find the dates of the top 5 worst air-quality readings in Brooklyn
# as given in the list

airquality_sorted = dict(sorted(date_measurement.items(), key=lambda x: x[1], reverse=True)[:5])
```


```python
assert(list(airquality_sorted.values())) == [55.4, 54.7, 53.3, 47.5, 44]
print('Correct')
```

    Correct



```python

```
