# JSON-Azure-Policies


{
  "properties": {
    "displayName": "Deny NSG Rule changes that allow common Ports From Any or Internet",
    "policyType": "Custom",
    "mode": "All",
    "description": "Deny NSG Rule changes that allow common Ports From Any or Internet",
    "metadata": {
    },
    "parameters": {},
    "policyRule": {
      "if": {
            "allOf": [
              {
                "field": "type",
                "equals": "Microsoft.Network/networkSecurityGroups/securityRules"
              },
              {
                "anyOf": [
                	{
	                  "field": "Microsoft.Network/networkSecurityGroups/securityRules[*].sourcePortRange",
					"equals": "*"
					},
					{
					"field": "Microsoft.Network/networkSecurityGroups/securityRules[*].sourceAddressPrefix",
					"equals": "Internet"
					},
       	        ]
              },
              {
                "field": "Microsoft.Network/networkSecurityGroups/securityRules/access",
                "equals": "Allow"
              },
	      {
		"field": "Microsoft.Network/networkSecurityGroups/securityRules/direction",
		"equals": "Inbound"
	      },
              {
                "anyOf": [
						  {
                            "field": "Microsoft.Network/networkSecurityGroups/securityRules[*].destinationPortRange",
                            "equals": "21"
                          },
						  {
                            "field": "Microsoft.Network/networkSecurityGroups/securityRules[*].destinationPortRange",
                            "equals": "22"
                          },
						  {
                            "field": "Microsoft.Network/networkSecurityGroups/securityRules[*].destinationPortRange",
                            "equals": "23"
                          },
                          {
                            "field": "Microsoft.Network/networkSecurityGroups/securityRules[*].destinationPortRange",
                            "equals": "80"
                          },
						  {
                            "field": "Microsoft.Network/networkSecurityGroups/securityRules[*].destinationPortRange",
                            "equals": "443"
                          },
						  {
                            "field": "Microsoft.Network/networkSecurityGroups/securityRules[*].destinationPortRange",
                            "equals": "3389"
                          }
                ]
              }
            ]
      },
      "then": {
        "effect": "deny"
      }
    }
  },

  }
