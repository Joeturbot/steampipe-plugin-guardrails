# Table: guardrails_tag

Tags is a unified collection of all tags discovered by Turbot Guardrails across all
resources in all clouds.

It is recommended that queries to this table should include (usually in the `where` clause) at least one
of these columns: `id`, `key`, `value` or `filter`.

## Examples

### List all tags

```sql
select
  *
from
  guardrails_tag
order by
  key,
  value;
```

### Find all resources for the Sales department

```sql
select
  key,
  value,
  resource_ids
from
  guardrails_tag
where
  key = 'Department'
  and value = 'Sales';
```

### Find departments with the most tagged resources

```sql
select
  key,
  value,
  jsonb_array_length(resource_ids) as count
from
  guardrails_tag
where
  key = 'Department'
order by
  count desc;
```

### List tags without values

```sql
select
  *
from
  guardrails_tag
where
  value is null or trim(value) = '';
```
