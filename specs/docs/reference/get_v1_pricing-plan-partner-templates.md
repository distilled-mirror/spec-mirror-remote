---
updatedAt: 2026-05-27T21:19:01.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# List pricing plan partner templates

List all pricing plan partner templates.

## Authentication

This endpoint requires the following token type:

- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

Any one of the scopes in a token type's row is enough. `all:read` and `all:write` work too.

| Token type | Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|---|
| Client credentials access token | Manage companies (`company_management`) | View pricing plans (`pricing_plan:read`) | Manage pricing plans (`pricing_plan:write`) |

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
      "Product": {
        "additionalProperties": false,
        "description": "A Remote product offering (e.g., EOR, Contractor Management) with its tier and billing frequency.",
        "example": {
          "description": "EOR Monthly",
          "features": [
            "Feature 1",
            "Feature 2"
          ],
          "frequency": "monthly",
          "name": "EOR Monthly",
          "short_name": "EOR",
          "tier": "standard"
        },
        "properties": {
          "description": {
            "description": "A description of the product.",
            "type": "string"
          },
          "features": {
            "description": "Features included in this product tier.",
            "items": {
              "type": "string"
            },
            "type": "array"
          },
          "frequency": {
            "description": "The billing frequency (e.g., \"monthly\", \"annually\").",
            "type": "string"
          },
          "identifier": {
            "description": "A unique machine-readable identifier for this product.",
            "type": "string"
          },
          "name": {
            "description": "The full product name (e.g., \"EOR Monthly\").",
            "type": "string"
          },
          "short_name": {
            "description": "A short display name for the product (e.g., \"EOR\").",
            "type": "string"
          },
          "tier": {
            "description": "The product tier (e.g., \"standard\", \"premium\").",
            "type": "string"
          }
        },
        "required": [
          "name",
          "tier",
          "frequency"
        ],
        "title": "Product",
        "type": "object"
      },
      "ListPricingPlanPartnerTemplatesResponse": {
        "additionalProperties": false,
        "description": "List of pricing plan partner templates",
        "example": {
          "data": {
            "pricing_plan_partner_templates": [
              {
                "base_price": {
                  "amount": 29900,
                  "currency": {
                    "code": "CZK",
                    "name": "Czech Koruna",
                    "symbol": "Kč"
                  }
                },
                "id": "3b840951-099f-4bd5-90b9-032f7bfe51d9",
                "price": {
                  "amount": 29900,
                  "currency": {
                    "code": "CZK",
                    "name": "Czech Koruna",
                    "symbol": "Kč"
                  }
                },
                "product": {
                  "description": "EOR Monthly",
                  "features": [
                    "Feature 1",
                    "Feature 2"
                  ],
                  "frequency": "monthly",
                  "name": "EOR Monthly",
                  "short_name": "EOR",
                  "tier": "standard"
                }
              }
            ]
          }
        },
        "properties": {
          "data": {
            "additionalProperties": false,
            "properties": {
              "pricing_plan_partner_templates": {
                "items": {
                  "$ref": "#/components/schemas/PricingPlanPartnerTemplate"
                },
                "type": "array"
              }
            },
            "required": [
              "pricing_plan_partner_templates"
            ],
            "type": "object"
          }
        },
        "required": [
          "data"
        ],
        "title": "ListPricingPlanPartnerTemplatesResponse",
        "type": "object"
      },
      "PricingPlanPartnerTemplate": {
        "additionalProperties": false,
        "description": "Pricing plan partner template",
        "example": {
          "base_price": {
            "amount": 29900,
            "currency": {
              "code": "CZK",
              "name": "Czech Koruna",
              "symbol": "Kč"
            }
          },
          "id": "3b840951-099f-4bd5-90b9-032f7bfe51d9",
          "price": {
            "amount": 29900,
            "currency": {
              "code": "CZK",
              "name": "Czech Koruna",
              "symbol": "Kč"
            }
          },
          "product": {
            "description": "EOR Monthly",
            "features": [
              "Feature 1",
              "Feature 2"
            ],
            "frequency": "monthly",
            "name": "EOR Monthly",
            "short_name": "EOR",
            "tier": "standard"
          }
        },
        "properties": {
          "base_price": {
            "$ref": "#/components/schemas/Price"
          },
          "id": {
            "type": "string"
          },
          "period": {
            "description": "The period in months for the template, 0 means unlimited",
            "type": "integer"
          },
          "price": {
            "$ref": "#/components/schemas/Price"
          },
          "product": {
            "$ref": "#/components/schemas/Product"
          },
          "unlimited": {
            "description": "Whether the template is unlimited in time (do not expire)",
            "type": "boolean"
          }
        },
        "required": [
          "id",
          "product",
          "price",
          "base_price"
        ],
        "title": "PricingPlanPartnerTemplate",
        "type": "object"
      },
      "CurrencyDefinition": {
        "description": "Currency object without a UUID identifier",
        "example": {
          "code": "CZK",
          "name": "Czech Koruna",
          "symbol": "Kč"
        },
        "properties": {
          "code": {
            "type": "string"
          },
          "name": {
            "type": "string"
          },
          "symbol": {
            "type": "string"
          }
        },
        "required": [
          "code",
          "name",
          "symbol"
        ],
        "title": "CurrencyDefinition",
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
      "Price": {
        "additionalProperties": false,
        "description": "A monetary amount with its currency, used for pricing plan costs.",
        "example": {
          "amount": 29900,
          "currency": {
            "code": "CZK",
            "name": "Czech Koruna",
            "symbol": "Kč"
          }
        },
        "properties": {
          "amount": {
            "description": "Amount in cents",
            "type": "integer"
          },
          "currency": {
            "$ref": "#/components/schemas/CurrencyDefinition"
          }
        },
        "required": [
          "currency",
          "amount"
        ],
        "title": "Price",
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
    "title": "Partner Configuration",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/pricing-plan-partner-templates": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "List all pricing plan partner templates.\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\nAny one of the scopes in a token type's row is enough. `all:read` and `all:write` work too.\n\n| Token type | Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|---|\n| Client credentials access token | Manage companies (`company_management`) | View pricing plans (`pricing_plan:read`) | Manage pricing plans (`pricing_plan:write`) |",
        "operationId": "get_v1_pricing-plan-partner-templates",
        "parameters": [],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ListPricingPlanPartnerTemplatesResponse"
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
              "pricing_plan:read"
            ]
          },
          {
            "OAuth2ClientCredentials": [
              "all:read"
            ]
          },
          {
            "OAuth2ClientCredentials": [
              "all:write"
            ]
          }
        ],
        "summary": "List pricing plan partner templates",
        "tags": [
          "Pricing Plans"
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
    "company.pricing_plan.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company pricing plan is updated.",
        "operationId": "company.pricing_plan.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "company.pricing_plan.updated",
                  "pricing_plan_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "pricing_plan_id": {
                    "description": "The unique identifier of the pricing plan.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "company_id",
                  "pricing_plan_id"
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
        "summary": "company.pricing_plan.updated",
        "tags": [
          "Pricing Plans"
        ]
      }
    },
    "sso_configuration.disabled": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the SSO Configuration is disabled.",
        "operationId": "sso_configuration.disabled",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "event_type": "sso_configuration.disabled"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  }
                },
                "required": [
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
        "summary": "sso_configuration.disabled",
        "tags": [
          "SSO Configuration"
        ]
      }
    },
    "sso_configuration.enabled": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the SSO Configuration is enabled.",
        "operationId": "sso_configuration.enabled",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "event_type": "sso_configuration.enabled"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  }
                },
                "required": [
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
        "summary": "sso_configuration.enabled",
        "tags": [
          "SSO Configuration"
        ]
      }
    },
    "sso_configuration.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the SSO Configuration is updated.",
        "operationId": "sso_configuration.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "event_type": "sso_configuration.updated"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  }
                },
                "required": [
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
        "summary": "sso_configuration.updated",
        "tags": [
          "SSO Configuration"
        ]
      }
    }
  }
}
```