---
updatedAt: 2026-09-30T13:12:00.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# List eligible project leads

Lists the users eligible to be assigned as a lead for a company's projects.

## Authentication

This endpoint requires the following token type:

- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

| Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|
| Manage projects (`projects`) | View projects (`project:read`) | Manage projects (`project:write`) |

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
      "EligibleLead": {
        "additionalProperties": false,
        "description": "A user eligible to be assigned as a project lead",
        "example": {
          "id": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
          "name": "Jane Doe"
        },
        "properties": {
          "id": {
            "description": "User identifier.",
            "example": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
            "format": "uuid",
            "title": "EligibleLeadID",
            "type": "string"
          },
          "name": {
            "description": "Name of the user.",
            "type": "string"
          }
        },
        "required": [
          "id",
          "name"
        ],
        "title": "EligibleLead",
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
      "ListEligibleLeadsResponse": {
        "additionalProperties": false,
        "description": "List of users eligible to be assigned as project leads.",
        "example": {
          "data": [
            {
              "id": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
              "name": "Jane Doe"
            }
          ]
        },
        "properties": {
          "data": {
            "items": {
              "$ref": "#/components/schemas/EligibleLead"
            },
            "type": "array"
          }
        },
        "required": [
          "data"
        ],
        "title": "ListEligibleLeadsResponse",
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
              "projects": "projects",
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
              "projects": "projects",
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
      }
    }
  },
  "info": {
    "title": "Contractors",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/project-eligible-leads": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "Lists the users eligible to be assigned as a lead for a company's projects.\n\n## Authentication\n\nThis endpoint requires the following token type:\n\n- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\n| Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|\n| Manage projects (`projects`) | View projects (`project:read`) | Manage projects (`project:write`) |",
        "operationId": "get_v1_project-eligible-leads",
        "parameters": [],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ListEligibleLeadsResponse"
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
              "project:read",
              "project:write",
              "projects",
              "all:write",
              "all:read"
            ]
          }
        ],
        "summary": "List eligible project leads",
        "tags": [
          "Projects"
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
      "name": "Employments"
    }
  ],
  "webhooks": {
    "contractor_invoice.employer_paid": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when Remote has confirmed receipt of the employer's\nfunds for a contractor invoice (the associated outstanding payment moves to\n`paid_in`). Payout to the contractor has not happened yet.\n\nThe payload is stateless. Use the contractor invoice ID and employment ID to retrieve current details.\n",
        "operationId": "contractor_invoice.employer_paid",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "123-example",
                  "contractor_invoice_id": "123-example",
                  "employment_id": "123-example",
                  "event_type": "contractor_invoice.employer_paid"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "contractor_invoice_id": {
                    "description": "The unique identifier of the contractor invoice.",
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
                  "event_type",
                  "contractor_invoice_id",
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
        "summary": "contractor_invoice.employer_paid",
        "tags": [
          "Invoices"
        ]
      }
    },
    "contractor_invoice.funds_returned": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the payout of a contractor invoice is returned — the funds were sent but the\ncontractor's bank rejected them, for example because of incorrect bank details. It is sent once per invoice:\nif a retry fails or is returned again, the event is not sent again.\n\nThe payload is stateless. Use the contractor invoice ID and employment ID to retrieve current details.\n",
        "operationId": "contractor_invoice.funds_returned",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "123-example",
                  "contractor_invoice_id": "123-example",
                  "employment_id": "123-example",
                  "event_type": "contractor_invoice.funds_returned"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "contractor_invoice_id": {
                    "description": "The unique identifier of the contractor invoice.",
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
                  "event_type",
                  "contractor_invoice_id",
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
        "summary": "contractor_invoice.funds_returned",
        "tags": [
          "Invoices"
        ]
      }
    },
    "contractor_invoice.issued": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a contractor invoice is issued for the first time —\neither submitted by the contractor on creation, or transitioned out of `draft`.\n\nThe payload is stateless. Use the contractor invoice ID and employment ID to retrieve current details.\n",
        "operationId": "contractor_invoice.issued",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "123-example",
                  "contractor_invoice_id": "123-example",
                  "employment_id": "123-example",
                  "event_type": "contractor_invoice.issued"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "contractor_invoice_id": {
                    "description": "The unique identifier of the contractor invoice.",
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
                  "event_type",
                  "contractor_invoice_id",
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
        "summary": "contractor_invoice.issued",
        "tags": [
          "Invoices"
        ]
      }
    },
    "contractor_invoice.paid_out": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a contractor invoice has been paid out — funds\nhave been delivered to the contractor. This is the terminal lifecycle event.\n\nThe payload is stateless. Use the contractor invoice ID and employment ID to retrieve current details.\n",
        "operationId": "contractor_invoice.paid_out",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "123-example",
                  "contractor_invoice_id": "123-example",
                  "employment_id": "123-example",
                  "event_type": "contractor_invoice.paid_out"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "contractor_invoice_id": {
                    "description": "The unique identifier of the contractor invoice.",
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
                  "event_type",
                  "contractor_invoice_id",
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
        "summary": "contractor_invoice.paid_out",
        "tags": [
          "Invoices"
        ]
      }
    },
    "contractor_invoice.pay_out_failed": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the payout of a contractor invoice fails — the funds could not be sent to the\ncontractor, for example because of an issue with the contractor's bank details. It is sent once per invoice:\nif a retry fails again, the event is not sent again.\n\nThe payload is stateless. Use the contractor invoice ID and employment ID to retrieve current details.\n",
        "operationId": "contractor_invoice.pay_out_failed",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "123-example",
                  "contractor_invoice_id": "123-example",
                  "employment_id": "123-example",
                  "event_type": "contractor_invoice.pay_out_failed"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "contractor_invoice_id": {
                    "description": "The unique identifier of the contractor invoice.",
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
                  "event_type",
                  "contractor_invoice_id",
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
        "summary": "contractor_invoice.pay_out_failed",
        "tags": [
          "Invoices"
        ]
      }
    },
    "contractor_invoice.payment_initiated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employer initiates payment on a contractor invoice\nfor the first time (transition to `pending_payment` from `issued` or `approved`).\n\nThe payload is stateless. Use the contractor invoice ID and employment ID to retrieve current details.\n",
        "operationId": "contractor_invoice.payment_initiated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "123-example",
                  "contractor_invoice_id": "123-example",
                  "employment_id": "123-example",
                  "event_type": "contractor_invoice.payment_initiated"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "contractor_invoice_id": {
                    "description": "The unique identifier of the contractor invoice.",
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
                  "event_type",
                  "contractor_invoice_id",
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
        "summary": "contractor_invoice.payment_initiated",
        "tags": [
          "Invoices"
        ]
      }
    },
    "employment.contractor_management_plan.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a contractor's plan changes between Contractor Management (CM)\nand Contractor Management Plus (CM+).\n\nThe payload is stateless. Use the employment endpoint to retrieve the current plan details.\n",
        "operationId": "employment.contractor_management_plan.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "129d02bc-dd6a-11ed-ac99-cb057df06a33",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.contractor_management_plan.updated"
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
                  }
                },
                "required": [
                  "event_type",
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
        "summary": "employment.contractor_management_plan.updated",
        "tags": [
          "Employments"
        ]
      }
    },
    "employment.contractor_of_record_termination.cancelled": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a contractor of record termination request is cancelled.\n\nThe payload is stateless. Use the termination request ID and employment ID to retrieve the current details.\n",
        "operationId": "employment.contractor_of_record_termination.cancelled",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "123-example",
                  "employment_id": "123-example",
                  "event_type": "employment.contractor_of_record_termination.cancelled",
                  "termination_request_id": "123-example"
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
                  "termination_request_id": {
                    "description": "The unique identifier of the termination request.",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "termination_request_id",
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
        "summary": "employment.contractor_of_record_termination.cancelled",
        "tags": [
          "Employments"
        ]
      }
    },
    "employment.cor_hiring.invoice_created": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a invoice report is created for a employment.",
        "operationId": "employment.cor_hiring.invoice_created",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "f2a1b3c4-d5e6-7f8g-9h0i-j1k2l3m4n5o6",
                  "employment_id": "f8e9d2c7-3a1b-4f5c-9e6d-8b7a2c1d0e3f",
                  "event_type": "employment.cor_hiring.invoice_created",
                  "invoice_report_id": "c7f8e9d2-3a1b-4f5c-9e6d-8b7a2c1d0e3f"
                },
                "properties": {
                  "company_id": {
                    "type": "string"
                  },
                  "employment_id": {
                    "type": "string"
                  },
                  "event_type": {
                    "type": "string"
                  },
                  "invoice_report_id": {
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "invoice_report_id",
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
        "summary": "employment.cor_hiring.invoice_created",
        "tags": [
          "COR Hiring"
        ]
      }
    },
    "employment.cor_hiring.proof_of_payment_accepted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a proof of payment is accepted for a contractor of record employment.",
        "operationId": "employment.cor_hiring.proof_of_payment_accepted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "f2a1b3c4-d5e6-7f8g-9h0i-j1k2l3m4n5o6",
                  "employment_id": "f8e9d2c7-3a1b-4f5c-9e6d-8b7a2c1d0e3f",
                  "event_type": "employment.cor_hiring.proof_of_payment_accepted",
                  "proof_of_payment_id": "c7f8e9d2-3a1b-4f5c-9e6d-8b7a2c1d0e3f"
                },
                "properties": {
                  "company_id": {
                    "type": "string"
                  },
                  "employment_id": {
                    "type": "string"
                  },
                  "event_type": {
                    "type": "string"
                  },
                  "proof_of_payment_id": {
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "proof_of_payment_id",
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
        "summary": "employment.cor_hiring.proof_of_payment_accepted",
        "tags": [
          "COR Hiring"
        ]
      }
    },
    "employment.cor_hiring.proof_of_payment_submitted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a proof of payment is submitted for a contractor of record employment.",
        "operationId": "employment.cor_hiring.proof_of_payment_submitted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "f2a1b3c4-d5e6-7f8g-9h0i-j1k2l3m4n5o6",
                  "employment_id": "f8e9d2c7-3a1b-4f5c-9e6d-8b7a2c1d0e3f",
                  "event_type": "employment.cor_hiring.proof_of_payment_submitted",
                  "proof_of_payment_id": "c7f8e9d2-3a1b-4f5c-9e6d-8b7a2c1d0e3f"
                },
                "properties": {
                  "company_id": {
                    "type": "string"
                  },
                  "employment_id": {
                    "type": "string"
                  },
                  "event_type": {
                    "type": "string"
                  },
                  "proof_of_payment_id": {
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "proof_of_payment_id",
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
        "summary": "employment.cor_hiring.proof_of_payment_submitted",
        "tags": [
          "COR Hiring"
        ]
      }
    }
  }
}
```