---
updatedAt: 2026-05-27T21:25:32.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# List expense categories for the authenticated employee

Returns the flat list of expense categories applicable to the current employee. Only active categories are returned, filtered by the employee's country / legal-entity visibility rules. Leaf nodes have `is_selectable: true`; parent nodes are excluded unless `include_parents=true`.

## Authentication

This endpoint requires the following token type:

- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage expenses (`employment_payments`) | View expenses (`expense:read`) | Manage expenses (`expense:write`) |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "NotFoundResponse": {
        "description": "Returned when the requested resource does not exist or is not accessible with the current authentication credentials.",
        "example": {
          "message": "{resource} not found"
        },
        "properties": {
          "message": {
            "description": "A message indicating which resource was not found.",
            "pattern": "Not Found",
            "type": "string"
          }
        },
        "title": "NotFoundResponse",
        "type": "object"
      },
      "ExpenseCategoryNode": {
        "description": "A single expense category in the flat list structure",
        "example": {
          "code": "travel.flights",
          "description": "Flight expenses for business travel",
          "instructions": "Please include flight confirmation number",
          "is_selectable": true,
          "parent": {
            "code": "travel",
            "slug": "travel-abc123",
            "title": "Travel"
          },
          "prompt": "What was the purpose of this flight?",
          "scope": "global",
          "slug": "travel-flights-abc123",
          "status": "active",
          "title": "Flights"
        },
        "properties": {
          "code": {
            "description": "Category code (e.g., 'travel.flights')",
            "type": "string"
          },
          "description": {
            "description": "Category description",
            "nullable": true,
            "type": "string"
          },
          "instructions": {
            "description": "Instructions for using this category",
            "nullable": true,
            "type": "string"
          },
          "is_selectable": {
            "description": "Whether this category can be selected",
            "type": "boolean"
          },
          "parent": {
            "description": "Parent category information if this is a child category",
            "nullable": true,
            "properties": {
              "code": {
                "description": "Parent category code",
                "type": "string"
              },
              "slug": {
                "description": "Parent category slug",
                "type": "string"
              },
              "title": {
                "description": "Parent category title",
                "type": "string"
              }
            },
            "type": "object"
          },
          "prompt": {
            "description": "Prompt for user guidance",
            "nullable": true,
            "type": "string"
          },
          "scope": {
            "description": "Category scope (global, country, company, legal_entity)",
            "type": "string"
          },
          "slug": {
            "description": "Unique identifier for the category",
            "type": "string"
          },
          "status": {
            "description": "Category status (active, inactive)",
            "type": "string"
          },
          "title": {
            "description": "Human-readable category name",
            "type": "string"
          }
        },
        "title": "ExpenseCategoryNode",
        "type": "object"
      },
      "UnauthorizedResponse": {
        "description": "Returned when the request does not include valid authentication credentials. Ensure you are passing a valid OAuth2 access token or API token in the Authorization header.",
        "example": {
          "message": "Unauthorized"
        },
        "properties": {
          "message": {
            "pattern": "Unauthorized",
            "type": "string"
          }
        },
        "required": [
          "message"
        ],
        "title": "UnauthorizedResponse",
        "type": "object"
      },
      "ListExpenseCategoriesResponse": {
        "description": "Response containing a flat list of expense categories. Parent categories have is_selectable: false, while leaf categories have is_selectable: true. Child categories include parent_slug information.",
        "example": {
          "data": [
            {
              "code": "travel",
              "description": "Travel-related expenses",
              "instructions": null,
              "is_selectable": false,
              "parent": null,
              "prompt": null,
              "scope": "global",
              "slug": "travel-abc123",
              "status": "active",
              "title": "Travel"
            },
            {
              "code": "travel.flights",
              "description": "Flight expenses for business travel",
              "instructions": "Please include flight confirmation number",
              "is_selectable": true,
              "parent": {
                "code": "travel",
                "slug": "travel-abc123",
                "title": "Travel"
              },
              "prompt": "What was the purpose of this flight?",
              "scope": "global",
              "slug": "travel-flights-abc123",
              "status": "active",
              "title": "Flights"
            }
          ]
        },
        "properties": {
          "data": {
            "items": {
              "$ref": "#/components/schemas/ExpenseCategoryNode"
            },
            "type": "array"
          }
        },
        "title": "ListExpenseCategoriesResponse",
        "type": "object"
      },
      "ForbiddenResponse": {
        "description": "Returned when the authenticated user or token does not have permission to perform the requested action. Check that the token has the required OAuth2 scopes and that the user has the necessary role.",
        "example": {
          "message": "Forbidden"
        },
        "properties": {
          "message": {
            "pattern": "Forbidden",
            "type": "string"
          }
        },
        "required": [
          "message"
        ],
        "title": "ForbiddenResponse",
        "type": "object"
      }
    },
    "securitySchemes": {
      "OAuth2": {
        "description": "Authenticate using OAuth 2.0 protocol.\n",
        "flows": {
          "authorizationCode": {
            "authorizationUrl": "/auth/oauth2/authorize",
            "scopes": {
              "company_department:read": "company_department:read",
              "webhook:write": "webhook:write",
              "magic_link:write": "magic_link:write",
              "offboarding:write": "offboarding:write",
              "custom_field:write": "custom_field:write",
              "address:write": "address:write",
              "expense:read": "expense:read",
              "employment:write": "employment:write",
              "identity_verification:write": "identity_verification:write",
              "timesheet:write": "timesheet:write",
              "travel_letter:write": "travel_letter:write",
              "incentive:read": "incentive:read",
              "personal_detail:read": "personal_detail:read",
              "invoices:write": "invoices:write",
              "work_authorization:write": "work_authorization:write",
              "timeoff:write": "timeoff:write",
              "company_structure:read": "company_structure:read",
              "benefit_renewal:write": "benefit_renewal:write",
              "benefit_offer:read": "benefit_offer:read",
              "employment_documents": "employment_documents",
              "onboarding:write": "onboarding:write",
              "payroll_run:read": "payroll_run:read",
              "risk_reserve:write": "risk_reserve:write",
              "invoices": "invoices",
              "resignation_letter:read": "resignation_letter:read",
              "resignation:read": "resignation:read",
              "convert_currency:read": "convert_currency:read",
              "employments": "employments",
              "probation_document:read": "probation_document:read",
              "company_admin": "company_admin",
              "payroll": "payroll",
              "help_center_article:read": "help_center_article:read",
              "timesheet:read": "timesheet:read",
              "custom_field_value:write": "custom_field_value:write",
              "company_currencies:read": "company_currencies:read",
              "payslip:read": "payslip:read",
              "pay_item:write": "pay_item:write",
              "resignation:write": "resignation:write",
              "custom_field:read": "custom_field:read",
              "payroll_calendar:read": "payroll_calendar:read",
              "contract_amendment:write": "contract_amendment:write",
              "offboarding:read": "offboarding:read",
              "timeoff:read": "timeoff:read",
              "probation_document:write": "probation_document:write",
              "country:read": "country:read",
              "webhook:read": "webhook:read",
              "company_department:write": "company_department:write",
              "company_manager:read": "company_manager:read",
              "pay_item:read": "pay_item:read",
              "contract_amendment:read": "contract_amendment:read",
              "company:read": "company:read",
              "sso_configuration:write": "sso_configuration:write",
              "benefit_offer:write": "benefit_offer:write",
              "contract_eligibility:write": "contract_eligibility:write",
              "benefit_renewal:read": "benefit_renewal:read",
              "background_check:read": "background_check:read",
              "custom_field_value:read": "custom_field_value:read",
              "expense:write": "expense:write",
              "identity_verification:read": "identity_verification:read",
              "address:read": "address:read",
              "document:write": "document:write",
              "time_and_attendance": "time_and_attendance",
              "employment_payments": "employment_payments",
              "form:read": "form:read",
              "work_authorization:read": "work_authorization:read",
              "invoices:read": "invoices:read",
              "incentive:write": "incentive:write",
              "employment:read": "employment:read",
              "contract:read": "contract:read",
              "company_manager:write": "company_manager:write",
              "travel_letter:read": "travel_letter:read",
              "document:read": "document:read",
              "sso_configuration:read": "sso_configuration:read"
            },
            "tokenUrl": "/auth/oauth2/token"
          },
          "clientCredentials": {
            "scopes": {
              "company:read": "company:read",
              "company:write": "company:write",
              "company_admin": "company_admin",
              "company_management": "company_management",
              "convert_currency:read": "convert_currency:read",
              "country:read": "country:read",
              "employment_documents": "employment_documents",
              "employment_payments": "employment_payments",
              "employments": "employments",
              "help_center_article:read": "help_center_article:read",
              "invoices": "invoices",
              "payroll": "payroll",
              "payroll_calendar:read": "payroll_calendar:read",
              "pricing_plan:read": "pricing_plan:read",
              "pricing_plan:write": "pricing_plan:write",
              "time_and_attendance": "time_and_attendance",
              "webhook:read": "webhook:read",
              "webhook:write": "webhook:write"
            },
            "tokenUrl": "/auth/oauth2/token"
          }
        },
        "type": "oauth2"
      },
      "OAuth2Assertion": {
        "description": "Authenticate as the employee using the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant in the OAuth2 protocol.\n",
        "flows": {
          "clientCredentials": {
            "scopes": {
              "address:read": "address:read",
              "address:write": "address:write",
              "bank_account:read": "bank_account:read",
              "bank_account:write": "bank_account:write",
              "document:read": "document:read",
              "document:write": "document:write",
              "emergency_contact:read": "emergency_contact:read",
              "emergency_contact:write": "emergency_contact:write",
              "employment_documents": "employment_documents",
              "employment_payments": "employment_payments",
              "employments": "employments",
              "expense:read": "expense:read",
              "incentive:read": "incentive:read",
              "payroll": "payroll",
              "payslip:read": "payslip:read",
              "personal_detail:read": "personal_detail:read",
              "personal_detail:write": "personal_detail:write",
              "time_and_attendance": "time_and_attendance",
              "timeoff:read": "timeoff:read",
              "timeoff:write": "timeoff:write",
              "timesheet:read": "timesheet:read"
            },
            "tokenUrl": "/auth/oauth2/token",
            "x-assertionType": "urn:ietf:params:oauth:client-assertion-type:jwt-bearer"
          }
        },
        "type": "oauth2"
      }
    }
  },
  "info": {
    "title": "Employee Actions",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/employee/expense-categories": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "Returns the flat list of expense categories applicable to the current employee. Only active categories are returned, filtered by the employee's country / legal-entity visibility rules. Leaf nodes have `is_selectable: true`; parent nodes are excluded unless `include_parents=true`.\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage expenses (`employment_payments`) | View expenses (`expense:read`) | Manage expenses (`expense:write`) |",
        "operationId": "get_v1_employee_expense-categories",
        "parameters": [
          {
            "description": "Include parent (non-selectable) categories in addition to selectable leaves",
            "in": "query",
            "name": "include_parents",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "description": "Expense ID (slug) whose category should be included in the result, even if it is not selectable by default",
            "in": "query",
            "name": "expense_id",
            "required": false,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ListExpenseCategoriesResponse"
                }
              }
            },
            "description": "Success"
          },
          "401": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/UnauthorizedResponse"
                }
              }
            },
            "description": "Unauthorized"
          },
          "403": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ForbiddenResponse"
                }
              }
            },
            "description": "Forbidden"
          },
          "404": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/NotFoundResponse"
                }
              }
            },
            "description": "Not Found"
          }
        },
        "security": [
          {
            "OAuth2Assertion": [
              "https://gateway.remote.com/employment.manage",
              "expense:read",
              "expense:write",
              "employment_payments",
              "all:write",
              "all:read"
            ]
          }
        ],
        "summary": "List expense categories for the authenticated employee",
        "tags": [
          "Expenses"
        ]
      }
    }
  },
  "security": [
    {
      "OAuth2": []
    }
  ],
  "servers": [
    {
      "url": "https://gateway.remote.com/",
      "variables": {}
    },
    {
      "url": "https://gateway.remote-sandbox.com/",
      "variables": {}
    }
  ]
}
```