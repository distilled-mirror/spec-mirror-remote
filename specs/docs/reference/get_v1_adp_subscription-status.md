---
updatedAt: 2026-09-01T13:18:32.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# Receive an ADP Marketplace subscription-status event

Called by ADP Marketplace when a subscription's status changes (e.g. trial ended, suspended).

## Authentication

This endpoint requires the following token type:

- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "AdpSubscriptionOrderEventResponse": {
        "description": "The answer to an ADP Marketplace event: either the success acknowledgement or the error one.",
        "example": {
          "accountIdentifier": "G3XZAJYHXEV6DH1N",
          "success": true
        },
        "oneOf": [
          {
            "$ref": "#/components/schemas/AdpSubscriptionOrderSuccessAck"
          },
          {
            "$ref": "#/components/schemas/AdpSubscriptionOrderErrorAck"
          }
        ],
        "title": "AdpSubscriptionOrderEventResponse"
      },
      "AdpSubscriptionOrderSuccessAck": {
        "description": "The answer to ADP when the event was received. ADP's own connectivity test (a call without `eventUrl`) is answered with `success` only.",
        "example": {
          "accountIdentifier": "G3XZAJYHXEV6DH1N",
          "success": true
        },
        "properties": {
          "accountIdentifier": {
            "description": "The organization identifier from the event. A value does not mean the subscription was saved. Absent for ADP's connectivity test, and may be `null`.",
            "example": "G3XZAJYHXEV6DH1N",
            "nullable": true,
            "type": "string"
          },
          "success": {
            "description": "`true` means the event was received. It is also sent when the event could not be saved.",
            "enum": [
              true
            ],
            "example": true,
            "type": "boolean"
          }
        },
        "required": [
          "success"
        ],
        "title": "AdpSubscriptionOrderSuccessAck",
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
      "AdpSubscriptionOrderErrorAck": {
        "description": "The answer to ADP when the event could not be fetched or processed. ADP requires HTTP 200 with this body, never a 4xx or 5xx.",
        "example": {
          "errorCode": "TRANSPORT_ERROR",
          "message": "Failed to process the event",
          "success": "false"
        },
        "properties": {
          "errorCode": {
            "description": "One of ADP's predefined subscription response error codes. `TRANSPORT_ERROR`: the event URL was refused, or the fetch from ADP failed or returned an error status. `INVALID_RESPONSE`: anything else went wrong, including getting Tiger's ADP token.",
            "enum": [
              "TRANSPORT_ERROR",
              "INVALID_RESPONSE"
            ],
            "type": "string"
          },
          "message": {
            "description": "A short description of the failure.",
            "type": "string"
          },
          "success": {
            "description": "Always the string `\"false\"`.",
            "enum": [
              "false"
            ],
            "type": "string"
          }
        },
        "required": [
          "success",
          "errorCode",
          "message"
        ],
        "title": "AdpSubscriptionOrderErrorAck",
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
    "/v1/adp/subscription-status": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "Called by ADP Marketplace when a subscription's status changes (e.g. trial ended, suspended).\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).",
        "operationId": "get_v1_adp_subscription-status",
        "parameters": [
          {
            "description": "URL ADP provides to fetch the event payload from. Absent for ADP's own connectivity/test calls, which are acked without a fetch.",
            "in": "query",
            "name": "eventUrl",
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
                  "$ref": "#/components/schemas/AdpSubscriptionOrderEventResponse"
                }
              }
            },
            "description": "ADP acknowledgement, success or error (always HTTP 200)"
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
          }
        },
        "security": [
          {
            "OAuth2ClientCredentials": []
          }
        ],
        "summary": "Receive an ADP Marketplace subscription-status event",
        "tags": [
          "ADP Marketplace"
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