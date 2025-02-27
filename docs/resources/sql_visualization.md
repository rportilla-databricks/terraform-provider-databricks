---
subcategory: "Databricks SQL"
---
# databricks_sql_visualization Resource

To manage [SQLA resources](https://docs.databricks.com/sql/get-started/concepts.html) you must have `databricks_sql_access` on your [databricks_group](group.md#databricks_sql_access) or [databricks_user](user.md#databricks_sql_access).

**Note:** documentation for this resource is a work in progress.

A visualization is always tied to a [query](sql_query.md). Every query may have one or more visualizations.

## Example Usage

```hcl
resource "databricks_sql_visualization" "q1v1" {
  query_id    = databricks_sql_query.q1.id
  type        = "table"
  name        = "My Table"
  description = "Some Description"

  // The options encoded in this field are passed verbatim to the SQLA API.
  options = jsonencode(
    {
      "itemsPerPage" : 25,
      "columns" : [
        {
          "name" : "p1",
          "type" : "string"
          "title" : "Parameter 1",
          "displayAs" : "string",
        },
        {
          "name" : "p2",
          "type" : "string"
          "title" : "Parameter 2",
          "displayAs" : "link",
          "highlightLinks" : true,
        }
      ]
    }
  )
}
```

## Related Resources

The following resources are often used in the same context:

* [End to end workspace management](../guides/workspace-management.md) guide.
* [databricks_sql_dashboard](sql_dashboard.md) to manage Databricks SQL [Dashboards](https://docs.databricks.com/sql/user/dashboards/index.html).
* [databricks_sql_endpoint](sql_endpoint.md) to manage Databricks SQL [Endpoints](https://docs.databricks.com/sql/admin/sql-endpoints.html).
* [databricks_sql_global_config](sql_global_config.md) to configure the security policy, [databricks_instance_profile](instance_profile.md), and [data access properties](https://docs.databricks.com/sql/admin/data-access-configuration.html) for all [databricks_sql_endpoint](sql_endpoint.md) of workspace.
* [databricks_sql_permissions](sql_permissions.md) to manage data object access control lists in Databricks workspaces for things like tables, views, databases, and [more](https://docs.databricks.com/security/access-control/table-acls/object-privileges.html).
