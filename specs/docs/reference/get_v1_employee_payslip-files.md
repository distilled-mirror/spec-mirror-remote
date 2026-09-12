---
updatedAt: 2026-05-27T21:25:32.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# List payslip files for the authenticated employee

Returns a paginated list of payslip files belonging to the current employee.

## Authentication

This endpoint requires the following token type:

- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage payroll runs (`payroll`) | View payslips (`payslip:read`) | - |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "PayslipFile": {
        "description": "A single payslip file with its associated payroll run metadata.",
        "example": {
          "currency": {
            "code": "USD",
            "symbol": "$"
          },
          "id": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
          "name": "payslip.pdf",
          "net_salary": {
            "converted_amount": 460000,
            "converter": "Transferwise",
            "fee": "0.00",
            "rate": "0.92",
            "source_amount": 500000
          },
          "period_end": "2026-04-30",
          "period_start": "2026-04-01"
        },
        "properties": {
          "currency": {
            "$ref": "#/components/schemas/PayslipFileCurrency"
          },
          "id": {
            "$ref": "#/components/schemas/UuidSlug"
          },
          "name": {
            "description": "Original filename of the payslip",
            "example": "payslip.pdf",
            "type": "string"
          },
          "net_salary": {
            "$ref": "#/components/schemas/PayslipFileNetSalary"
          },
          "period_end": {
            "format": "date",
            "nullable": true,
            "type": "string"
          },
          "period_start": {
            "format": "date",
            "nullable": true,
            "type": "string"
          }
        },
        "required": [
          "id",
          "name"
        ],
        "title": "PayslipFile",
        "type": "object"
      },
      "CurrencyCode": {
        "description": "Currency code of the SWIFT fee. Only present when processing_fee is set.",
        "example": "BRL",
        "maxLength": 3,
        "minLength": 3,
        "nullable": true,
        "title": "CurrencyCode",
        "type": "string"
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
      "PayslipFileNetSalary": {
        "additionalProperties": true,
        "description": "Net salary amount including source/converted amounts, currencies and conversion rate. Shape produced by `Tiger.Billing.Value.Amount.build/1`.",
        "example": {
          "converted_amount": 460000,
          "converter": "Transferwise",
          "fee": "0.00",
          "rate": "0.92",
          "source_amount": 500000
        },
        "nullable": true,
        "properties": {
          "converted_amount": {
            "nullable": true,
            "type": "integer"
          },
          "converter": {
            "nullable": true,
            "type": "string"
          },
          "fee": {
            "$ref": "#/components/schemas/Decimal"
          },
          "rate": {
            "$ref": "#/components/schemas/Decimal"
          },
          "source_amount": {
            "nullable": true,
            "type": "integer"
          }
        },
        "title": "PayslipFileNetSalary",
        "type": "object"
      },
      "UuidSlug": {
        "description": "Identifier of the employment being terminated.",
        "example": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
        "format": "uuid",
        "title": "UuidSlug",
        "type": "string"
      },
      "ListPayslipFilesResponse": {
        "description": "Response schema listing many payslip_files",
        "example": {
          "current_page": 1,
          "payslip_files": [
            {
              "currency": {
                "code": "USD",
                "symbol": "$"
              },
              "id": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
              "name": "payslip.pdf",
              "net_salary": {
                "converted_amount": 460000,
                "converter": "Transferwise",
                "fee": "0.00",
                "rate": "0.92",
                "source_amount": 500000
              },
              "period_end": "2026-04-30",
              "period_start": "2026-04-01"
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
              "payslip_files": {
                "items": {
                  "$ref": "#/components/schemas/PayslipFile"
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
        "title": "ListPayslipFilesResponse",
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
      "Decimal": {
        "description": "A decimal number represented as a string to preserve precision. Supports negative values and fractional digits.",
        "example": "-123.456",
        "pattern": "^-?\\d+(\\.\\d+)?$",
        "title": "Decimal",
        "type": "string"
      },
      "PayslipFileCurrency": {
        "example": {
          "code": "USD",
          "symbol": "$"
        },
        "nullable": true,
        "properties": {
          "code": {
            "$ref": "#/components/schemas/CurrencyCode"
          },
          "symbol": {
            "description": "The currency symbol",
            "example": "$",
            "type": "string"
          }
        },
        "required": [
          "code",
          "symbol"
        ],
        "title": "PayslipFileCurrency",
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
    "/v1/employee/payslip-files": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "Returns a paginated list of payslip files belonging to the current employee.\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage payroll runs (`payroll`) | View payslips (`payslip:read`) | - |",
        "operationId": "get_v1_employee_payslip-files",
        "parameters": [
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
                  "$ref": "#/components/schemas/ListPayslipFilesResponse"
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
              "payslip:read",
              "payroll",
              "all:write",
              "all:read"
            ]
          }
        ],
        "summary": "List payslip files for the authenticated employee",
        "tags": [
          "Payslips"
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