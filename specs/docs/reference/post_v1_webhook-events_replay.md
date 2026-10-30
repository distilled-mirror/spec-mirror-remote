---
updatedAt: 2026-05-27T21:27:06.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# Replay Webhook Events

Replay webhook events

## Authentication

This endpoint requires the following token type:

- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

Any one of the scopes in a token type's row is enough. `all:write` works too.

| Token type | Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|---|
| Client credentials access token | Manage company resources (`company_admin`) | - | Manage webhooks (`webhook:write`) |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
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
      "ReplayWebhookEventsParams": {
        "additionalProperties": false,
        "description": "Replay webhook events params",
        "example": {
          "after": "2025-01-02T00:00:00Z",
          "before": "2025-01-01T00:00:00Z",
          "company_id": "123e4567-e89b-12d3-a456-426614174000",
          "event_type": "timesheet.created",
          "successfully_delivered": true
        },
        "oneOf": [
          {
            "$ref": "#/components/schemas/IdsRequiredParams"
          },
          {
            "$ref": "#/components/schemas/BeforeAfterRequiredParams"
          }
        ],
        "title": "ReplayWebhookEventsParams",
        "type": "object"
      },
      "BeforeAfterRequiredParams": {
        "additionalProperties": false,
        "example": {
          "after": "2025-01-02T00:00:00Z",
          "before": "2025-01-01T00:00:00Z"
        },
        "properties": {
          "after": {
            "description": "Only replay events triggered after this timestamp (ISO 8601).",
            "example": "2025-01-01T00:00:00Z",
            "type": "string"
          },
          "before": {
            "description": "Only replay events triggered before this timestamp (ISO 8601).",
            "example": "2025-01-01T00:00:00Z",
            "type": "string"
          },
          "company_id": {
            "description": "Optional filter to only replay events for a specific company.",
            "example": "123e4567-e89b-12d3-a456-426614174000",
            "type": "string"
          },
          "event_type": {
            "description": "Optional filter to only replay events of this type.",
            "example": "timesheet.created",
            "type": "string"
          },
          "successfully_delivered": {
            "description": "Optional filter by delivery status. Set to false to replay only failed deliveries.",
            "example": true,
            "type": "boolean"
          }
        },
        "required": [
          "before",
          "after"
        ],
        "title": "BeforeAfterRequiredParams",
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
      "IdsRequiredParams": {
        "additionalProperties": false,
        "example": {
          "ids": [
            "0073fcb5-b669-4e4a-b963-2a47744e75a1"
          ]
        },
        "properties": {
          "ids": {
            "description": "A list of webhook event IDs to replay.",
            "example": [
              "0073fcb5-b669-4e4a-b963-2a47744e75a1"
            ],
            "items": {
              "type": "string"
            },
            "type": "array"
          }
        },
        "required": [
          "ids"
        ],
        "title": "IdsRequiredParams",
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
              "company_department:read": "View departments: Read and list company departments",
              "webhook:write": "Manage webhooks: Set webhook callbacks and replay webhooks",
              "magic_link:write": "Create magic links: Create magic links",
              "offboarding:write": "Manage offboarding: Creates offboarding requests",
              "custom_field:write": "Manage custom fields: Create custom fields",
              "address:write": "Manage addresses: Create and update employee residential address",
              "expense:read": "View expenses: List and read expenses",
              "employment:write": "Manage employments: Create and update employments",
              "identity_verification:write": "Manage identity verification: Write identity verification data",
              "timesheet:write": "Manage timesheets: Create timesheets",
              "travel_letter:write": "Manage travel letters: Create travel letters",
              "all:read": "Read only: List and retrieve information about all resources",
              "incentive:read": "View incentives: List incentives and recurring incentives",
              "personal_detail:read": "View personal details: Read employee personal information",
              "invoices:write": "Manage invoices: Create invoices",
              "work_authorization:write": "Manage work authorizations: Create work authorization requests",
              "timeoff:write": "Manage timeoffs: Create, update and cancel timeoffs",
              "company_structure:read": "View company structure: Show company structure",
              "benefit_renewal:write": "Manage benefit renewals: Update benefit renewal requests",
              "benefit_offer:read": "View benefit offers: List benefit offers",
              "employment_documents": "Manage employment documents: Manage employment documents",
              "onboarding:write": "Manage onboarding: Cancel onboarding",
              "https://gateway.remote.com/company.manage": "Legacy scope. A new request for it gets `all:write`; tokens authorized before late March 2026 may still hold it. Many endpoints accept it, but not all: see the endpoint's `security` in the OpenAPI file",
              "project:write": "Manage projects: Create and update company projects and their leads and team members",
              "pay_in_details:read": "View pay-in details: Read the payment reference and Remote's bank details for paying contractor invoices",
              "payroll_run:read": "View payroll runs: List and show payroll runs",
              "risk_reserve:write": "Manage risk reserves: Create risk reserves for a company",
              "invoices": "Manage invoices: Manage invoices",
              "resignation_letter:read": "View resignation letters: Read resignation letters",
              "resignation:read": "View resignations: Read resignation requests",
              "convert_currency:read": "Convert currencies: Convert currencies",
              "all:write": "Full Access: Grant access to all scopes based on your current role permissions",
              "https://gateway.remote.com/employment.manage": "Legacy scope. A new request for it gets `all:write`; tokens authorized before late March 2026 may still hold it. Many endpoints accept it, but not all: see the endpoint's `security` in the OpenAPI file",
              "employments": "Manage employments: Create and manage employments",
              "probation_document:read": "View probation documents: Read probation completion letters and probation extensions documents",
              "company_admin": "Manage company resources: Create and manage company resources",
              "payroll": "Manage payroll runs: Manage payroll runs and calendars",
              "help_center_article:read": "View help articles: Read help center articles",
              "timesheet:read": "View timesheets: Read timesheets",
              "custom_field_value:write": "Manage custom field values: Create custom field values",
              "company_currencies:read": "View company currencies: List company supported currencies",
              "payslip:read": "View payslips: List and show employee's payslip",
              "pay_item:write": "Manage pay items: Create pay items for employments",
              "resignation:write": "Manage resignations: Validate resignation requests",
              "custom_field:read": "View custom fields: List custom fields",
              "payroll_calendar:read": "View payroll calendars: List payroll calendars",
              "contract_amendment:write": "Manage contract amendments: Create contract amendments",
              "offboarding:read": "View offboarding requests: Read and list offboarding requests",
              "timeoff:read": "View timeoffs: Read and list timeoffs",
              "pay_in_details": "View pay-in bank details: Read the payment reference and Remote's receiving bank accounts for paying invoices",
              "probation_document:write": "Manage probation documents: Create probation completion letters and probation extensions documents",
              "country:read": "View countries: Read and list countries",
              "webhook:read": "View webhooks: Read webhooks callback logs",
              "company_department:write": "Manage departments: Create company departments",
              "company_manager:read": "View managers: Read and list company managers",
              "pay_item:read": "View pay items: List pay items for employments",
              "contract_amendment:read": "View contract amendments: List and show contract amendments",
              "company:read": "View companies: Read and list companies",
              "sso_configuration:write": "Manage SSO: Set SSO configuration",
              "benefit_offer:write": "Manage benefit offers: Create benefit offers",
              "contract_eligibility:write": "Manage contract eligibility: Create contract eligibility for an employment",
              "benefit_renewal:read": "View benefit renewals: List benefit renewal requests",
              "background_check:read": "View background checks: Read and show background check requests",
              "custom_field_value:read": "View custom field values: List custom field values",
              "expense:write": "Manage expenses: Create expenses",
              "identity_verification:read": "View identity verification: Read identity verification data",
              "address:read": "View addresses: Read employee residential address",
              "document:write": "Manage documents: Write and update documents",
              "time_and_attendance": "Manage timeoffs: Manage timeoffs, leave-policies and timesheets",
              "employment_payments": "Manage expenses: Manage expenses and incentives",
              "form:read": "View forms: Read json schema forms",
              "work_authorization:read": "View work authorizations: List work authorization requests",
              "invoices:read": "View invoices: Read and list invoices",
              "incentive:write": "Manage incentives: Create incentives",
              "employment:read": "View employments: List and read employments",
              "contract:read": "View contracts: List employment contracts",
              "projects": "Manage projects: Create and manage company projects and their leads and team members",
              "company_manager:write": "Manage managers: Create and delete company managers",
              "travel_letter:read": "View travel letters: Read travel letters",
              "project:read": "View projects: List and read company projects",
              "document:read": "View documents: Read and list documents",
              "sso_configuration:read": "View SSO configuration: Read SSO configuration"
            },
            "tokenUrl": "/auth/oauth2/token"
          },
          "clientCredentials": {
            "scopes": {
              "all:read": "Read only: List and retrieve information about all resources",
              "all:write": "Full Access: Grant access to all scopes based on your current role permissions",
              "company:read": "View companies: Read and list companies",
              "company:write": "Manage companies: Create, Read and update companies",
              "company_admin": "Manage company resources: Create and manage company resources",
              "company_management": "Manage companies: Create and manage companies",
              "convert_currency:read": "Convert currencies: Convert currencies",
              "country:read": "View countries: Read and list countries",
              "employment_documents": "Manage employment documents: Manage employment documents",
              "employment_payments": "Manage expenses: Manage expenses and incentives",
              "employments": "Manage employments: Create and manage employments",
              "help_center_article:read": "View help articles: Read help center articles",
              "https://gateway.remote.com/company.manage": "Legacy scope, kept as sent. Some endpoints accept it, not all: see the endpoint's `security` in the OpenAPI file",
              "https://gateway.remote.com/employment.manage": "Legacy scope, kept as sent. Some endpoints accept it, not all: see the endpoint's `security` in the OpenAPI file",
              "invoices": "Manage invoices: Manage invoices",
              "payroll": "Manage payroll runs: Manage payroll runs and calendars",
              "payroll_calendar:read": "View payroll calendars: List payroll calendars",
              "pricing_plan:read": "View pricing plans: List pricing plans",
              "pricing_plan:write": "Manage pricing plans: Create pricing plans",
              "time_and_attendance": "Manage timeoffs: Manage timeoffs, leave-policies and timesheets",
              "webhook:read": "View webhooks: Read webhooks callback logs",
              "webhook:write": "Manage webhooks: Set webhook callbacks and replay webhooks"
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
              "all:read": "Read only: List and retrieve information about all resources",
              "all:write": "Full Access: Grant access to all scopes based on your current role permissions",
              "company:read": "View companies: Read and list companies",
              "company:write": "Manage companies: Create, Read and update companies",
              "company_admin": "Manage company resources: Create and manage company resources",
              "company_management": "Manage companies: Create and manage companies",
              "convert_currency:read": "Convert currencies: Convert currencies",
              "country:read": "View countries: Read and list countries",
              "employment_documents": "Manage employment documents: Manage employment documents",
              "employment_payments": "Manage expenses: Manage expenses and incentives",
              "employments": "Manage employments: Create and manage employments",
              "help_center_article:read": "View help articles: Read help center articles",
              "https://gateway.remote.com/company.manage": "Legacy scope, kept as sent. Some endpoints accept it, not all: see the endpoint's `security` in the OpenAPI file",
              "https://gateway.remote.com/employment.manage": "Legacy scope, kept as sent. Some endpoints accept it, not all: see the endpoint's `security` in the OpenAPI file",
              "invoices": "Manage invoices: Manage invoices",
              "payroll": "Manage payroll runs: Manage payroll runs and calendars",
              "payroll_calendar:read": "View payroll calendars: List payroll calendars",
              "pricing_plan:read": "View pricing plans: List pricing plans",
              "pricing_plan:write": "Manage pricing plans: Create pricing plans",
              "time_and_attendance": "Manage timeoffs: Manage timeoffs, leave-policies and timesheets",
              "webhook:read": "View webhooks: Read webhooks callback logs",
              "webhook:write": "Manage webhooks: Set webhook callbacks and replay webhooks"
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
    "/v1/webhook-events/replay": {
      "post": {
        "callbacks": {},
        "deprecated": false,
        "description": "Replay webhook events\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\nAny one of the scopes in a token type's row is enough. `all:write` works too.\n\n| Token type | Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|---|\n| Client credentials access token | Manage company resources (`company_admin`) | - | Manage webhooks (`webhook:write`) |",
        "operationId": "post_v1_webhook-events_replay",
        "parameters": [],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/ReplayWebhookEventsParams"
              }
            }
          },
          "description": "WebhookEvent",
          "required": true
        },
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/SuccessResponse"
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
              "https://gateway.remote.com/company.manage"
            ]
          },
          {
            "OAuth2ClientCredentials": [
              "webhook:write"
            ]
          },
          {
            "OAuth2ClientCredentials": [
              "all:write"
            ]
          }
        ],
        "summary": "Replay Webhook Events",
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