# Subquery

## Find Duplicated Records

```sql
-- First, list all the duplicated records
SELECT * FROM contacts
WHERE first_name+last_name IN (
  SELECT first_name+last_name FROM contacts
  GROUP BY first_name+last_name
  HAVING COUNT(*) > 1
)

-- Find the duplicated one

SELECT * FROM contacts A
WHERE EXISTS (
  SELECT B.contact_id FROM contacts B
  WHERE B.first_name = A.first_name
  AND B.last_name = A.last_name
  AND B.contact_id < A.contract_id
)
```