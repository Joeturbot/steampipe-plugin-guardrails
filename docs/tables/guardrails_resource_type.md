# Table: guardrails_resource_type

List all the cloud resource types known to Turbot Guardrails.

## Examples

### List all resource types

```sql
select
  id,
  uri,
  trunk_title
from
  guardrails_resource_type
order by
  trunk_title;
```

### List all resource types for AWS S3

```sql
select
  id,
  uri,
  trunk_title
from
  guardrails_resource_type
where
  mod_uri like 'tmod:@turbot/aws-s3%'
order by
  trunk_title;
```

### Count resource types by cloud provider

```sql
select
  sum(case when mod_uri like 'tmod:@turbot/aws-%' then 1 else 0 end) as aws,
  sum(case when mod_uri like 'tmod:@turbot/azure-%' then 1 else 0 end) as azure,
  sum(case when mod_uri like 'tmod:@turbot/gcp-%' then 1 else 0 end) as gcp,
  count(*) as total
from
  guardrails_resource_type;
```
