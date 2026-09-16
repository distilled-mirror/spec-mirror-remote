---
updatedAt: 2026-05-27T21:26:44.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Token

Endpoint to exchange tokens in the Authorization Code, Assertion Flow, Client Credentials and Refresh Token flows

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
            "description": "The client id generated during registration",
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
          "grant_type",
          "client_id"
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
        "description": "The assertion token is a JWT token that contains the following claims:\n\n- `sub`: The subject of the token, in one of the following formats:\n  - `urn:remote-api:employment:<employment_id>` — mints an **employee-role** access token whose `sub` is the employment owner's user slug. Scopes are restricted to those valid for the employee role (e.g. `personal_detail:read`, `timeoff:write`).\n  - `urn:remote-api:employee:employment:<employment_id>` — same as above; the recommended format for new integrations. Use this when issuing a token on behalf of an employee so they can submit their own onboarding data (e.g. `PUT /v1/employee/address`).\n  - `urn:remote-api:company-manager:user:<user_id>` — mints a **company_manager-role** access token. Scopes are restricted to those valid for the company-manager role.\n\n- `iss`: The issuer of the token, which is the client ID\n- `aud`: The audience of the token, which is the OAuth audience\n- `exp`: The expiration time of the token (max 10 minutes in the future)\n- `iat`: The issued at time of the token\n- `scope`: The scope of the token (space-separated). Optional. If omitted, the minted access token defaults to `all:write` for the subject's role. If provided, every scope must be valid for the subject's role or the assertion is rejected.\n\nThe assertion must be signed with the client secret (HS256).\n\n**Example — minting an employee token to submit a residential address:**\n\n```\nsub:   urn:remote-api:employee:employment:emp_2t3h9\niss:   <your client_id>\naud:   <configured OAuth audience>\nexp:   <now + 300 seconds>\niat:   <now>\nscope: address:write\n```\n\nThe resulting access token can be used at `PUT /v1/employee/address` to submit the address for that employment.\n",
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
        "description": "Endpoint to exchange tokens in the Authorization Code, Assertion Flow, Client Credentials and Refresh Token flows\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Basic authentication** (`BasicAuth`) — using the `CLIENT_ID` as login and the `CLIENT_SECRET` as password. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).",
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