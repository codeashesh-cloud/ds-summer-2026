today i learned three chapter
i learn the select statement , from statements and and where

SQLBolt

Sql= structured Query language
it allows the users to query, manipulate and transform the data froma relational database. 
it is very simple and easy to use. 

#Relational Databse
it is the collection of related (two-dimensional) tables. 
each tables are similar to an Excel spreadhseet, with a fixed number of named columns ( attributes) and any number of the rows of data. 

#####  sql lesson 1: SELECT queries 101
to retrieve the data from a sql datbase, we need to write the select statements. ( queries)
# SELECT
for example
# SELECT column, column2 FROM mytable;
# SSELECT * FROM mytable;    # selects everything


#######################################################################################################################################################################################################################################

####  sql lesson 2: Queries with constraints (pt.1)

# SELECT column, column2 FROM mytable where condition and/or condition;

operator 
=, !=,<,>,<=,>=                                 they are the standard numerical operators
between ..... and.....          	            Number is within range of two values
not between ..... and.....                      uNmber is not within range of two values
IN .....                                        NUMBER EXISTS IN A LIST
NOT IN ...


#######################################################################################################################################################################################################################################

#### SQL Lesson 3: Queries with constraints (Pt. 2)
 when using the where clauses with columns containing strings, there are number of use to use them

 operator
 =                                             case sensitive exact string comparison                                                                                        eg. col_name='abc' 
 != or <>                                      case sensitive exact string inequality                                                                                         eg. col_name!='abc'
 LIKE                                          case insensetive exact string comparison                                                                                      eg. col_nmae like 'ABC'
 NOT LIKE                                      case insensetive exact string inequality comparison                                                                           eg col_name NOT LIKE 'ABCD'
 %                                             Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE)         col_name LIKE "%AT%"(matches 'AT', 'ATTIC', 'CAT' or even 'BATS')   
 _                                            Used anywhere in a string to match a single character                                                          col_name LIKE "AN_"(matches "AND", but not "AN")      

 ######################################################################################################################################################################################################################################


## SQL Lesson 4 — Filtering and Sorting Query Results

### 1. `DISTINCT` — remove duplicate rows

Use when query results have repeated values you don't want.

```sql
SELECT DISTINCT column1, column2
FROM mytable
WHERE condition;
```

⚠️ `DISTINCT` removes duplicates **across all selected columns combined**, not per column.
For column-specific deduplication → use `GROUP BY` (later lesson).

---

### 2. `ORDER BY` — sort the results

Sorts rows by a column, ascending or descending.

```sql
SELECT column1, column2
FROM mytable
WHERE condition
ORDER BY column1 ASC;   -- ascending (A→Z, 0→9)
```

```sql
ORDER BY column1 DESC;  -- descending (Z→A, 9→0)
```

- Default is `ASC` if you don't specify
- Sorts alphanumerically (numbers and text both work)

---

### 3. `LIMIT` and `OFFSET` — return only some rows

- `LIMIT n` → return at most `n` rows
- `OFFSET m` → skip the first `m` rows before counting

```sql
SELECT column1
FROM mytable
ORDER BY column1 ASC
LIMIT 5 OFFSET 10;
```

This skips the first 10 rows, then returns the next 5.

**Real-world use:** pagination on websites (Reddit, Pinterest, search results — page 1 = first 10, page 2 = next 10, etc.)

---

### Putting it all together — full query template

```sql
SELECT DISTINCT column1, column2
FROM mytable
WHERE condition
ORDER BY column1 DESC
LIMIT 5 OFFSET 10;
```

The clauses always go in this order:
**SELECT → FROM → WHERE → ORDER BY → LIMIT → OFFSET**

---

### Quick reference table

| Keyword     | What it does                              |
|-------------|-------------------------------------------|
| `DISTINCT`  | Removes duplicate rows                    |
| `ORDER BY`  | Sorts results by a column                 |
| `ASC`       | Ascending order (default)                 |
| `DESC`      | Descending order                          |
| `LIMIT n`   | Returns at most `n` rows                  |
| `OFFSET m`  | Skips first `m` rows                      |

---

### My understanding check
- [ ] I can write a query that returns only unique values from a column
- [ ] I can sort results in both directions
- [ ] I know what `LIMIT 5 OFFSET 10` returns (rows 11-15)
- [ ] I know the order clauses must appear in

Lesson 5 is just review 


######################################################################################################################################################################################################################################


## SQLBolt Lesson 6: INNER JOIN

### Why we need JOINs
- Real databases split data across multiple tables (normalization)
- Reduces duplicate data; lets each table grow independently
- Trade-off: queries get more complex, can be slower on big tables
- To answer questions that span tables, we need to combine them

### How tables connect
- Each table has a **primary key** — a column that uniquely identifies each row
- Often an auto-incrementing integer, but can be a string or hash
- Two tables "share information about an entity" by referencing the same key

### INNER JOIN syntax

    SELECT columns
    FROM table_a
    INNER JOIN table_b
        ON table_a.id = table_b.id
    WHERE ...
    ORDER BY ...
    LIMIT ...;

### What INNER JOIN does (in plain words)
- Looks at every row in table A and every row in table B
- Wherever the `ON` condition matches, it combines them into one wider row
- Rows that don't match in BOTH tables get dropped
- Result: only rows that exist in both tables

### Things to remember
- `JOIN` and `INNER JOIN` are the same thing — stick with `INNER JOIN` for clarity
- The `ON` clause is what tells SQL *how* to match the rows
- Always qualify column names when they exist in both tables: `movies.id` not just `id`
- `WHERE`, `ORDER BY`, `LIMIT` all still work the same — applied *after* the join


######################################################################################################################################################################################################################################


##  Lesson 7: OUTER JOINs

### Why we need them
- INNER JOIN only returns rows that have a match in BOTH tables
- If data is "asymmetric" (one table has rows the other doesn't), INNER JOIN drops them
- OUTER JOINs let us keep the unmatched rows instead

### The three OUTER JOINs

| Join type  | Keeps rows from         | Drops rows from                  |
|------------|-------------------------|----------------------------------|
| LEFT JOIN  | Left table (always)     | Unmatched rows from right        |
| RIGHT JOIN | Right table (always)    | Unmatched rows from left         |
| FULL JOIN  | Both tables (always)    | Nothing                          |

- "Left" = the table named first (after FROM)
- "Right" = the table named second (after JOIN)
- Unmatched rows get NULL in the columns from the other table

### Syntax (same as INNER JOIN, just swap the keyword)

    SELECT columns
    FROM table_a
    LEFT JOIN table_b
        ON table_a.id = table_b.a_id;

### Gotchas
- LEFT OUTER JOIN == LEFT JOIN (the "OUTER" is optional, kept from SQL-92)
- Same for RIGHT and FULL
- You'll get NULLs in results — need to handle them with WHERE or IS NULL (Lesson 8)
- SQLBolt's browser only supports LEFT JOIN in exercises, but the concepts apply to all three