# Joins

* [Data denormalization is broken](https://hackernoon.com/data-denormalization-is-broken-7b697352f405#.cdc1qnzif)

## Joins vs Subquery

Some joins can be rewritten as subquery.

```sql
SELECT job_id, title, location FROM jobs a
INNER JOIN jobs b
ON a.job_id = b.job_id
GROUP BY job_id, title, location

-- Can be rewritten as subquery

SELECT * from jobs
WHERE job_id IN (SELECT job_id FROM jobs)
```

```sql
SELECT contract_id, contract_value FROM contracts c
INNER JOIN payments p
ON c.contract_id = p.payment_contract_id
GROUP BY contract_id, contract_value

-- Can be more efficiently written as subquery

SELECT * FROM contracts
WHERE contract_id IN (SELECT payment_contract_id FROM payments)
```