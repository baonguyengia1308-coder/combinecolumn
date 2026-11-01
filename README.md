# 175. Combine Two Tables (Easy)

## Problem Description

Write a solution to report the first name, last name, city, and state of each person in the `Person` table. If the address of a `personId` is not in the `Address` table, report `null` instead.

Return the result table in **any order**.

---

### Table Schema

#### Table: `Person`
| Column Name | Type |
| :--- | :--- |
| personId | int |
| firstName | varchar |
| lastName | varchar |

* `personId` is the primary key (column with unique values) for this table.
* This table contains ID, first name, and last name of each person.

#### Table: `Address`
| Column Name | Type |
| :--- | :--- |
| addressId | int |
| personId | int |
| city | varchar |
| state | varchar |

* `addressId` is the primary key (column with unique values) for this table.
* Each row of this table contains an ID of a city and state, mapped to a `personId`.

---

### Examples

#### Example 1:

**Input:**

**Table `Person`:**
| personId | lastName | firstName |
| :--- | :--- | :--- |
| 1 | Wang | Allen |
| 2 | Alice | Bob |

**Table `Address`:**
| addressId | personId | city | state |
| :--- | :--- | :--- | :--- |
| 1 | 2 | New York City | New York |
| 2 | 3 | Leetcode | California |

**Output:**
| firstName | lastName | city | state |
| :--- | :--- | :--- | :--- |
| Allen | Wang | Null | Null |
| Bob | Alice | New York City | New York |

**Explanation:** 
* `personId = 1` has no address in the `Address` table, so the city and state are returned as `null`.
* `personId = 2` has an address in the `Address` table, so the city and state are mapped accordingly.

---

## Solution (SQL)

```sql
SELECT 
    p.firstName, 
    p.lastName, 
    a.city, 
    a.state 
FROM 
    Person p 
LEFT JOIN 
    Address a 
ON 
    p.personId = a.personId;
