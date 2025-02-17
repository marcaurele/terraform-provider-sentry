---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "sentry_issue_alert Data Source - terraform-provider-sentry"
subcategory: ""
description: |-
  Sentry Issue Alert data source. See the Sentry documentation https://docs.sentry.io/api/alerts/retrieve-an-issue-alert-rule-for-a-project/ for more information.
---

# sentry_issue_alert (Data Source)

Sentry Issue Alert data source. See the [Sentry documentation](https://docs.sentry.io/api/alerts/retrieve-an-issue-alert-rule-for-a-project/) for more information.

## Example Usage

```terraform
# Retrieve an Issue Alert
# URL format: https://sentry.io/organizations/[organization]/alerts/rules/[project]/[internal_id]/details/
data "sentry_issue_alert" "original" {
  organization = "my-organization"
  project      = "my-project"
  internal_id  = "42"
}

# Create a copy of an Issue Alert
resource "sentry_issue_alert" "copy" {
  organization = data.sentry_issue_alert.original.organization
  project      = data.sentry_issue_alert.original.project

  # Copy and modify attributes as necessary.

  name = "${data.sentry_issue_alert.original.name}-copy"

  action_match = data.sentry_issue_alert.original.action_match
  filter_match = data.sentry_issue_alert.original.filter_match
  frequency    = data.sentry_issue_alert.original.frequency

  conditions = data.sentry_issue_alert.original.conditions
  filters    = data.sentry_issue_alert.original.filters
  actions    = data.sentry_issue_alert.original.actions
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `id` (String) The ID of this resource.
- `organization` (String) The organization the resource belongs to.
- `project` (String) The project the resource belongs to.

### Read-Only

- `action_match` (String) Trigger actions when an event is captured by Sentry and `any` or `all` of the specified conditions happen.
- `actions` (String) List of actions. In JSON string format.
- `conditions` (String) List of conditions. In JSON string format.
- `environment` (String) Perform issue alert in a specific environment.
- `filter_match` (String) A string determining which filters need to be true before any actions take place. Required when a value is provided for `filters`.
- `filters` (String) A list of filters that determine if a rule fires after the necessary conditions have been met. In JSON string format.
- `frequency` (Number) Perform actions at most once every `X` minutes for this issue.
- `name` (String) The issue alert name.
- `owner` (String) The ID of the team or user that owns the rule.
