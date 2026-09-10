---
updatedAt: 2026-07-29T14:56:54.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# List Pay Codes

Lists pay codes available for a legal entity.
Pay codes represent the allowed pay element types that can be submitted via `POST /v1/pay-items/bulk`.

## Authentication

This endpoint accepts any one of the following token types:

- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).
- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage payroll runs (`payroll`) | View pay items (`pay_item:read`) | Manage pay items (`pay_item:write`) |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "PayCode": {
        "additionalProperties": false,
        "example": {
          "category": "time_and_attendance",
          "code": "overtime",
          "description": "Hours worked beyond standard schedule",
          "external_import_code": null,
          "name": "Overtime",
          "slug": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
          "type": "hours"
        },
        "properties": {
          "category": {
            "description": "Pay element category (e.g. time_and_attendance, bonus)",
            "type": "string"
          },
          "code": {
            "description": "Code to use in the `code` field of POST /v1/pay-items/bulk",
            "type": "string"
          },
          "description": {
            "description": "Description of the pay code",
            "nullable": true,
            "type": "string"
          },
          "external_import_code": {
            "description": "Customer-specific code used for bulk import mapping",
            "nullable": true,
            "type": "string"
          },
          "name": {
            "description": "Human-readable name of the pay code",
            "type": "string"
          },
          "slug": {
            "description": "Unique identifier for this pay code",
            "format": "uuid",
            "type": "string"
          },
          "type": {
            "description": "How the `amount` field on POST /v1/pay-items/bulk must be encoded for this pay code:\n`amount` in cents, `percentage` in basis points, `unit` as a raw count, `hours` as a whole number of hours, `duration` in seconds.\n",
            "type": "string"
          }
        },
        "required": [
          "slug",
          "code",
          "name",
          "type",
          "category"
        ],
        "title": "PayCode",
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
      "ListPayCodesResponse": {
        "description": "Response schema listing many pay_codes",
        "example": {
          "current_page": 1,
          "pay_codes": [
            {
              "category": "time_and_attendance",
              "code": "overtime",
              "description": "Hours worked beyond standard schedule",
              "external_import_code": null,
              "name": "Overtime",
              "slug": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
              "type": "hours"
            }
          ],
          "total_count": 1,
          "total_pages": 1
        },
        "properties": {
          "data": {
            "properties": {
              "current_page": {
                "description": "The current page among all of the total_pages",
                "type": "integer"
              },
              "pay_codes": {
                "items": {
                  "$ref": "#/components/schemas/PayCode"
                },
                "type": "array"
              },
              "total_count": {
                "description": "The total number of records in the result",
                "type": "integer"
              },
              "total_pages": {
                "description": "The total number of pages the user can go through",
                "type": "integer"
              }
            },
            "type": "object"
          }
        },
        "title": "ListPayCodesResponse",
        "type": "object"
      },
      "UuidSlug": {
        "description": "Identifier of the employment being terminated.",
        "example": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
        "format": "uuid",
        "title": "UuidSlug",
        "type": "string"
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
    "title": "Pay & Compensation",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/companies/{company_id}/legal-entities/{legal_entity_id}/pay-codes": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "Lists pay codes available for a legal entity.\nPay codes represent the allowed pay element types that can be submitted via `POST /v1/pay-items/bulk`.\n\n## Authentication\n\nThis endpoint accepts any one of the following token types:\n\n- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage payroll runs (`payroll`) | View pay items (`pay_item:read`) | Manage pay items (`pay_item:write`) |",
        "operationId": "get_v1_companies_company_id_legal-entities_legal_entity_id_pay-codes",
        "parameters": [
          {
            "description": "Company ID",
            "in": "path",
            "name": "company_id",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/UuidSlug"
            }
          },
          {
            "description": "Legal entity ID",
            "in": "path",
            "name": "legal_entity_id",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/UuidSlug"
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
                  "$ref": "#/components/schemas/ListPayCodesResponse"
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
            "OAuth2AuthorizationCode": [
              "https://gateway.remote.com/company.manage",
              "pay_item:read",
              "pay_item:write",
              "payroll",
              "all:write",
              "all:read"
            ],
            "OAuth2ClientCredentials": [
              "https://gateway.remote.com/company.manage",
              "pay_item:read",
              "pay_item:write",
              "payroll",
              "all:write",
              "all:read"
            ]
          }
        ],
        "summary": "List Pay Codes",
        "tags": [
          "Pay Items"
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
    "expense.approved": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an expense is approved.",
        "operationId": "expense.approved",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "expense.approved",
                  "expense_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "expense_id": {
                    "description": "The unique identifier of the related expense.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "expense_id",
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
        "summary": "expense.approved",
        "tags": [
          "Expenses"
        ]
      }
    },
    "expense.created": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a draft expense is created.",
        "operationId": "expense.created",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "expense.created",
                  "expense_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "expense_id": {
                    "description": "The unique identifier of the related expense.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "expense_id",
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
        "summary": "expense.created",
        "tags": [
          "Expenses"
        ]
      }
    },
    "expense.declined": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an expense is declined.",
        "operationId": "expense.declined",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "expense.declined",
                  "expense_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "expense_id": {
                    "description": "The unique identifier of the related expense.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "expense_id",
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
        "summary": "expense.declined",
        "tags": [
          "Expenses"
        ]
      }
    },
    "expense.deleted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an expense is deleted by a team member or an admin.",
        "operationId": "expense.deleted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "expense.deleted",
                  "expense_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "expense_id": {
                    "description": "The unique identifier of the related expense.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "expense_id",
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
        "summary": "expense.deleted",
        "tags": [
          "Expenses"
        ]
      }
    },
    "expense.reimbursed": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an expense is reimbursed.",
        "operationId": "expense.reimbursed",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "expense.reimbursed",
                  "expense_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "expense_id": {
                    "description": "The unique identifier of the related expense.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "expense_id",
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
        "summary": "expense.reimbursed",
        "tags": [
          "Expenses"
        ]
      }
    },
    "expense.submitted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an expense is submitted by an employee.",
        "operationId": "expense.submitted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "expense.submitted",
                  "expense_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "expense_id": {
                    "description": "The unique identifier of the related expense.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "expense_id",
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
        "summary": "expense.submitted",
        "tags": [
          "Expenses"
        ]
      }
    },
    "expense.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an expense is updated.",
        "operationId": "expense.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "expense.updated",
                  "expense_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "expense_id": {
                    "description": "The unique identifier of the related expense.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "expense_id",
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
        "summary": "expense.updated",
        "tags": [
          "Expenses"
        ]
      }
    },
    "incentive.created": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an incentive is created",
        "operationId": "incentive.created",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "incentive.created",
                  "incentive_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "incentive_id": {
                    "description": "The unique identifier of the related incentive.",
                    "type": "string"
                  }
                },
                "required": [
                  "incentive_id",
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
        "summary": "incentive.created",
        "tags": [
          "Incentives"
        ]
      }
    },
    "incentive.deleted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an incentive is deleted.",
        "operationId": "incentive.deleted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "incentive.deleted",
                  "incentive_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "incentive_id": {
                    "description": "The unique identifier of the related incentive.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "incentive_id",
                  "employment_id",
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
        "summary": "incentive.deleted",
        "tags": [
          "Incentives"
        ]
      }
    },
    "incentive.paid": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an incentive is paid",
        "operationId": "incentive.paid",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2610f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "incentive.paid",
                  "incentive_id": "0078fcb5-b669-4e4a-b963-2a47744e75a1"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "incentive_id": {
                    "description": "The unique identifier of the related incentive.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "incentive_id",
                  "employment_id",
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
        "summary": "incentive.paid",
        "tags": [
          "Incentives"
        ]
      }
    },
    "incentive.processing_started": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an incentive has its processing started",
        "operationId": "incentive.processing_started",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "incentive.processing_started",
                  "incentive_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "incentive_id": {
                    "description": "The unique identifier of the related incentive.",
                    "type": "string"
                  }
                },
                "required": [
                  "incentive_id",
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
        "summary": "incentive.processing_started",
        "tags": [
          "Incentives"
        ]
      }
    },
    "incentive.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an incentive is updated.",
        "operationId": "incentive.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "incentive.updated",
                  "incentive_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "incentive_id": {
                    "description": "The unique identifier of the related incentive.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "incentive_id",
                  "employment_id",
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
        "summary": "incentive.updated",
        "tags": [
          "Incentives"
        ]
      }
    },
    "payslip.released": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a payslip is ready and available for an employee.\n",
        "operationId": "payslip.released",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "45b34922-2590-43a0-ac05-ad23834adb8f",
                  "event_type": "payslip.released",
                  "payslip_id": "86e56288-ca62-11ed-9702-a703c40b6c0d"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_id": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  },
                  "event_type": {
                    "description": "The webhook event type identifier.",
                    "type": "string"
                  },
                  "payslip_id": {
                    "description": "The unique identifier of the related payslip.",
                    "type": "string"
                  }
                },
                "required": [
                  "employment_id",
                  "payslip_id",
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
        "summary": "payslip.released",
        "tags": [
          "Payslips"
        ]
      }
    }
  }
}
```