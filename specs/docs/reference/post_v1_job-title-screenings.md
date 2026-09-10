---
updatedAt: 2026-09-03T14:00:27.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Create a job title screening

Screens a batch of job titles for EOR hiring eligibility, before any company or
employment exists. Callable with an integration (client credentials) token or a
company-scoped token issued through the integration; screenings belong to the
integration either way. Returns immediately with a `processing` screening — poll the
show endpoint until `status` is `completed`. Verdicts are advisory and reflect the
eligibility policy at the time of screening: the policy evolves over time and the same
checks re-run during onboarding, so the onboarding outcome may differ from an earlier
screening verdict for the same title.

## Authentication

This endpoint accepts any one of the following token types:

- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).
- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

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
      "JobTitleScreeningItem": {
        "additionalProperties": false,
        "example": {
          "job_title": "Nurse",
          "role_description": null,
          "role_is_onsite": null,
          "role_requires_license": null,
          "verdict": "eligible"
        },
        "properties": {
          "job_title": {
            "description": "The screened job title.",
            "type": "string"
          },
          "role_description": {
            "description": "The role description, if provided.",
            "nullable": true,
            "type": "string"
          },
          "role_is_onsite": {
            "description": "Whether the role is onsite, if provided.",
            "enum": [
              "yes",
              "no",
              "not_applicable"
            ],
            "nullable": true,
            "type": "string"
          },
          "role_requires_license": {
            "description": "Whether the role requires a license, if provided.",
            "enum": [
              "yes",
              "no",
              "not_applicable"
            ],
            "nullable": true,
            "type": "string"
          },
          "verdict": {
            "description": "The screening verdict. `pending` while the screening is processing; `eligible` and `not_eligible` are definitive; `needs_review` means the title will require a human review during onboarding; `eligible_with_risk_acknowledgement` means the title is eligible once the employer acknowledges the risk during onboarding. Verdicts are advisory and reflect the eligibility policy at the time of screening: the policy evolves over time and the same checks re-run during onboarding, so the onboarding outcome may differ from an earlier screening verdict for the same title.",
            "enum": [
              "pending",
              "eligible",
              "not_eligible",
              "needs_review",
              "eligible_with_risk_acknowledgement"
            ],
            "type": "string"
          }
        },
        "required": [
          "job_title",
          "verdict"
        ],
        "title": "JobTitleScreeningItem",
        "type": "object"
      },
      "JobTitleScreeningResponse": {
        "example": {
          "data": {
            "job_title_screening": {
              "created_at": "2026-01-01T00:00:00Z",
              "id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
              "items": [
                {
                  "job_title": "Nurse",
                  "role_description": null,
                  "role_is_onsite": null,
                  "role_requires_license": null,
                  "verdict": "eligible"
                }
              ],
              "status": "completed",
              "updated_at": "2026-01-01T00:01:00Z"
            }
          }
        },
        "properties": {
          "data": {
            "properties": {
              "job_title_screening": {
                "$ref": "#/components/schemas/JobTitleScreening"
              }
            },
            "type": "object"
          }
        },
        "title": "JobTitleScreeningResponse",
        "type": "object"
      },
      "CreateJobTitleScreeningParams": {
        "additionalProperties": false,
        "example": {
          "items": [
            {
              "job_title": "Nurse"
            },
            {
              "job_title": "Security Guard",
              "role_description": "Guards the office building at night",
              "role_is_onsite": "yes",
              "role_requires_license": "no"
            }
          ]
        },
        "properties": {
          "items": {
            "description": "The job titles to screen. `role_description`, `role_is_onsite` and `role_requires_license` are optional but must be provided together; when present they allow an ambiguous title to be resolved without a human review.",
            "items": {
              "additionalProperties": false,
              "properties": {
                "job_title": {
                  "description": "The job title to screen.",
                  "maxLength": 255,
                  "type": "string"
                },
                "role_description": {
                  "description": "The role description.",
                  "maxLength": 5000,
                  "type": "string"
                },
                "role_is_onsite": {
                  "description": "Whether the role is onsite.",
                  "enum": [
                    "yes",
                    "no",
                    "not_applicable"
                  ],
                  "type": "string"
                },
                "role_requires_license": {
                  "description": "Whether the role requires a license.",
                  "enum": [
                    "yes",
                    "no",
                    "not_applicable"
                  ],
                  "type": "string"
                }
              },
              "required": [
                "job_title"
              ],
              "type": "object"
            },
            "maxItems": 200,
            "minItems": 1,
            "type": "array"
          }
        },
        "required": [
          "items"
        ],
        "title": "CreateJobTitleScreeningParams",
        "type": "object"
      },
      "JobTitleScreening": {
        "additionalProperties": false,
        "example": {
          "created_at": "2026-01-01T00:00:00Z",
          "id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
          "items": [
            {
              "job_title": "Nurse",
              "role_description": null,
              "role_is_onsite": null,
              "role_requires_license": null,
              "verdict": "eligible"
            }
          ],
          "status": "completed",
          "updated_at": "2026-01-01T00:01:00Z"
        },
        "properties": {
          "created_at": {
            "description": "The timestamp when the screening request was created.",
            "type": "string"
          },
          "id": {
            "description": "The unique identifier (UUID) of the screening request.",
            "type": "string"
          },
          "items": {
            "items": {
              "$ref": "#/components/schemas/JobTitleScreeningItem"
            },
            "type": "array"
          },
          "status": {
            "description": "The processing status of the screening request. Poll until `completed` or `failed`. A `failed` screening gave up after retries; unscreened items stay `pending` and the batch should be resubmitted as a new screening.",
            "enum": [
              "processing",
              "completed",
              "failed"
            ],
            "type": "string"
          },
          "updated_at": {
            "description": "The timestamp of the last update to the screening request.",
            "type": "string"
          }
        },
        "required": [
          "id",
          "status",
          "items",
          "created_at",
          "updated_at"
        ],
        "title": "JobTitleScreening",
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
    "title": "Integrations",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/job-title-screenings": {
      "post": {
        "callbacks": {},
        "deprecated": false,
        "description": "Screens a batch of job titles for EOR hiring eligibility, before any company or\nemployment exists. Callable with an integration (client credentials) token or a\ncompany-scoped token issued through the integration; screenings belong to the\nintegration either way. Returns immediately with a `processing` screening — poll the\nshow endpoint until `status` is `completed`. Verdicts are advisory and reflect the\neligibility policy at the time of screening: the policy evolves over time and the same\nchecks re-run during onboarding, so the onboarding outcome may differ from an earlier\nscreening verdict for the same title.\n\n## Authentication\n\nThis endpoint accepts any one of the following token types:\n\n- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n- **Client credentials access token** (`OAuth2ClientCredentials`) — obtained through the Client Credentials flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).",
        "operationId": "post_v1_job-title-screenings",
        "parameters": [],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/CreateJobTitleScreeningParams"
              }
            }
          },
          "description": "Job title screening params",
          "required": false
        },
        "responses": {
          "202": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/JobTitleScreeningResponse"
                }
              }
            },
            "description": "Accepted"
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
            "OAuth2AuthorizationCode": [],
            "OAuth2ClientCredentials": []
          }
        ],
        "summary": "Create a job title screening",
        "tags": [
          "Job Title Screenings"
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