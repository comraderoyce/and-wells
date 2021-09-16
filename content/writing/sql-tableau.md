+++
math = false 
meta = false
toc = false
author = "Royce"
title = "SQL basics for Tableau and Redshift"
date = "2021-09-15"
category = "notes"
description = "Notes on working with SQL and Tableau"

+++

There is something about not reading a manual or taking a walk through the basic documentation when learning a piece of software that is rewarding yet very painful. 
True to form, I jumped into creating a Tableau dashboard without much prior knowledge of Tableau or SQL. Here are some things I wish I would have known when starting the work.

<!--more-->


I have been speedrunning learning Tableau and SQL for a work project. The brief is to create a dashboard that shows the reach and type of customer interactions with a regional suite of websites. There were a bunch of tables for each channel (email, sales calls, website visits, etc.) along with some cross-table user information like their ID. Further, there were tables with 

# SQL Super Basics

The first thing to note is to use a data extract instead of a live connection. That would have saved me a ton of time{{% marginnote %}}Think lots of queries because no SQL Workbench, times the query optimization of an sql noob, compounded by the live connection rerunning the query for every change.{{% /marginnote %}} waiting for queries to run.

```sql
"this is a row"
this is a cell value'
-- this is a comment
```

The row vs column thing is an important distinction and has caught me up many times already.

Some other basics: 

- `UNION` needs to be run on tables that have the same number of columns.
- `FULL OUTER JOIN` will return multiple columns of the key used to match on.
- With `SELECT` statements, you can assign a table alias by putting a key in after the relevant `SELECT`:

    For example, the following would let you then call the table with the alias `t1`.

    ```sql
    SELECT a.date, a.id, a.interactions
    FROM your_table_with_a_very_long a
    ```
- Use `SELECT DISTINCT` instead of `SELECT` to return fewer rows if you only need the unique values from a table.

Working with dates is a bit complicated but here is a useful tricks: 

```sql
-- this gets you a formatted basic day
CAST(login_date AS date) as "login date"
```

# Composing

We wanted to create a dashboard that would represent the most important metrics for acquisition and user retention. There were multiple channels for both phases. But the main structure of the dashboard was to represent these metrics by their magnitude over time. 

So it helped to think about the final data structure that I wanted for the dashboard, and then write the query around that. 

To represent the metrics as a bar chart with the date on the x-axis, the main table would have dates as their anchor. From there, the individual actions would be grouped by the user's unique ID. Their individual interactions would then be listed out. I started by trying to make a table where there was a row for each day and a unique ID, with a column per interaction type. 

The first round query came back with a table structured like this: 

| date        | id          | emails    | calls        |
| ----------- | ----------- | -         | ----         |
| 1/1/21      | u1          | 0         | 1            |
| 1/1/21      | u2          | 1         | 0            |

This proved to be an issue. I was generating the main table by getting a list of users from one of the interactions, and then the `LEFT JOIN` would leave out users that were not in this list. This meant that if users had a phone call, but no email, they wouldn't be added in the `JOIN`. There was likely a way to fix this by using `JOIN` better, but I ended up giving up on making that work. Instead, I set the interaction type as a column, summed the interactions per type per date, and then combined them with `UNION ALL` into a total interactions table.

The final setup:

| date        | id          | type      | interactions |
| ----------- | ----------- | -         | ----         |
| 1/1/21      | u1          | call      | 1            |
| 1/1/21      | u2          | email     | 1            |


With each interaction row, I wanted to include some additional user metadata like 

From there I was able to append the metadata without issue using `LEFT JOIN` against the full list of interactions. {{% marginnote %}}This probably isn't ideal from a SQL performance or table length perspective.{{% /marginnote %}}

# Transforming Data

`CASE` statements were useful for transforming some data into human-readable formats or the correct categories that I wanted in the dashboard labels.

In this case, there was some user category metadata that was stored as different hex strings. `CASE` lets me if/then the table values to get a final value I wanted.

I could have accomplished this particular transform on the Tableau side using aliases, but `CASE` can handle more complicated logic. 

One thing to know about `CASE` is that it will evaluate with the first match, then ignore any other logic that follows.

Calculated fields will let you set exact names for metrics derived from the underlying data. For example, I wanted to do a running count calculation. This was easy enough, but then the resulting data takes on strange names in labels and tooltips. You can then copy over the calculation from the "shelf" and then creating a new calculated field with the name you want. 

# Using Joins

You can use a `JOIN` in conjunction with a `SELECT` statement to replace a column for your table. For example, I had some user interaction information in one table, assigned to their website ID. However, this ID is different from the global ID that I was using from other interactions. 

The following solved this by using `SELECT` on the `JOIN` table. This wasn't super intuitive to me, but it sort of runs backward, as the table created by the `JOIN` is what is being picked through with the `SELECT` statement. Essentially you create the full table structure and then choose out pieces with the `SELECT` statement. {{% marginnote %}}A bit weird for me since `SELECT` comes first{{% /marginnote %}}


```sql
SELECT
    CAST(login_date AS date) as "login date",
    u.global_id as "id",
    'login' as "interaction type",
    COUNT(u.global_id) as "interactions"
FROM table_1 l
JOIN table_2 u ON l.userid=u.id
WHERE "status" = 'Success'
GROUP BY 1, 2, 3
```

# Tableau Notes

Once the basic data is in a good place with a reasonable query, some other useful features of Tableau let you further manipulate things in the way you might want. 

- Aliases, as the name suggests, let you replace values in the underlying data with a defined alias of your choice. Useful for simplifying complicated data. 
- You can rename columns in the left-hand data sidebar, letting you get simple names without having to rewrite your data query. 
- Calculated fields are useful to derive additional data from the underlying data in your query. It also is the way I was able to set specific names to things like cumulative counts that are generated by Tableau but show up oddly in tooltips and labels. 
- Calculated fields can return True/False values as well as typical calculations like sums or averages. 
- Sets let you determine in/out classifications for data. 
- By combining sets with calculated fields, I was able to create a combined field for segmenting the user base based on their interactions. For example, if users had interactions of multiple types, they were in multiple sets and the calculated field would allow comparisons for the True/False values to assign them a segment accordingly.

# Optimizations

Tooling is important. Things would have likely proceeded much faster if I had access to SQL Workbench to properly explore the data objects. As it were, the virtual machine I was using refused to run SQL Workbench so I was stuck with writing queries in VS Code and testing them by running the query through Tableau. Not ideal. Not made any better by the fact that I didn't know how to use a data extract and was instead using Live queries.

It took a bit to get set up to start the work. The first step was getting access to a virtual workstation. Then getting correct permissions to the Redshift data lake. Then getting a Tableau license and install permissions on the virtual workspace. Then getting the connector to Tableau working with the particularly finicky settings of the Redshift instance. A few weeks later, I was able to access the data objects within Tableau and start creating a workbook. Making this more turn-key would have likely saved about $50,000 in working time between client and contractor billable hours. This is particularly painful when the blocks boil down to simple things providing database permissions and paying for licenses. If there isn't a study on the amount of time and money wasted on such things, there really should be. It would be eye-opening and likely it is in the _very large numbers_ as these things just pile up over time and across projects. 

