---
updatedAt: 2026-05-27T21:26:44.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# Token

Endpoint to exchange tokens in the Authorization Code, Assertion Flow, Client Credentials and Refresh Token flows.

For backward compatibility, this endpoint returns `400` with `invalid_grant` in some cases where
RFC 6749 would use `invalid_client` (invalid client credentials) or `unauthorized_client`
(the integration is not allowed to use the grant type). Use `error_description` to tell these
cases apart.

## Authentication

This endpoint requires the following token type:

- **Basic authentication** (`BasicAuth`) — using the `CLIENT_ID` as login and the `CLIENT_SECRET` as password. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

# OpenAPI definition

````json
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
      "OAuth2TokenParams": {
        "example": {
          "code": "eyJhbG...xb6H0",
          "grant_type": "authorization_code"
        },
        "oneOf": [
          {
            "$ref": "#/components/schemas/AuthorizationCodeParams"
          },
          {
            "$ref": "#/components/schemas/ClientCredentialsParams"
          },
          {
            "$ref": "#/components/schemas/RefreshTokenParams"
          },
          {
            "$ref": "#/components/schemas/AssertionTokenParams"
          }
        ],
        "title": "OAuth2TokenParams",
        "type": "object"
      },
      "RefreshTokenParams": {
        "example": {
          "grant_type": "refresh_token",
          "refresh_token": "b480036a-d229-49ef-a606-7e8fba58a5eb"
        },
        "properties": {
          "grant_type": {
            "description": "The Authorization flow",
            "enum": [
              "refresh_token"
            ],
            "type": "string"
          },
          "refresh_token": {
            "description": "The refresh token generated in the Authorization Code flow",
            "type": "string"
          }
        },
        "required": [
          "grant_type",
          "refresh_token"
        ],
        "title": "RefreshTokenParams",
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
      "ClientCredentialsParams": {
        "example": {
          "client_id": "<client_id>",
          "grant_type": "client_credentials"
        },
        "properties": {
          "client_id": {
            "description": "The client id generated during registration. Optional here - it can instead be sent via the Basic auth header, which is always required for this grant type.",
            "type": "string"
          },
          "grant_type": {
            "description": "The Authorization flow",
            "enum": [
              "client_credentials"
            ],
            "type": "string"
          }
        },
        "required": [
          "grant_type"
        ],
        "title": "ClientCredentialsParams",
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
      "AssertionTokenParams": {
        "description": "The assertion token is a JWT token that contains the following claims:\n\n- `sub`: The subject of the token, in one of the following formats:\n  - `urn:remote-api:employment:<employment_id>` — mints an **employee-role** access token whose `sub` is the employment owner's user slug. Scopes are restricted to those valid for the employee role (e.g. `personal_detail:read`, `timeoff:write`).\n  - `urn:remote-api:employee:employment:<employment_id>` — same as above; the recommended format for new integrations. Use this when issuing a token on behalf of an employee so they can submit their own onboarding data (e.g. `PUT /v1/employee/address`).\n  - `urn:remote-api:company-manager:user:<user_id>` — mints a **company_manager-role** access token. Scopes are restricted to those valid for the company-manager role.\n\n- `iss`: The issuer of the token, which is the client ID\n- `aud`: The audience of the token, which is the OAuth audience\n- `exp`: The expiration time of the token (max 10 minutes in the future)\n- `iat`: The issued at time of the token\n- `scope`: The scope of the token (space-separated). Optional. If omitted, the minted access token defaults to `all:write` for the subject's role. If provided, every scope must be valid for the subject's role or the assertion is rejected.\n\nThe assertion must be signed with the client secret (HS256).\n\nRemote must allow the integration to act on behalf of users, and the integration must manage the subject's company.\nRemote can also limit an integration to grants that carry a user's consent, such as the Authorization Code flow;\nthis grant is then refused.\n\n**Example — minting an employee token to submit a residential address:**\n\n```\nsub:   urn:remote-api:employee:employment:emp_2t3h9\niss:   <your client_id>\naud:   <configured OAuth audience>\nexp:   <now + 300 seconds>\niat:   <now>\nscope: address:write\n```\n\nThe resulting access token can be used at `PUT /v1/employee/address` to submit the address for that employment.\n",
        "example": {
          "assertion": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.cThIIoDvwdueQB468K5xDc5633seEFoqwxjF_xSJyQQ",
          "grant_type": "urn:ietf:params:oauth:grant-type:jwt-bearer"
        },
        "properties": {
          "assertion": {
            "description": "The assertion token",
            "type": "string"
          },
          "grant_type": {
            "description": "The Assertion flow grant type",
            "enum": [
              "urn:ietf:params:oauth:grant-type:jwt-bearer"
            ],
            "type": "string"
          }
        },
        "required": [
          "grant_type",
          "assertion"
        ],
        "title": "AssertionTokenParams",
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
      "AuthorizationCodeParams": {
        "example": {
          "code": "eyJhbG...xb6H0",
          "grant_type": "authorization_code"
        },
        "properties": {
          "code": {
            "description": "The authorization code generated in Authorization Code flow",
            "type": "string"
          },
          "grant_type": {
            "description": "The Authorization flow",
            "enum": [
              "authorization_code"
            ],
            "type": "string"
          }
        },
        "required": [
          "grant_type",
          "code"
        ],
        "title": "AuthorizationCodeParams",
        "type": "object"
      }
    },
    "securitySchemes": {
      "BasicAuth": {
        "description": "Authenticate using the basic authentication for partners.\n\nUse the CLIENT_ID as login and CLIENT_SECRET as password.\n",
        "scheme": "basic",
        "type": "http"
      },
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
      }
    }
  },
  "info": {
    "title": "Getting Started",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/auth/oauth2/token": {
      "post": {
        "callbacks": {},
        "deprecated": false,
        "description": "Endpoint to exchange tokens in the Authorization Code, Assertion Flow, Client Credentials and Refresh Token flows.\n\nFor backward compatibility, this endpoint returns `400` with `invalid_grant` in some cases where\nRFC 6749 would use `invalid_client` (invalid client credentials) or `unauthorized_client`\n(the integration is not allowed to use the grant type). Use `error_description` to tell these\ncases apart.\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Basic authentication** (`BasicAuth`) — using the `CLIENT_ID` as login and the `CLIENT_SECRET` as password. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).",
        "operationId": "post_auth_oauth2_token",
        "parameters": [],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/OAuth2TokenParams"
              }
            }
          },
          "description": "OAuth2Token",
          "required": false
        },
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/OAuth2Tokens"
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
            "BasicAuth": []
          }
        ],
        "summary": "Token",
        "tags": [
          "OAuth2"
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
````