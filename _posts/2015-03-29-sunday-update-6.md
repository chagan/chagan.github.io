---
layout: post
title: Sunday Update No. 6&#58; Generating queries from csv with psycopg2
---

##The Numbers
* Total commits: 4
* Repos contributed to: 1
* Most popular repo: [Smartsheet Calendar](https://github.com/chagan/smartsheet-calendar)
* Most popular days: Mar. 25, 2 commits

##What I learned
The project I worked on most this week isn't complete, so I wanted to go over something that didn't end up on github but was still a learning moment for me.

We're doing a lot of work around campaign finance in the Chicago mayoral election, and this week I wanted to quickly check if a list any of a list of names shows up in the records. In the past I've sometimes gone with the incredibly long sql where statement for something like this, but we were comparing a number of different lists with dozens of names, so hand-coding the query wasn't going to work.

I needed to scrape some of the data, and in the process of writing to a csv I realized I could just as easily send that info directly to an sql query. I was writing the scraper in python and the database itself is postgres, so I was able to easily add a call to [psycopg2](http://initd.org/psycopg/) for each time the scraper found a matching element. (note: The project isn't out yet so these are just example queries, but I'll try and post a link to the project and full code next week)

{% highlight python %}
from bs4 import BeautifulSoup
import urllib2
import psycopg2
import probablepeople
import csv
import re

data = []

conn = psycopg2.connect("dbname=electionmoney user=chris")
cur = conn.cursor()

def scrape():
    soup = BeautifulSoup(open("scrape.html"))
    table_body = soup.find('tbody')
    rows = table_body.find_all('tr',class_='data')
    cur = conn.cursor()

    for row in rows:
        td = row.find_all('td')
        state = td[6].string.split(',')[-1]
        peep = probablepeople.tag(td[2].string)[0]
        lastname = peep['Surname']
        cur.execute("""SELECT * FROM receipts where lower(trim("LastOnlyName"))=lower(trim(%s)) AND lower(trim("State"))=lower(trim(%s))""", (lastname,state))
        results = cur.fetchall()
        cur.close

        for item in results:
            if item not in data:
                data.append(item)

{% endhighlight %}

I reused that same format with a csv list of companies by replacing the beautiful soup code with ```with open('companies.csv', 'rb') as csvfile:``` and iterating on the rows.

The biggest issue I had was working with another query that required a LIKE comparison with a python variable. Since postgres uses '%' for wildcards and python uses '%' for variables, the psycopg2 query got confused about what exactly I meant. After some hunting, I found that creating the query itself as a variable and then passing that to psycopg2 worked.

{% highlight python %}
query = "".join(('%',company,'%'))
cur.execute("""SELECT * FROM receipts where lower(trim("Employer")) LIKE lower(trim(%s))""", (query,))
{% endhighlight %}

This made re-querying the data much easier and as an added bonus makes the entire trail reproducible and able to be put under version control. Earlier this month I was lucky enough to go to [NICAR](https://www.ire.org/nicar/), IRE's computer-assisted reporting (i.e, journo-nerd) conference, and one of my main goals coming out is to [have a better process for data projects](https://docs.google.com/presentation/d/18KE-VO9T6V1I_aGyekdDtFhYP4K0Saph7aBuBS3N8tc/edit#slide=id.p). I feel like this is another step in that direction.

##This week
Again, a lot of items I talked about last week are still on this week's to-do list

* I need to write up my formal goals list for this project
* Continue to add features to the blog (archives, comments, etc ...)
* Write up my process for actually creating the blog in more depth
* Write up the process for the campaign finance tracker
* Finish and writeup the smartsheet calendar project