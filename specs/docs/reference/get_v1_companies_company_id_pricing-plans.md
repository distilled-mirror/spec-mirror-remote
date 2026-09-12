---
updatedAt: 2026-05-27T21:19:01.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# List pricing plans

List all pricing plans for a company.
Currently the endpoint only returns the pricing plans for the EOR monthly product and the contractor products (Standard, Plus and COR).

## Authentication

This endpoint accepts any one of the following token types:

- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).
- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage companies (`company_management`) | View pricing plans (`pricing_plan:read`) | Manage pricing plans (`pricing_plan:write`) |

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
      "PricingPlan": {
        "additionalProperties": false,
        "description": "A pricing plan assigned to a company, defining the product, billing frequency, and cost.",
        "example": {
          "base_price": {
            "amount": 29900,
            "currency": {
              "code": "CZK",
              "name": "Czech Koruna",
              "symbol": "Kč"
            }
          },
          "end_date": "2025-12-31",
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
          },
          "start_date": "2025-01-01",
          "type": "termed"
        },
        "properties": {
          "base_price": {
            "$ref": "#/components/schemas/Price"
          },
          "end_date": {
            "description": "End date of the pricing plan this will be nil if the pricing plan is unlimited otherwise it will be the last day of the month",
            "format": "date",
            "nullable": true,
            "type": "string"
          },
          "id": {
            "description": "The unique identifier (UUID) of the pricing plan.",
            "type": "string"
          },
          "price": {
            "$ref": "#/components/schemas/Price"
          },
          "product": {
            "$ref": "#/components/schemas/Product"
          },
          "start_date": {
            "description": "Start date of the pricing plan this will always be the first of the month, for example 2025-01-01 will be used if the user provided 2025-01-02",
            "format": "date",
            "type": "string"
          },
          "type": {
            "description": "The pricing plan type (e.g., \"termed\" for fixed-term, \"evergreen\" for ongoing).",
            "type": "string"
          }
        },
        "required": [
          "id",
          "type",
          "start_date",
          "end_date",
          "product",
          "price",
          "base_price"
        ],
        "title": "PricingPlan",
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
      "ListCompanyPricingPlansResponse": {
        "additionalProperties": false,
        "description": "Company pricing plans",
        "example": {
          "data": {
            "pricing_plans": [
              {
                "base_price": {
                  "amount": 29900,
                  "currency": {
                    "code": "CZK",
                    "name": "Czech Koruna",
                    "symbol": "Kč"
                  }
                },
                "end_date": "2025-12-31",
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
                },
                "start_date": "2025-01-01",
                "type": "termed"
              }
            ]
          }
        },
        "properties": {
          "data": {
            "additionalProperties": false,
            "properties": {
              "pricing_plans": {
                "items": {
                  "$ref": "#/components/schemas/PricingPlan"
                },
                "type": "array"
              }
            },
            "required": [
              "pricing_plans"
            ],
            "type": "object"
          }
        },
        "required": [
          "data"
        ],
        "title": "ListCompanyPricingPlansResponse",
        "type": "object"
      },
      "UuidSlug": {
        "description": "Identifier of the employment being terminated.",
        "example": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
        "format": "uuid",
        "title": "UuidSlug",
        "type": "string"
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
      "OAuth2AuthorizationCode": {
        "description": "Authenticate as the token authorizer using `authorization_code` / `refresh_token` grants in the OAuth 2.0 protocol.\n",
        "flows": {
          "authorizationCode": {
            "authorizationUrl": "/auth/oauth2/authorize",
            "refreshUrl": "/auth/oauth2/token",
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
              "project:read": "project:read",
              "document:read": "document:read",
              "sso_configuration:read": "sso_configuration:read"
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
    "title": "Partner Configuration",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/companies/{company_id}/pricing-plans": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "List all pricing plans for a company.\nCurrently the endpoint only returns the pricing plans for the EOR monthly product and the contractor products (Standard, Plus and COR).\n\n## Authentication\n\nThis endpoint accepts any one of the following token types:\n\n- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage companies (`company_management`) | View pricing plans (`pricing_plan:read`) | Manage pricing plans (`pricing_plan:write`) |",
        "operationId": "get_v1_companies_company_id_pricing-plans",
        "parameters": [
          {
            "description": "Company ID",
            "example": "123e4567-e89b-12d3-a456-426614174000",
            "in": "path",
            "name": "company_id",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/UuidSlug"
            }
          }
        ],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ListCompanyPricingPlansResponse"
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
              "pricing_plan:read",
              "pricing_plan:write",
              "company_management",
              "all:write",
              "all:read"
            ]
          },
          {
            "OAuth2AuthorizationCode": [
              "https://gateway.remote.com/company.manage",
              "pricing_plan:read",
              "pricing_plan:write",
              "company_management",
              "all:write",
              "all:read"
            ]
          }
        ],
        "summary": "List pricing plans",
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