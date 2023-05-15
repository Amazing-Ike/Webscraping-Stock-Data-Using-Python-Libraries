In this project, we will use web-scraping to obtain financial data. 
Using beautiful soup we will extract historical share data from a web-page.

Table of Contents

-Extracting data using Beautiful soup
-Downloading the Webpage Using Requests Library
-Parsing Webpage HTML Using BeautifulSoup
-Extracting Data and Building DataFrame
-Extracting data using pandas


#!pip install pandas==1.3.3
#!pip install requests==2.26.0
!mamba install bs4==4.10.0 -y
!mamba install html5lib==1.1 -y 
!pip install lxml==4.6.4
#!pip install plotly==5.3.1

                  __    __    __    __
                 /  \  /  \  /  \  /  \
                /    \/    \/    \/    \
███████████████/  /██/  /██/  /██/  /████████████████████████
              /  / \   / \   / \   / \  \____
             /  /   \_/   \_/   \_/   \    o \__,
            / _/                       \_____/  `
            |/
        ███╗   ███╗ █████╗ ███╗   ███╗██████╗  █████╗
        ████╗ ████║██╔══██╗████╗ ████║██╔══██╗██╔══██╗
        ██╔████╔██║███████║██╔████╔██║██████╔╝███████║
        ██║╚██╔╝██║██╔══██║██║╚██╔╝██║██╔══██╗██╔══██║
        ██║ ╚═╝ ██║██║  ██║██║ ╚═╝ ██║██████╔╝██║  ██║
        ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝     ╚═╝╚═════╝ ╚═╝  ╚═╝

        mamba (1.4.2) supported by @QuantStack

        GitHub:  https://github.com/mamba-org/mamba
        Twitter: https://twitter.com/QuantStack

█████████████████████████████████████████████████████████████


Looking for: ['bs4==4.10.0']

[+] 0.0s
[+] 0.1s
pkgs/main/linux-64 ━━━━━━━━━╸━━━━━━━━━━━━━━━   0.0 B /  ??.?MB @  ??.?MB/s  0.1s
pkgs/main/noarch   ━━━━━━━━━━━━━╸━━━━━━━━━━━   0.0 B /  ??.?MB @  ??.?MB/s  0.1s
pkgs/r/linux-64    ━━━━━━━━━━╸━━━━━━━━━━━━━━   0.0 B /  ??.?MB @  ??.?MB/s  0.1s
pkgs/r/noarch      ━━━━━━━━━━━━╸━━━━━━━━━━━━   0.0 B /  ??.?MB @  ??.?MB/s  0.1s[+] 0.2s
pkgs/main/linux-64 ━━━━━━━━━━━╸━━━━━━━━━━━━━   0.0 B /  ??.?MB @  ??.?MB/s  0.2s
pkgs/main/noarch   ━━━━━━━━━━━━━━╸━━━━━━━━━━   0.0 B /  ??.?MB @  ??.?MB/s  0.2s
pkgs/r/linux-64    ━━━━━━━━━━━╸━━━━━━━━━━━━━   0.0 B /  ??.?MB @  ??.?MB/s  0.2s
pkgs/r/noarch      ━━━━━━━━━━━━━━╸━━━━━━━━━━   0.0 B /  ??.?MB @  ??.?MB/s  0.2spkgs/main/linux-64                                            No change
pkgs/main/noarch                                              No change
pkgs/r/linux-64                                               No change
pkgs/r/noarch                                                 No change
[+] 0.3s

Pinned packages:
  - python 3.7.*


Transaction

  Prefix: /home/jupyterlab/conda/envs/python

  All requested packages already installed


                  __    __    __    __
                 /  \  /  \  /  \  /  \
                /    \/    \/    \/    \
███████████████/  /██/  /██/  /██/  /████████████████████████
              /  / \   / \   / \   / \  \____
             /  /   \_/   \_/   \_/   \    o \__,
            / _/                       \_____/  `
            |/
        ███╗   ███╗ █████╗ ███╗   ███╗██████╗  █████╗
        ████╗ ████║██╔══██╗████╗ ████║██╔══██╗██╔══██╗
        ██╔████╔██║███████║██╔████╔██║██████╔╝███████║
        ██║╚██╔╝██║██╔══██║██║╚██╔╝██║██╔══██╗██╔══██║
        ██║ ╚═╝ ██║██║  ██║██║ ╚═╝ ██║██████╔╝██║  ██║
        ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝     ╚═╝╚═════╝ ╚═╝  ╚═╝

        mamba (1.4.2) supported by @QuantStack

        GitHub:  https://github.com/mamba-org/mamba
        Twitter: https://twitter.com/QuantStack

█████████████████████████████████████████████████████████████


Looking for: ['html5lib==1.1']

pkgs/main/linux-64                                          Using cache
pkgs/main/noarch                                            Using cache
pkgs/r/linux-64                                             Using cache
pkgs/r/noarch                                               Using cache

Pinned packages:
  - python 3.7.*


Transaction

  Prefix: /home/jupyterlab/conda/envs/python

  All requested packages already installed

Requirement already satisfied: lxml==4.6.4 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (4.6.4)

#Next is to import the required libraries (pandas, requests, and BeautifulSoup)

import pandas as pd
import requests
from bs4 import BeautifulSoup
import pandas as pd
import requests
from bs4 import BeautifulSoup

#Use Webscraping to Extract Stock Data

In this project, we are using yahoo finance website and looking to extract Amazon data.


#Table that we need to extract
On the following webpage we have a table with columns name (Date, Open, High, Low, close, adj close volume) out of which we must extract following columns

"Date"
"Open"
"High"
"Low"
"Close"
"Volume"

#Steps to be followed for extracting data
1. Send an HTTP request to the webpage using the requests library.
2. Parse the HTML content of the webpage using BeautifulSoup.
3. Identify the HTML tags that contain the data you want to extract.
4. Use BeautifulSoup methods to extract the data from the HTML tags.
5. Print the extracted data

#Step-1 Send an HTTP Request to the webpage
We are using Request library for sending an HTTP request to the webpage.

url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/amazon_data_webpage.html"
The requests.get() method takes a URL as its first argument, which specifies the location of the resource to be retrieved. In this case, the value of the url variable is passed as the argument to the requests.get() method, as we've stored a webpage URL in a url variable.

we have used .text method for extracting the HTML content as a string in order to make it readable.

data  = requests.get(url).text
print(data)

#Step:-2 Parse the HTML content

What is parsing?
In simple words, parsing refers to the process of analyzing a string of text or a data structure, 
usually following a set of rules or grammar, to understand its structure and meaning. 
Parsing involves breaking down a piece of text or data into its individual components or elements, 
and then analyzing those components to extract the desired information or to understand their relationships and meanings.

Next we will take the raw HTML content of a webpage or a string of HTML code which needs to be parsed and transformed into a structured, 
hierarchical format that can be more easily analyzed and manipulated in Python. 
This can be done using a Python library called Beautiful Soup.

How to parse the data using Beautiful soup library?
Create a new Beautiful soup object.

Note:- To create a Beautiful Soup object in Python, you need to pass two arguments to its constructor:
The HTML or XML content that you want to parse as a string.
The name of the parser that you want to use to parse the HTML or XML content. 
This argument is optional, and if you don't specify a parser, Beautiful Soup will use the default HTML parser included with the library.
here in this lab we are using "html5lib" parser.

soup = BeautifulSoup(data, 'html5lib')

#Step-3 Identify the HTML tags
As stated above webpage consist of table so, we will be scrapping the content of the HTML webpage and convert the table into a dataframe.

We will creates an empty DataFrame using the pd.DataFrame() function with the following columns.

"Date"
"Open"
"High"
"Low"
"Close"
"Volume"

amazon_data = pd.DataFrame(columns=["Date", "Open", "High", "Low", "Close", "Volume"])

Working on HTML table 

These are the following tags which are used while creating HTML tables.

<table> tag: This tag is root tag used to define the start and end of the table. 
  All the content of the table is enclosed within these tags.

<tr> tag: This tag is used to define a table row. Each row of the table is defined within this tag.

<td> tag: This tag is used to define a table cell. Each cell of the table is defined within this tag. 
  You can specify the content of the cell between the opening and closing tags.

<th> tag: This tag is used to define a header cell in the table. The header cell is used to describe the contents of a column or row. 
  By default, the text inside a tag is bold and centered.

<tbody> tag: This is the main content of the table, which is defined using the tag. It contains one or more rows of elements.

#Step-4 Use Beautiful soup method for extracting data
We will use find() and find_all() methods of the BeautifulSoup object to locate the table body and table row respectively in the HTML.

The find() method will return particular tag content.
The find_all() method returns a list of all matching tags in the HTML.
# First we isolate the body of the table which contains all the information
# Then we loop through each row and find all the column values for each row
for row in soup.find("tbody").find_all('tr'):
    col = row.find_all("td")
    date = col[0].text
    Open = col[1].text
    high = col[2].text
    low = col[3].text
    close = col[4].text
    adj_close = col[5].text
    volume = col[6].text
    
# Finally we append the data of each row to the table
amazon_data = amazon_data.append({"Date":date, "Open":Open, "High":high, "Low":low, "Close":close, "Adj Close":adj_close, "Volume":volume}, ignore_index=True)    

#Step-5 Print the Extracted Data
We can now print out the DataFrame using head() or tail() function

amazon_data.head()
  
#Extracting data using pandas library
We can also use the pandas read_html function from pandas library and use the URL for extracting data.

What is read_html in pandas library?
pd.read_html(url) is a function provided by the pandas library in Python that is used to extract tables from HTML web pages. 
It takes in a URL as input and returns a list of all the tables found on the webpage.

read_html_pandas_data = pd.read_html(url)
Or we can convert the BeautifulSoup object to a string

read_html_pandas_data = pd.read_html(str(soup))
Because there is only one table on the page, we just take the first table in the list returned

amazon_dataframe = read_html_pandas_data[0]
​
amazon_dataframe.head()
  
#Using Webscraping to Extract Stock Data
  
Use the requests library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/amazon_data_webpage.html. 
Save the text of the response as a variable named html_data.

url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/amazon_data_webpage.html"
html_data = requests.get(url).text

#Parse the html data using beautiful_soup.

soup = BeautifulSoup(html_data,"html5lib")

Question 1 What is the content of the title attribute?

soup.title
  
<title>Amazon.com, Inc. (AMZN) Stock Historical Prices &amp; Data - Yahoo Finance</title>
  
Using beautiful soup extract the table with historical share prices and store it into a dataframe named amazon_data. 
The dataframe should have columns Date, Open, High, Low, Close, Adj Close, and Volume. 
Fill in each variable with the correct data from the list col.

amazon_data = pd.DataFrame(columns=["Date", "Open", "High", "Low", "Close", "Volume"])
​
for row in soup.find("tbody").find_all('tr'):
    col = row.find_all("td")
    date = col[0].text
    Open = col[1].text
    high = col[2].text
    low = col[3].text
    close = col[4].text
    adj_close = col[5].text
    volume = col[6].text
    
# Finally we append the data of each row to the table
  
amazon_data = amazon_data.append({"Date":date, "Open":Open, "High":high, "Low":low, "Close":close, "Adj Close":adj_close, "Volume":volume}, ignore_index=True)  

#Print out the first five rows of the amazon_data dataframe you created.

amazon_data.head()
  
Date	Open	High	Low	Close	Volume	Adj Close
0	Jan 01, 2021	3,270.00	3,363.89	3,086.00	3,206.20	71,528,900	3,206.20
1	Dec 01, 2020	3,188.50	3,350.65	3,072.82	3,256.93	77,556,200	3,256.93
2	Nov 01, 2020	3,061.74	3,366.80	2,950.12	3,168.04	90,810,500	3,168.04
3	Oct 01, 2020	3,208.00	3,496.24	3,019.00	3,036.15	116,226,100	3,036.15
4	Sep 01, 2020	3,489.58	3,552.25	2,871.00	3,148.73	115,899,300	3,148.73

#What is the name of the columns of the dataframe?

amazon_data.columns

Index(['Date', 'Open', 'High', 'Low', 'Close', 'Volume', 'Adj Close'], dtype='object')
​
#What is the Open of the last row of the amazon_data dataframe?

amazon_data.tail()
Date	Open	High	Low	Close	Volume	Adj Close
56	May 01, 2016	663.92	724.23	656.00	722.79	90,614,500	722.79
57	Apr 01, 2016	590.49	669.98	585.25	659.59	78,464,200	659.59
58	Mar 01, 2016	556.29	603.24	538.58	593.64	94,009,500	593.64
59	Feb 01, 2016	578.15	581.80	474.00	552.52	124,144,800	552.52
60	Jan 01, 2016	656.29	657.72	547.18	587.00	130,200,900	587.00

