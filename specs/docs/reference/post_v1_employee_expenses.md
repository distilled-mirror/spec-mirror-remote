---
updatedAt: 2026-05-27T21:25:32.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Create an expense for the authenticated employee

Creates a new expense record for the current employee.

## Authentication

This endpoint requires the following token type:

- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage expenses (`employment_payments`) | - | Manage expenses (`expense:write`) |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "Base64File": {
        "description": "All the params needed upload a base64 file.",
        "example": {
          "content": "UGVyaW9kIEVuZCBEYXRlLFBheSBEYXRlLEVtcG...5jZSBPZiBSZXNpZGVuYdXJyZW50LEFsbG93",
          "name": "receipt.pdf"
        },
        "properties": {
          "content": {
            "description": "The content in base64 encoding.",
            "format": "binary",
            "type": "string"
          },
          "name": {
            "description": "The file name.",
            "type": "string"
          }
        },
        "required": [
          "name",
          "content"
        ],
        "title": "Base64File",
        "type": "object"
      },
      "ActionError": {
        "properties": {
          "action": {
            "description": "The action that lead to the error message.",
            "type": "string"
          },
          "code": {
            "description": "An error code that describes the nature of the error.",
            "type": "string"
          },
          "message": {
            "description": "A developer friendly error message that gives details on what the error was and how it may be remedied.",
            "type": "string"
          }
        },
        "required": [
          "code",
          "message",
          "action"
        ],
        "title": "ActionError",
        "type": "object"
      },
      "Timezone": {
        "description": "[TZ identifier](https://www.iana.org/time-zones)",
        "example": "Etc/UTC",
        "title": "Timezone",
        "type": "string"
      },
      "UnprocessableEntityResponse": {
        "anyOf": [
          {
            "properties": {
              "errors": {
                "type": "object"
              }
            },
            "required": [
              "errors"
            ],
            "type": "object"
          },
          {
            "properties": {
              "message": {
                "oneOf": [
                  {
                    "type": "string"
                  },
                  {
                    "$ref": "#/components/schemas/ParameterError"
                  },
                  {
                    "items": {
                      "$ref": "#/components/schemas/ParameterError"
                    },
                    "title": "ParameterErrors",
                    "type": "array"
                  },
                  {
                    "$ref": "#/components/schemas/ActionError"
                  },
                  {
                    "items": {
                      "$ref": "#/components/schemas/ActionError"
                    },
                    "title": "ActionErrors",
                    "type": "array"
                  }
                ]
              }
            },
            "required": [
              "message"
            ],
            "type": "object"
          }
        ],
        "example": {
          "errors": {
            "some_field": [
              "is invalid"
            ]
          }
        },
        "title": "UnprocessableEntityResponse",
        "type": "object"
      },
      "ParamsToCreateEmployeeExpense": {
        "description": "  Params for creating an expense as the authenticated employee.\n\n  The employment is implied by the access token, so `employment_id` is not accepted.\n  `reviewer_id` and `reviewed_at` are also omitted — they only apply to manager-created expenses.\n\n  Category selection mirrors the company endpoint: use either `category` (legacy enum, deprecated but supported)\n  or `expense_category_slug` (recommended). When both are provided, `expense_category_slug` wins.\n",
        "example": {
          "amount": 8000,
          "currency": "EUR",
          "expense_category_slug": "uuid-tech-equipment-slug",
          "expense_date": "2020-12-11",
          "receipt": {
            "content": "UGVyaW9kIEVuZCBEYXRlLFBheSBEYXRlLEVtcG...5jZSBPZiBSZXNpZGVuYdXJyZW50LEFsbG93",
            "name": "receipt.pdf"
          },
          "tax_amount": 0,
          "timezone": "Etc/UTC",
          "title": "new keyboard"
        },
        "properties": {
          "amount": {
            "description": "The expense amount in the specified currency, in cents.",
            "type": "integer"
          },
          "category": {
            "deprecated": true,
            "description": "Categories allowed for an expense (legacy, deprecated).<br/>\nNote: `coworking`, `home_office`, `phone_utilities`, `travel` are deprecated and will be removed in the future.\n",
            "enum": [
              "car_rental",
              "coworking_office",
              "education_training",
              "entertainment",
              "flight",
              "fuel",
              "gifts",
              "insurance",
              "lodging",
              "meals",
              "other",
              "parking_toll",
              "subscription",
              "tech_equipment",
              "telecommunication",
              "transport",
              "utilities",
              "vaccination_testing",
              "visa",
              "wellness",
              "coworking",
              "home_office",
              "phone_utilities",
              "travel"
            ],
            "nullable": true,
            "type": "string"
          },
          "currency": {
            "description": "  The three-letter code for the expense currency.<br/>\n  Examples: `\"USD\"`, `\"EUR\"`, `\"CAD\"`\n",
            "type": "string"
          },
          "expense_category_slug": {
            "description": "Slug of the expense category from the hierarchical categories system (recommended). Takes precedence over legacy category field.",
            "nullable": true,
            "type": "string"
          },
          "expense_date": {
            "description": "Date of the purchase, which must be in the past",
            "type": "string"
          },
          "receipt": {
            "$ref": "#/components/schemas/Base64File"
          },
          "receipts": {
            "items": {
              "$ref": "#/components/schemas/Base64File"
            },
            "maxItems": 5,
            "type": "array"
          },
          "tax_amount": {
            "description": "The tax portion of the expense amount, in cents. Use 0 if no tax applies.",
            "type": "integer"
          },
          "timezone": {
            "$ref": "#/components/schemas/Timezone"
          },
          "title": {
            "description": "A short description of the expense (e.g., \"New keyboard\", \"Team dinner\").",
            "type": "string"
          }
        },
        "required": [
          "expense_date",
          "title",
          "amount",
          "currency"
        ],
        "title": "ParamsToCreateEmployeeExpense",
        "type": "object"
      },
      "SuccessResponse": {
        "description": "A generic success response returned by operations that don't produce a specific resource (e.g., updates, deletes).",
        "example": {
          "data": {
            "status": "ok"
          }
        },
        "properties": {
          "data": {
            "properties": {
              "status": {
                "description": "The result status. Always `\"ok\"` for successful operations.",
                "type": "string"
              }
            },
            "type": "object"
          }
        },
        "required": [
          "data"
        ],
        "title": "SuccessResponse",
        "type": "object"
      },
      "BadRequestResponse": {
        "description": "Returned when the request is malformed or contains invalid parameters. The message may be a simple string or a structured object with a code and detailed message.",
        "example": {
          "message": "invalid {resource}"
        },
        "oneOf": [
          {
            "properties": {
              "message": {
                "description": "A human-readable error message describing what was wrong with the request.",
                "type": "string"
              }
            },
            "required": [
              "message"
            ],
            "type": "object"
          },
          {
            "properties": {
              "message": {
                "properties": {
                  "code": {
                    "type": "string"
                  },
                  "message": {
                    "type": "string"
                  }
                },
                "required": [
                  "code",
                  "message"
                ],
                "type": "object"
              }
            },
            "type": "object"
          }
        ],
        "title": "BadRequestResponse",
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
      "ParameterError": {
        "example": {
          "code": "invalid_param",
          "message": "Invalid parameter",
          "param": "employment_id"
        },
        "properties": {
          "code": {
            "description": "An error code that describes the nature of the error.",
            "type": "string"
          },
          "message": {
            "description": "A developer friendly error message that gives details on what the error was and how it may be remedied.",
            "type": "string"
          },
          "param": {
            "description": "The parameter that lead to the error message.",
            "type": "string"
          }
        },
        "required": [
          "code",
          "message",
          "param"
        ],
        "title": "ParameterError",
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
              "project:write": "project:write",
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
              "project:read": "project:read",
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
    "/v1/employee/expenses": {
      "post": {
        "callbacks": {},
        "deprecated": false,
        "description": "Creates a new expense record for the current employee.\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage expenses (`employment_payments`) | - | Manage expenses (`expense:write`) |",
        "operationId": "post_v1_employee_expenses",
        "parameters": [],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/ParamsToCreateEmployeeExpense"
              }
            }
          },
          "description": "Expense params",
          "required": false
        },
        "responses": {
          "201": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/SuccessResponse"
                }
              }
            },
            "description": "Created"
          },
          "400": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/BadRequestResponse"
                }
              }
            },
            "description": "Bad Request"
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
          "422": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/UnprocessableEntityResponse"
                }
              }
            },
            "description": "Unprocessable Entity"
          }
        },
        "security": [
          {
            "OAuth2Assertion": [
              "https://gateway.remote.com/employment.manage",
              "expense:write",
              "employment_payments",
              "all:write"
            ]
          }
        ],
        "summary": "Create an expense for the authenticated employee",
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