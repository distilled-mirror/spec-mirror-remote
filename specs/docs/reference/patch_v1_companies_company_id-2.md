---
updatedAt: 2026-05-27T21:12:30.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Update a company

Given an ID and a request object with new information, updates a company.

### Getting a company and its owner to `active` status
If you created a company using the
[create a company endpoint](#tag/Companies/operation/post_create_company) without all the required
request body parameters, you can use this endpoint to provide the missing data. Once the company
and its owner have all the necessary data, both their statuses will be set to `active` and the company
onboarding will be marked as "completed".

The following constitutes a company with "all the necessary data":
* Complete `address`, with valid `address`, `postal_code`, `country` and `state` parameters (Varies by country. Use the
[show form schema endpoint](#tag/Countries/operation/get_show_form_country) to see which address parameters
are required).
* Company `tax_number` or `registration_number` is not nil
* Company `name` is not nil (already required when creating the company)
* Company has a `desired_currency` in their bank account (already required when creating the company)
* Company has accepted terms of service (already required when creating the company)

## Authentication

This endpoint requires the following token type:

- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage companies (`company_management`) | - | Manage companies (`company:write`) |

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
      "CompanyResponse": {
        "description": "Shows a company",
        "example": {
          "data": {
            "company": {
              "address_details": {
                "address": "1709 Broderick St",
                "address_line_2": "Flat number 123",
                "city": "San Francisco",
                "postal_code": "94115",
                "state": "CA"
              },
              "bank_account_details": {
                "account_holder": "Joe Smith",
                "account_number": "31234123123",
                "account_type": "savings",
                "name": "Bank name",
                "ownership_type": "BUSINESS",
                "routing_number": "123124123"
              },
              "company_owner_email": "te@remote.com",
              "company_owner_name": "Joe Smith",
              "company_owner_user_id": "75619adf-8775-4531-9e7d-5b2cbabdc1a8",
              "country_code": "USA",
              "created_at": "2021-07-15T18:18:17Z",
              "default_legal_entity_credit_risk_status": "no_deposit_required",
              "desired_currency": "USD",
              "external_id": "00001111",
              "id": "e5a8b061-company-id-4c5c81ac885e",
              "name": "Your Company Name",
              "phone_number": "+1123123456",
              "status": "active",
              "terms_of_service_accepted_at": "2021-10-29T12:39:15Z",
              "updated_at": "2021-07-15T18:18:17Z"
            }
          }
        },
        "properties": {
          "data": {
            "properties": {
              "company": {
                "$ref": "#/components/schemas/Company"
              }
            }
          }
        },
        "required": [
          "data"
        ],
        "title": "CompanyResponse",
        "type": "object"
      },
      "Company": {
        "example": {
          "address_details": {
            "address": "1709 Broderick St",
            "address_line_2": "Flat number 123",
            "city": "San Francisco",
            "postal_code": "94115",
            "state": "CA"
          },
          "bank_account_details": {
            "account_holder": "Joe Smith",
            "account_number": "31234123123",
            "account_type": "savings",
            "name": "Bank name",
            "ownership_type": "BUSINESS",
            "routing_number": "123124123"
          },
          "company_owner_email": "te@remote.com",
          "company_owner_name": "Joe Smith",
          "company_owner_user_id": "75619adf-8775-4531-9e7d-5b2cbabdc1a8",
          "country_code": "USA",
          "created_at": "2021-07-15T18:18:17Z",
          "default_legal_entity_credit_risk_status": "no_deposit_required",
          "desired_currency": "USD",
          "external_id": "00001111",
          "id": "e5a8b061-company-id-4c5c81ac885e",
          "name": "Your Company Name",
          "phone_number": "+1123123456",
          "status": "active",
          "terms_of_service_accepted_at": "2021-10-29T12:39:15Z",
          "updated_at": "2021-07-15T18:18:17Z"
        },
        "properties": {
          "address_details": {
            "description": "Fields can vary depending on the country. Please, check the required fields structure using the [Show form schema endpoint](#operation/get_show_form_country).\nUse the desired country and `address_details` as the form name for the placeholders.\nThe response complies with the [JSON Schema](https://developer.remote.com/docs/how-json-schemas-work) specification.\n",
            "type": "object"
          },
          "bank_account_details": {
            "description": "Fields can vary depending on the country. Please, check the required fields structure using the [Show form schema endpoint](#operation/get_show_form_country).\nUse the desired country and `bank_account_details` as the form name for the placeholders.\nThe response complies with the [JSON Schema](https://developer.remote.com/docs/how-json-schemas-work) specification.\n",
            "type": "object"
          },
          "company_owner_email": {
            "description": "The email address of the company owner who administers the Remote account.",
            "format": "email",
            "type": "string"
          },
          "company_owner_name": {
            "description": "The full name of the company owner. Cannot be changed after company creation.",
            "type": "string"
          },
          "company_owner_user_id": {
            "description": "The unique identifier (UUID) of the company owner's user account on Remote.",
            "type": "string"
          },
          "country_code": {
            "description": "The ISO 3166-1 3-letter country code where the company is registered.",
            "type": "string"
          },
          "created_at": {
            "description": "The timestamp when the company was created on Remote.",
            "format": "date-time",
            "type": "string"
          },
          "default_legal_entity_credit_risk_status": {
            "description": "The credit risk status of the company default legal entity.\n- `not_started`: The credit risk assessment has not started yet.\n- `ready`: The credit risk assessment is ready to be started.\n- `in_progress`: The automated credit risk assessment is in progress.\n- `referred`: The credit risk assessment has been referred to a human reviewer.\n- `fail`: The credit risk assessment has failed and the company will be archived.\n- `deposit_required`: The company default legal entity requires a deposit before onboarding new employees.\n- `no_deposit_required`: The company default legal entity does not require a deposit before onboarding new employees.\n",
            "enum": [
              "not_started",
              "ready",
              "in_progress",
              "referred",
              "fail",
              "deposit_required",
              "no_deposit_required"
            ],
            "type": "string"
          },
          "desired_currency": {
            "description": "The ISO 4217 currency code the company prefers for billing and invoicing (e.g., \"USD\", \"EUR\").",
            "type": "string"
          },
          "external_id": {
            "description": "A unique reference code for this company in a non-Remote system. Null if not set.",
            "nullable": true,
            "type": "string"
          },
          "id": {
            "description": "The unique identifier (UUID) of the company.",
            "type": "string"
          },
          "name": {
            "description": "The company's registered name. Can only be changed while the company is in `pending` status.",
            "type": "string"
          },
          "phone_number": {
            "description": "The company's contact phone number.",
            "type": "string"
          },
          "registration_number": {
            "description": "The company's business registration number. Null if not provided. Can only be set while the company is in `pending` status.",
            "nullable": true,
            "type": "string"
          },
          "status": {
            "description": "The company status determines what a company is allowed to do:\n- `pending`: The company has been created and the company owner invited. Remote is waiting for the company owner to complete onboarding.\n- `review`: The company is under review. In rare occasions, a company may not automatically get created in `active` status because Remote needs to\n  manually review the company that was created. The company will become `active` once the review is completed and no further action is necessary\n  through the Remote API.\n- `active`: The company owner has completed onboarding and the company is ready to employ.\n- `archived`: The company is no longer active on the Remote platform and no changes can be made to the company.\n",
            "enum": [
              "pending",
              "review",
              "active",
              "archived"
            ],
            "type": "string"
          },
          "tax_number": {
            "description": "The company's tax identification number. Null if not provided. Can only be set while the company is in `pending` status.",
            "nullable": true,
            "type": "string"
          },
          "terms_of_service_accepted_at": {
            "description": "The timestamp when the company owner accepted Remote's Terms of Service.",
            "format": "date-time",
            "type": "string"
          },
          "updated_at": {
            "description": "The timestamp when the company record was last updated.",
            "format": "date-time",
            "type": "string"
          }
        },
        "required": [
          "address_details",
          "company_owner_email",
          "company_owner_user_id",
          "country_code",
          "created_at",
          "desired_currency",
          "id",
          "name",
          "status",
          "updated_at",
          "terms_of_service_accepted_at",
          "default_legal_entity_credit_risk_status"
        ],
        "title": "Company",
        "type": "object"
      },
      "TooManyRequestsResponse": {
        "description": "Returned when the API rate limit has been exceeded (HTTP 429). Wait before retrying. Check the `Retry-After` response header for the recommended wait time.",
        "example": {
          "message": "Too many requests"
        },
        "properties": {
          "message": {
            "pattern": "Too many requests",
            "type": "string"
          }
        },
        "title": "TooManyRequestsResponse",
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
      "UpdateCompanyParams": {
        "example": {
          "address_details": {
            "address": "1709 Broderick St",
            "address_line_2": "Flat number 123",
            "city": "San Francisco",
            "postal_code": "94115",
            "state": "CA"
          },
          "bank_account_details": {
            "account_holder": "Joe Smith",
            "account_number": "31234123123",
            "account_type": "savings",
            "name": "Bank name",
            "ownership_type": "BUSINESS",
            "routing_number": "123124123"
          },
          "country_code": "USA",
          "desired_currency": "USD",
          "name": "Tech Vision",
          "phone_number": "+11123123456",
          "tax_number": "123456789"
        },
        "properties": {
          "address_details": {
            "description": "Fields can vary depending on the country. Please, check the required fields structure using the [Show form schema endpoint](#operation/get_show_form_country).\nUse the desired country and `address_details` as the form name for the placeholders.\nThe response complies with the [JSON Schema](https://developer.remote.com/docs/how-json-schemas-work) specification.\n",
            "type": "object"
          },
          "bank_account_details": {
            "description": "Fields can vary depending on the country. Please, check the required fields structure using the [Show form schema endpoint](#operation/get_show_form_country).\nUse the desired country and `bank_account_details` as the form name for the placeholders.\nThe response complies with the [JSON Schema](https://developer.remote.com/docs/how-json-schemas-work) specification.\n",
            "type": "object"
          },
          "country_code": {
            "description": "Country of company address",
            "type": "string"
          },
          "desired_currency": {
            "description": "Desired currency for invoicing and displaying converted salaries in Remote UI regardless of the employee's country.\n\nThis field is only accepted if company is in status `pending`. Please contact Remote if you wish to update it.\n",
            "enum": [
              "AUD",
              "CAD",
              "CHF",
              "DKK",
              "EUR",
              "GBP",
              "JPY",
              "NOK",
              "NZD",
              "SEK",
              "SGD",
              "USD"
            ],
            "type": "string"
          },
          "name": {
            "description": "This field is only accepted if company is in status `pending`. Please contact Remote if you wish to update it.\n",
            "type": "string"
          },
          "phone_number": {
            "description": "A phone number the company can be contacted with.",
            "type": "string"
          },
          "registration_number": {
            "description": "The company registration number. This field or tax_number (but not both) should be submitted.\n\nThis field is only accepted if company is in status `pending`.\n",
            "type": "string"
          },
          "tax_number": {
            "description": "  The tax identifier of the company. This field or registration_number (but not both) should be submitted.\n\n  This field is only accepted if company is in status `pending`.\n",
            "type": "string"
          }
        },
        "title": "UpdateCompanyParams",
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
    "title": "Companies",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/companies/{company_id}": {
      "patch": {
        "callbacks": {},
        "deprecated": false,
        "description": "Given an ID and a request object with new information, updates a company.\n\n### Getting a company and its owner to `active` status\nIf you created a company using the\n[create a company endpoint](#tag/Companies/operation/post_create_company) without all the required\nrequest body parameters, you can use this endpoint to provide the missing data. Once the company\nand its owner have all the necessary data, both their statuses will be set to `active` and the company\nonboarding will be marked as \"completed\".\n\nThe following constitutes a company with \"all the necessary data\":\n* Complete `address`, with valid `address`, `postal_code`, `country` and `state` parameters (Varies by country. Use the\n[show form schema endpoint](#tag/Countries/operation/get_show_form_country) to see which address parameters\nare required).\n* Company `tax_number` or `registration_number` is not nil\n* Company `name` is not nil (already required when creating the company)\n* Company has a `desired_currency` in their bank account (already required when creating the company)\n* Company has accepted terms of service (already required when creating the company)\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage companies (`company_management`) | - | Manage companies (`company:write`) |",
        "operationId": "patch_v1_companies_company_id (2)",
        "parameters": [
          {
            "description": "Requires a Company-scoped access token obtained through the Authorization Code flow or the Refresh Token flow.\n\nThe refresh token needs to have been obtained through the Authorization Code flow.\n",
            "example": "Bearer <COMPANY-SCOPED ACCESS TOKEN>",
            "in": "header",
            "name": "Authorization",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "description": "Version of the address_details form schema",
            "example": 1,
            "in": "query",
            "name": "address_details_json_schema_version",
            "required": false,
            "schema": {
              "default": "latest",
              "oneOf": [
                {
                  "description": "Specific version number",
                  "minimum": 1,
                  "type": "integer"
                },
                {
                  "description": "Use latest version",
                  "enum": [
                    "latest"
                  ],
                  "type": "string"
                }
              ]
            }
          },
          {
            "description": "Version of the bank_account_details form schema",
            "example": 1,
            "in": "query",
            "name": "bank_account_details_json_schema_version",
            "required": false,
            "schema": {
              "default": "latest",
              "oneOf": [
                {
                  "description": "Specific version number",
                  "minimum": 1,
                  "type": "integer"
                },
                {
                  "description": "Use latest version",
                  "enum": [
                    "latest"
                  ],
                  "type": "string"
                }
              ]
            }
          },
          {
            "description": "Company ID\n",
            "example": "0a8s2d1-company-id-2e3f4th",
            "in": "path",
            "name": "company_id",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/UpdateCompanyParams"
              }
            }
          },
          "description": "Update Company params",
          "required": false
        },
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/CompanyResponse"
                }
              }
            },
            "description": "Success"
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
          },
          "429": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/TooManyRequestsResponse"
                }
              }
            },
            "description": "Too many requests"
          }
        },
        "security": [
          {
            "OAuth2ClientCredentials": [
              "https://gateway.remote.com/company.manage",
              "company:write",
              "company_management",
              "all:write"
            ]
          }
        ],
        "summary": "Update a company",
        "tags": [
          "Company Management"
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
  "tags": [
    {
      "name": "Companies"
    }
  ],
  "webhooks": {
    "company.activated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company is activated.",
        "operationId": "company.activated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "ba310525-9282-40c9-8977-14d844bf891a",
                  "event_type": "company.activated"
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
        "summary": "company.activated",
        "tags": [
          "Companies"
        ]
      }
    },
    "company.archived": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company is archived.",
        "operationId": "company.archived",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "ba310525-9282-40c9-8977-14d844bf891a",
                  "event_type": "company.archived"
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
        "summary": "company.archived",
        "tags": [
          "Companies"
        ]
      }
    },
    "company.eor_hiring.additional_information_required": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when additional information is required for the EOR hiring process.",
        "operationId": "company.eor_hiring.additional_information_required",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "ba310525-9282-40c9-8977-14d844bf891a",
                  "event_type": "company.eor_hiring.additional_information_required"
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
        "summary": "company.eor_hiring.additional_information_required",
        "tags": [
          "Companies"
        ]
      }
    },
    "company.eor_hiring.no_reserve_payment_requested": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the credit risk status is no reserve payment requested.",
        "operationId": "company.eor_hiring.no_reserve_payment_requested",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "ba310525-9282-40c9-8977-14d844bf891a",
                  "event_type": "company.eor_hiring.no_reserve_payment_requested"
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
        "summary": "company.eor_hiring.no_reserve_payment_requested",
        "tags": [
          "Companies"
        ]
      }
    },
    "company.eor_hiring.referred": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the credit risk status is referred.",
        "operationId": "company.eor_hiring.referred",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "ba310525-9282-40c9-8977-14d844bf891a",
                  "event_type": "company.eor_hiring.referred"
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
        "summary": "company.eor_hiring.referred",
        "tags": [
          "Companies"
        ]
      }
    },
    "company.eor_hiring.reserve_payment_requested": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the credit risk status is reserve payment requested.",
        "operationId": "company.eor_hiring.reserve_payment_requested",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "ba310525-9282-40c9-8977-14d844bf891a",
                  "event_type": "company.eor_hiring.reserve_payment_requested"
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
        "summary": "company.eor_hiring.reserve_payment_requested",
        "tags": [
          "Companies"
        ]
      }
    },
    "company.eor_hiring.verification_completed": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company verification is completed.",
        "operationId": "company.eor_hiring.verification_completed",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "f2a1b3c4-d5e6-7f8g-9h0i-j1k2l3m4n5o6",
                  "event_type": "company.eor_hiring.verification_completed"
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
        "summary": "company.eor_hiring.verification_completed",
        "tags": [
          "Companies"
        ]
      }
    },
    "company.manager_created": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company manager is created.",
        "operationId": "company.manager_created",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
                  "event_type": "company.manager_created",
                  "user_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99"
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
                  "user_id": {
                    "description": "The unique identifier of the related user.",
                    "type": "string"
                  }
                },
                "required": [
                  "company_id",
                  "user_id",
                  "event_type"
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
        "summary": "company.manager_created",
        "tags": [
          "Company Management"
        ]
      }
    },
    "company.manager_deleted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company manager is deleted.",
        "operationId": "company.manager_deleted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
                  "event_type": "company.manager_deleted",
                  "user_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99"
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
                  "user_id": {
                    "description": "The unique identifier of the related user.",
                    "type": "string"
                  }
                },
                "required": [
                  "company_id",
                  "user_id",
                  "event_type"
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
        "summary": "company.manager_deleted",
        "tags": [
          "Company Management"
        ]
      }
    },
    "company.manager_updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company manager is updated.",
        "operationId": "company.manager_updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
                  "event_type": "company.manager_updated",
                  "user_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99"
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
                  "user_id": {
                    "description": "The unique identifier of the related user.",
                    "type": "string"
                  }
                },
                "required": [
                  "company_id",
                  "user_id",
                  "event_type"
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
        "summary": "company.manager_updated",
        "tags": [
          "Company Management"
        ]
      }
    },
    "company.owner_changed": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company's Account Owner role is transferred to a different user, including rotation and demotion scenarios.",
        "operationId": "company.owner_changed",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
                  "event_type": "company.owner_changed",
                  "new_owner_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "previous_owner_id": "9a1b2c3d-4e5f-6a7b-8c9d-0e1f2a3b4c5d"
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
                  "new_owner_id": {
                    "description": "The unique identifier of the user who is now the Account Owner.",
                    "type": "string"
                  },
                  "previous_owner_id": {
                    "description": "The unique identifier of the user who was previously the Account Owner. Null if there was no previous owner.",
                    "nullable": true,
                    "type": "string"
                  }
                },
                "required": [
                  "company_id",
                  "new_owner_id",
                  "event_type"
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
        "summary": "company.owner_changed",
        "tags": [
          "Company Management"
        ]
      }
    },
    "company.partner_offboarded": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company is offboarded from a partner.",
        "operationId": "company.partner_offboarded",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "ba310525-9282-40c9-8977-14d844bf891a",
                  "event_type": "company.partner_offboarded",
                  "offboarding_date": "2021-01-01T00:00:00Z"
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
                  "offboarding_date": {
                    "description": "The date of the offboarding event.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "company_id",
                  "offboarding_date"
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
        "summary": "company.partner_offboarded",
        "tags": [
          "Companies"
        ]
      }
    },
    "employment_company_structure_node.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment company structure node is updated.",
        "operationId": "employment_company_structure_node.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "company_structure_node_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment_company_structure_node.updated"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "company_structure_node_id": {
                    "description": "The unique identifier of the company structure node.",
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
                  "company_structure_node_id",
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
        "summary": "employment_company_structure_node.updated",
        "tags": [
          "Org Structure"
        ]
      }
    }
  }
}
```