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
