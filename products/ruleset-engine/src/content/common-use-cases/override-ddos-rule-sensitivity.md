---
pcx-content-type: configuration
alwaysopen: true
order: 775
---

# Adjust the sensitivity of a specific HTTP DDoS rule to Low

Follow the steps below to override the sensitivity of a specific rule of the Cloudflare HTTP DDoS Managed Ruleset.

1. [Add a rule](/basic-operations/deploy-rulesets) to a phase to deploy the Cloudflare HTTP DDoS Managed Ruleset. You only need to deploy this specific ruleset when you wish to define one or more overrides, since it is enabled by default.
1. [Configure a rule override](/managed-rulesets/override-managed-ruleset) that sets the `sensitivity_level` of a specific rule.

The example below uses the [Update ruleset](/rulesets-api/update) operation to execute the steps in a single `PUT` request.

* Add a rule to the ruleset of the `ddos_l7` phase that applies the Cloudflare HTTP DDoS Managed Ruleset (with ID `<HTTP_DDOS_RULESET_ID>`).
* Create an override for the rule with ID `<RULE_ID>` and set the rule sensitivity to `low`. All other rules use the default sensitivity defined by Cloudflare.

<details>
<summary>Example: Use an override to set the sensitivity of an HTTP DDoS rule at the zone level</summary>
<div>

```json
curl -X PUT \
"https://api.cloudflare.com/client/v4/zones/<ZONE_ID>/rulesets/phases/ddos_l7/entrypoint" \
-H "Authorization: Bearer <API_TOKEN>" \
-d '{
  "rules": [
    {
      "action": "execute",
      "expression": "true",
      "action_parameters": {
        "id": "<HTTP_DDOS_RULESET_ID>",
        "overrides": {
          "rules": [
            {
              "id": "<RULE_ID>",
              "sensitivity_level": "low"
            }
          ]
        }
      }
    }
  ]
}'
```

</div>
</details>
