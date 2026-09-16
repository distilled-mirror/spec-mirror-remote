---
updatedAt: 2026-05-27T21:27:06.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# List Webhook Events

List all webhook events

## Authentication

This endpoint requires the following token type:

- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage company resources (`company_admin`) | View webhooks (`webhook:read`) | Manage webhooks (`webhook:write`) |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "WebhookEvent": {
        "additionalProperties": false,
        "example": {
          "company_id": "123e4567-e89b-12d3-a456-426614174000",
          "event_type": "timesheet.created",
          "first_triggered_at": "2025-01-01T00:00:00Z",
          "id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
          "last_triggered_at": "2025-01-02T00:00:00Z",
          "successfully_delivered": true
        },
        "properties": {
          "company_id": {
            "description": "The unique identifier (UUID) of the company this event belongs to.",
            "type": "string"
          },
          "event_type": {
            "description": "The type of event that was triggered (e.g., \"timesheet.created\", \"employment.activated\").",
            "type": "string"
          },
          "first_triggered_at": {
            "description": "The timestamp when this event was first triggered.",
            "type": "string"
          },
          "id": {
            "description": "The unique identifier (UUID) of the webhook event.",
            "type": "string"
          },
          "last_triggered_at": {
            "description": "The timestamp of the most recent delivery attempt for this event.",
            "type": "string"
          },
          "successfully_delivered": {
            "description": "Whether the webhook event was successfully delivered to the callback URL (received a 2XX response).",
            "type": "boolean"
          }
        },
        "required": [
          "id",
          "event_type",
          "successfully_delivered",
          "company_id",
          "first_triggered_at",
          "last_triggered_at"
        ],
        "title": "WebhookEvent",
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
      "ListWebhookEventsResponse": {
        "description": "Response schema listing many webhook_events",
        "example": {
          "current_page": 1,
          "total_count": 1,
          "total_pages": 1,
          "webhook_events": [
            {
              "company_id": "123e4567-e89b-12d3-a456-426614174000",
              "event_type": "timesheet.created",
              "first_triggered_at": "2025-01-01T00:00:00Z",
              "id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
              "last_triggered_at": "2025-01-02T00:00:00Z",
              "successfully_delivered": true
            }
          ]
        },
        "properties": {
          "data": {
            "properties": {
              "current_page": {
                "description": "The current page among all of the total_pages",
                "type": "integer"
              },
              "total_count": {
                "description": "The total number of records in the result",
                "type": "integer"
              },
              "total_pages": {
                "description": "The total number of pages the user can go through",
                "type": "integer"
              },
              "webhook_events": {
                "items": {
                  "$ref": "#/components/schemas/WebhookEvent"
                },
                "type": "array"
              }
            },
            "type": "object"
          }
        },
        "title": "ListWebhookEventsResponse",
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
      "OAuth2ClientCredentials": {
        "description": "Authenticate using `client_credentials` grant in the OAuth 2.0 protocol.\n",
        "flows": {
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
      }
    }
  },
  "info": {
    "title": "Integrations",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/webhook-events": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "List all webhook events\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage company resources (`company_admin`) | View webhooks (`webhook:read`) | Manage webhooks (`webhook:write`) |",
        "operationId": "get_v1_webhook-events",
        "parameters": [
          {
            "description": "Filter by webhook event type",
            "example": "timesheet.created",
            "in": "query",
            "name": "event_type",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "description": "Filter by delivery status (true = 200, false = 4xx/5xx)",
            "example": true,
            "in": "query",
            "name": "successfully_delivered",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "description": "Filter by company ID",
            "example": "123e4567-e89b-12d3-a456-426614174000",
            "in": "query",
            "name": "company_id",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "description": "Filter by date before (ISO 8601 format)",
            "example": "2025-01-01T00:00:00Z",
            "in": "query",
            "name": "before",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "description": "Filter by date after (ISO 8601 format)",
            "example": "2025-01-01T00:00:00Z",
            "in": "query",
            "name": "after",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "description": "Sort order",
            "example": "asc",
            "in": "query",
            "name": "order",
            "required": false,
            "schema": {
              "enum": [
                "asc",
                "desc"
              ],
              "type": "string"
            }
          },
          {
            "description": "Field to sort by",
            "example": "first_triggered_at",
            "in": "query",
            "name": "sort_by",
            "required": false,
            "schema": {
              "enum": [
                "first_triggered_at"
              ],
              "type": "string"
            }
          },
          {
            "description": "Starts fetching records after the given page",
            "example": 1,
            "in": "query",
            "name": "page",
            "required": false,
            "schema": {
              "default": 1,
              "minimum": 1,
              "type": "integer"
            }
          },
          {
            "description": "Number of items per page",
            "example": 20,
            "in": "query",
            "name": "page_size",
            "required": false,
            "schema": {
              "default": 20,
              "maximum": 100,
              "minimum": 1,
              "type": "integer"
            }
          }
        ],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ListWebhookEventsResponse"
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
          "404": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/NotFoundResponse"
                }
              }
            },
            "description": "Not Found"
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
            "OAuth2ClientCredentials": [
              "https://gateway.remote.com/company.manage",
              "webhook:read",
              "webhook:write",
              "company_admin",
              "all:write",
              "all:read"
            ]
          }
        ],
        "summary": "List Webhook Events",
        "tags": [
          "Webhook Events"
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
  ],
  "webhooks": {
    "custom_field.value_updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a custom field value is updated.",
        "operationId": "custom_field.value_updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "custom_field_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "custom_field.value_updated"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "custom_field_id": {
                    "description": "The unique identifier of the custom field.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  }
                },
                "required": [
                  "custom_field_id",
                  "employment_id",
                  "event_type",
                  "company_id"
                ]
              }
            }
          }
        },
        "responses": {
          "2XX": {
            "description": "Any 200 response confirms that the webhook was delivered."
          }
        },
        "security": [],
        "summary": "custom_field.value_updated",
        "tags": [
          "Custom Fields"
        ]
      }
    }
  }
}
```