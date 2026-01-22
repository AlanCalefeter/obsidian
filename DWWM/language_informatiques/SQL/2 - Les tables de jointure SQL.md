
### INNER JOIN

```sql
SELECT *
FROM A
INNER JOIN B ON A.key = B.key
```

### LEFT JOIN

```sql
SELECT *
FROM A
LEFT JOIN B ON A.key = B.key
```

### LEFT JOIN (sans l’intersection de B)

```sql
SELECT *
FROM A
LEFT JOIN B ON A.key = B.key
WHERE B.key IS NULL

```
### RIGHT JOIN

```sql
SELECT *
FROM A
RIGHT JOIN B ON A.key = B.key
```

### RIGHT JOIN (sans l’intersection de A)

```sql
SELECT *
FROM A
RIGHT JOIN B ON A.key = B.key
WHERE B.key IS NULL
```

### FULL JOIN

```sql
SELECT *
FROM A
FULL JOIN B ON A.key = B.key
```

### FULL JOIN (sans intersection)

```sql
SELECT *
FROM A
FULL JOIN B ON A.key = B.key
WHERE A.key IS NULL
OR B.key IS NULL
```


![[sql-join-infographie.png]]
