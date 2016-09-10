# Common Table Expression

```sql
WITH topclients AS
(
SELECT
rank() OVER(PARTITION BY c.region ORDER BY SUM(contract_value) DESC) AS Position,
c.contact_id, c.first_name, c.region, SUM(contract_value) AS Sales FROM contacts c
INNER JOIN contracts co
ON c.contact_id = co.contract_client
GROUP BY c.contact_id, c.first_name, c.region
)
SELECT * FROM topclients WHERE Position = 1
```

> Just make sure I have the joins correct...
> Then I need to bring out the data I am interested in

## Recursive Queries

Self referencing/join is a form of recursion.