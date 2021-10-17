---
layout: post
title:  "Logging with Python"
date:   2021-10-17 00:42:02 +0100
categories: Python Development
katex: false
description: "How to log in Python 3"
---
# Logging in Python

I somehow never really bothered to setup proper logging in Python until recently. But some days ago I did it and discovered three different ways to do it. We will discuss those and also how to use it afterward. To learn about all the details about logging in Python refer to the [documentation](https://docs.python.org/3/library/logging.html).

## Why should I use logging

While developing the print function is quite often sufficient to see what is going on in your code, but when the code gets into production, there is nobody looking at the console any more. With the logging functionality it is possible to 

- set criticality levels (DEBUG, INFO, WARNING, ERROR, etc)
- define multiple targets for a log
- custom format the message (incl. time stamps)

## How

To use logging, you have to setup a logger. You either use the default logger or a named one. Then it is as simple as to call the function of the wanted criticality.

### Root logger

The root logger is the default logger. If there is no special need to handle logs from different parts differently this is the easiest way to go.

```python
import logging

logging.debug('message')
logging.info('message)
logging.warning('message')
logging.error('message')
```

### Named logger

Named logger allow to get specific logging behavior for different parts of the code. Maybe you want to handle warnings in a ETL process differently warnings occurring during model training. In a project with several modules this is the recommended way to go. 

```python
import logging

my_logger = logging.getLogger('myLogger')

my_logger.debug('message')
my_logger.info('message)
my_logger.warning('message')
my_logger.error('message')
```

### Exceptions

Quite often, when logging an error you would like to have some more information than just the error message. There are two ways to handle this

1. Add `exec_info` to the logging call
2. Use `my_logger.exception('My text')` in the except block

```python
try:
    some code
except:
    my_logger.exception('An error occured in my block')    
```

## Setup

I will discuss different methods to setup logging in an other post.