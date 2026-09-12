---
updatedAt: 2026-05-27T21:12:30.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Create a company

  Creates a new company.

  ### Creating a company with only the required request body parameters
  When you call this endpoint and omit all the optional parameters in the request body,
  the following resources get created upon a successful response:
  * A new company with status `pending`.
  * A company owner for the new company with status `initiated`.

  See the [update a company endpoint](#tag/Companies/operation/patch_update_company) for
  more details on how to get your company and its owner to `active` status.

  If you'd like to create a company and its owner with `active` status in a single request,
  please provide the optional `address_details` parameter as well.

  ### Accepting the Terms of Service

  A required step for creating a company in Remote is to accept our Terms of Service (ToS).

  Company managers need to be aware of our Terms of Service and Privacy Policy,
  hence **it's the responsibility of our partners to advise and ensure company managers read
  and accept the ToS**. The terms have to be accepted only once, before creating a company,
  and the Remote API will collect the acceptance timestamp as its confirmation.

  To ensure users read the most recent version of Remote's Terms of Service, their **acceptance
  must be done within the last fifteen minutes prior the company creation action**.

  To retrieve this information, partners can provide an element with any text and a description
  explaining that by performing that action they are accepting Remote's Term of Service. For
  instance, the partner can add a checkbox or a "Create Remote Account" button followed by a
  description saying "By creating an account, you agree to
  [Remote's Terms of Service](https://remote.com/terms-of-service). Also see Remote's
  [Privacy Policy](https://remote.com/privacy-policy)".

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
      "ClientCredentialsResponse": {
        "allOf": [
          {
            "$ref": "#/components/schemas/BaseTokenResponse"
          }
        ],
        "example": {
          "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
          "expires_in": 7200,
          "token_type": "Bearer"
        },
        "title": "ClientCredentialsResponse",
        "type": "object"
      },
      "AuthorizationCodeResponse": {
        "allOf": [
          {
            "$ref": "#/components/schemas/BaseTokenResponse"
          },
          {
            "example": {
              "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
              "company_id": "6e60f5f9-e6a6-4b04-b13c-84bced848bab",
              "expires_in": 7200,
              "refresh_token": "b480036a-d229-49ef-a606-7e8fba58a5eb",
              "token_type": "Bearer",
              "user_id": "6550e536-8655-4bce-8bd9-b295f786ad71"
            },
            "properties": {
              "company_id": {
                "description": "The ID of the connected company.",
                "type": "string"
              },
              "refresh_token": {
                "description": "The refresh token. This token must be stored and used for issuing new access tokens for managing the company's resources.",
                "type": "string"
              },
              "user_id": {
                "description": "The ID of the user who connected the company.",
                "type": "string"
              }
            },
            "type": "object"
          }
        ],
        "example": {
          "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
          "company_id": "6e60f5f9-e6a6-4b04-b13c-84bced848bab",
          "expires_in": 7200,
          "refresh_token": "b480036a-d229-49ef-a606-7e8fba58a5eb",
          "token_type": "Bearer",
          "user_id": "6550e536-8655-4bce-8bd9-b295f786ad71"
        },
        "title": "AuthorizationCodeResponse",
        "type": "object"
      },
      "CompanyAlreadyExistsErrorResponse": {
        "description": "Error returned when a company with matching criteria already exists",
        "example": {
          "data": {
            "code": "resource_already_exists",
            "message": "The company with the provided EIN is already registered.",
            "resource_id": "d1bb9535-3296-4240-8a67-81475bd24e80",
            "resource_type": "company_creation"
          }
        },
        "properties": {
          "code": {
            "pattern": "resource_already_exists",
            "type": "string"
          },
          "message": {
            "pattern": "The company with the provided EIN is already registered.",
            "type": "string"
          },
          "resource_id": {
            "format": "uuid",
            "type": "string"
          },
          "resource_type": {
            "pattern": "company_creation",
            "type": "string"
          }
        },
        "title": "CompanyAlreadyExistsErrorResponse",
        "type": "object"
      },
      "CompanyCreationResponse": {
        "example": {
          "data": {
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
          }
        },
        "properties": {
          "data": {
            "anyOf": [
              {
                "$ref": "#/components/schemas/CompanyResponse"
              },
              {
                "$ref": "#/components/schemas/CompanyWithTokensResponse"
              }
            ]
          }
        },
        "title": "CompanyCreationResponse",
        "type": "object"
      },
      "RefreshTokenResponse": {
        "allOf": [
          {
            "$ref": "#/components/schemas/BaseTokenResponse"
          },
          {
            "example": {
              "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
              "expires_in": 7200,
              "refresh_token": "b480036a-d229-49ef-a606-7e8fba58a5eb",
              "token_type": "Bearer"
            },
            "properties": {
              "refresh_token": {
                "description": "The refresh token",
                "type": "string"
              }
            },
            "type": "object"
          }
        ],
        "example": {
          "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
          "expires_in": 7200,
          "refresh_token": "b480036a-d229-49ef-a606-7e8fba58a5eb",
          "token_type": "Bearer"
        },
        "title": "RefreshTokenResponse",
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
      "OAuth2Tokens": {
        "anyOf": [
          {
            "$ref": "#/components/schemas/AuthorizationCodeResponse"
          },
          {
            "$ref": "#/components/schemas/ClientCredentialsResponse"
          },
          {
            "$ref": "#/components/schemas/RefreshTokenResponse"
          }
        ],
        "example": {
          "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
          "company_id": "6e60f5f9-e6a6-4b04-b13c-84bced848bab",
          "expires_in": 7200,
          "refresh_token": "b480036a-d229-49ef-a606-7e8fba58a5eb",
          "token_type": "Bearer",
          "user_id": "6550e536-8655-4bce-8bd9-b295f786ad71"
        },
        "title": "OAuth2Tokens",
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
      "CompanyWithTokensResponse": {
        "description": "Shows a company with its refresh and access tokens. Please contact Remote if you need the tokens when creating a company.",
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
            },
            "tokens": {
              "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
              "company_id": "6e60f5f9-e6a6-4b04-b13c-84bced848bab",
              "expires_in": 7200,
              "refresh_token": "b480036a-d229-49ef-a606-7e8fba58a5eb",
              "token_type": "Bearer",
              "user_id": "6550e536-8655-4bce-8bd9-b295f786ad71"
            }
          }
        },
        "properties": {
          "company": {
            "$ref": "#/components/schemas/Company"
          },
          "tokens": {
            "$ref": "#/components/schemas/OAuth2Tokens"
          }
        },
        "title": "CompanyWithTokensResponse",
        "type": "object"
      },
      "CreateCompanyParams": {
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
          "company_owner_email": "ceo@techvision.com",
          "company_owner_name": "Joe Smith",
          "country_code": "USA",
          "desired_currency": "USD",
          "external_id": "00001111",
          "name": "Tech Vision",
          "phone_number": "+11123123456",
          "tax_number": "123456789",
          "terms_of_service_accepted_at": "2022-05-05 15:03:45Z"
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
            "description": "The company owner email.\n\nThis value cannot be changed once set.\n",
            "format": "email",
            "type": "string"
          },
          "company_owner_name": {
            "description": "The company owner name.\n\nThis value cannot be changed from the Remote API once set.\n",
            "type": "string"
          },
          "country_code": {
            "description": "3-letter country code of the country the company address is located in.\n\nFor a list of countries supported through the Remote API, make a call to the [list countries endpoint](#tag/Countries/operation/get_supported_country). This endpoint will also include the 3-letter country codes you can use for this field.\n",
            "type": "string"
          },
          "desired_currency": {
            "description": "Desired currency for invoicing and displaying converted salaries in Remote UI regardless of the employee's country.",
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
          "email_domain": {
            "description": "The domain of the company. Use this field to specify the company domain name when it's different from the domain in the company owner's email.",
            "type": "string"
          },
          "external_id": {
            "description": "Id of the company as represented in the external partner system.",
            "type": "string"
          },
          "name": {
            "description": "The company name",
            "type": "string"
          },
          "phone_number": {
            "description": "A phone number the company can be contacted with.",
            "type": "string"
          },
          "registration_number": {
            "description": "The company registration number. This field or `tax_number` (but not both) should be submitted.",
            "type": "string"
          },
          "tax_number": {
            "description": "The tax identifier of the company. This field or `registration_number` (but not both) should be submitted.",
            "type": "string"
          },
          "terms_of_service_accepted_at": {
            "description": "Date and time the Terms of Service were accepted. To ensure users read the most recent version of Remote's Terms of Service, their action cannot have been done more than fifteen minutes ago. The UTC offset must be included in the ISO 8601 format: `YYYY-MM-DD HOURS:MINUTES:SECONDSZ`",
            "format": "date-time",
            "type": "string"
          }
        },
        "required": [
          "company_owner_email",
          "company_owner_name",
          "country_code",
          "desired_currency",
          "name",
          "terms_of_service_accepted_at"
        ],
        "title": "CreateCompanyParams",
        "type": "object"
      },
      "BaseTokenResponse": {
        "example": {
          "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
          "expires_in": 7200,
          "token_type": "Bearer"
        },
        "properties": {
          "access_token": {
            "description": "A JWT token.",
            "type": "string"
          },
          "expires_in": {
            "description": "Number of seconds until token is expired.",
            "format": "int32",
            "type": "integer"
          },
          "token_type": {
            "description": "The type of the token. For now, always `Bearer`.",
            "type": "string"
          }
        },
        "title": "BaseTokenResponse",
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
      "CompanyNotEligibleForCreationErrorResponse": {
        "description": "Error returned when the company already have employees in countries supported by the integration.",
        "example": {
          "data": {
            "code": "resource_not_eligible",
            "message": "The company already have employees in integration supported countries.",
            "resource_id": "d1bb9535-3296-4240-8a67-81475bd24e80",
            "resource_type": "company_creation"
          }
        },
        "properties": {
          "code": {
            "pattern": "resource_not_eligible",
            "type": "string"
          },
          "message": {
            "pattern": "The company already have employees in integration supported countries.",
            "type": "string"
          },
          "resource_id": {
            "format": "uuid",
            "type": "string"
          },
          "resource_type": {
            "pattern": "company_creation",
            "type": "string"
          }
        },
        "title": "CompanyNotEligibleForCreationErrorResponse",
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
      },
      "CompanyCreationConflictErrorResponse": {
        "example": {
          "data": {
            "message": "The company with the provided EIN is already registered."
          }
        },
        "properties": {
          "message": {
            "oneOf": [
              {
                "$ref": "#/components/schemas/CompanyAlreadyExistsErrorResponse"
              },
              {
                "$ref": "#/components/schemas/CompanyNotEligibleForCreationErrorResponse"
              }
            ]
          }
        },
        "title": "CompanyCreationConflictErrorResponse",
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
    "/v1/companies": {
      "post": {
        "callbacks": {},
        "deprecated": false,
        "description": "  Creates a new company.\n\n  ### Creating a company with only the required request body parameters\n  When you call this endpoint and omit all the optional parameters in the request body,\n  the following resources get created upon a successful response:\n  * A new company with status `pending`.\n  * A company owner for the new company with status `initiated`.\n\n  See the [update a company endpoint](#tag/Companies/operation/patch_update_company) for\n  more details on how to get your company and its owner to `active` status.\n\n  If you'd like to create a company and its owner with `active` status in a single request,\n  please provide the optional `address_details` parameter as well.\n\n  ### Accepting the Terms of Service\n\n  A required step for creating a company in Remote is to accept our Terms of Service (ToS).\n\n  Company managers need to be aware of our Terms of Service and Privacy Policy,\n  hence **it's the responsibility of our partners to advise and ensure company managers read\n  and accept the ToS**. The terms have to be accepted only once, before creating a company,\n  and the Remote API will collect the acceptance timestamp as its confirmation.\n\n  To ensure users read the most recent version of Remote's Terms of Service, their **acceptance\n  must be done within the last fifteen minutes prior the company creation action**.\n\n  To retrieve this information, partners can provide an element with any text and a description\n  explaining that by performing that action they are accepting Remote's Term of Service. For\n  instance, the partner can add a checkbox or a \"Create Remote Account\" button followed by a\n  description saying \"By creating an account, you agree to\n  [Remote's Terms of Service](https://remote.com/terms-of-service). Also see Remote's\n  [Privacy Policy](https://remote.com/privacy-policy)\".\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage companies (`company_management`) | - | Manage companies (`company:write`) |",
        "operationId": "post_v1_companies",
        "parameters": [
          {
            "description": "Requires a client credentials access token obtained through the Client Credentials flow or the Refresh Token flow.\n\nThe refresh token needs to have been obtained through the Client Credentials flow.\n",
            "example": "Bearer <CLIENT-CREDENTIALS ACCESS TOKEN>",
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
            "description": "Complementary action(s) to perform when creating a company:\n\n- `get_oauth_access_tokens` returns the user's access and refresh tokens\n- `send_create_password_email ` sends a reset password token to the company owner's email so they can log in using Remote UI (not needed if integration plans to use SSO only)\n\nIf `action` contains `send_create_password_email` you can redirect the user to [https://employ.remote.com/api-integration-new-password-send](https://employ.remote.com/api-integration-new-password-send)\n",
            "example": "get_oauth_access_tokens,send_create_password_email",
            "in": "query",
            "name": "action",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "description": "Whether the request should be performed async\n",
            "example": true,
            "in": "query",
            "name": "async",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "description": "Scope of the access token\n",
            "example": "file:read timeoff:create",
            "in": "query",
            "name": "scope",
            "required": false,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/CreateCompanyParams"
              }
            }
          },
          "description": "Create Company params",
          "required": false
        },
        "responses": {
          "201": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/CompanyCreationResponse"
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
          "409": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/CompanyCreationConflictErrorResponse"
                }
              }
            },
            "description": "Conflict"
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
            "description": "Unprocessable Entity"
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
        "summary": "Create a company",
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