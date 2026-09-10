---
updatedAt: 2026-05-27T21:23:52.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get Onboarding Reserves Status for Employment

Returns the onboarding reserves status for a specific employment.

The status is the same as the credit risk status but takes the onboarding reserves policies into account.

## Authentication

This endpoint accepts any one of the following token types:

- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).
- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage employments (`employments`) | View employments (`employment:read`) | Manage employments (`employment:write`) |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
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
      "OnboardingReservesStatus": {
        "additionalProperties": false,
        "example": {
          "policies": [
            "country_policy",
            "industry_policy"
          ],
          "status": "deposit_required"
        },
        "properties": {
          "policies": {
            "description": "List of applicable onboarding reserves policies",
            "items": {
              "type": "string"
            },
            "type": "array"
          },
          "status": {
            "description": "Onboarding reserves status (same as credit risk status but takes onboarding reserves policies into account)",
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
          }
        },
        "required": [
          "status",
          "policies"
        ],
        "title": "OnboardingReservesStatus",
        "type": "object"
      },
      "UuidSlug": {
        "description": "Identifier of the employment being terminated.",
        "example": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
        "format": "uuid",
        "title": "UuidSlug",
        "type": "string"
      },
      "OnboardingReservesStatusResponse": {
        "additionalProperties": false,
        "example": {
          "data": {
            "policies": [
              "country_policy",
              "industry_policy"
            ],
            "status": "deposit_required"
          }
        },
        "properties": {
          "data": {
            "$ref": "#/components/schemas/OnboardingReservesStatus"
          }
        },
        "required": [
          "data"
        ],
        "title": "OnboardingReservesStatusResponse",
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
    "title": "Companies",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/companies/{company_id}/employments/{employment_id}/onboarding-reserves-status": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "Returns the onboarding reserves status for a specific employment.\n\nThe status is the same as the credit risk status but takes the onboarding reserves policies into account.\n\n## Authentication\n\nThis endpoint accepts any one of the following token types:\n\n- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage employments (`employments`) | View employments (`employment:read`) | Manage employments (`employment:write`) |",
        "operationId": "get_v1_companies_company_id_employments_employment_id_onboarding-reserves-status",
        "parameters": [
          {
            "description": "Company ID",
            "example": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
            "in": "path",
            "name": "company_id",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/UuidSlug"
            }
          },
          {
            "description": "Employment ID",
            "example": "97e04d61-0a6d-4c4f-9299-c08d1eeaba20",
            "in": "path",
            "name": "employment_id",
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
                  "$ref": "#/components/schemas/OnboardingReservesStatusResponse"
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
              "employment:read",
              "employment:write",
              "employments",
              "all:write",
              "all:read"
            ],
            "OAuth2ClientCredentials": [
              "https://gateway.remote.com/company.manage",
              "employment:read",
              "employment:write",
              "employments",
              "all:write",
              "all:read"
            ]
          }
        ],
        "summary": "Get Onboarding Reserves Status for Employment",
        "tags": [
          "Compliance"
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