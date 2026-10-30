---
updatedAt: 2026-05-27T21:29:57.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# List Employee Leave Policies

List the leave policies for the current employee

## Authentication

This endpoint accepts any one of the following token types:

- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [OAuth Assertion](https://developer.remote.com/docs/authorization-method-oauth-assertion).
- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained by the employee through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

Any one of the scopes in a token type's row is enough. `all:read` and `all:write` work too.

| Token type | Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|---|
| Employee-scoped access token | Manage timeoffs (`time_and_attendance`) | View timeoffs (`timeoff:read`) | Manage timeoffs (`timeoff:write`) |
| Company-scoped access token | Manage timeoffs (`time_and_attendance`) | View timeoffs (`timeoff:read`) | Manage timeoffs (`timeoff:write`) |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "ListLeavePoliciesDetailsResponse": {
        "description": "Response schema for listing leave policies details",
        "example": {
          "data": [
            {
              "custom": true,
              "leave_policy_variant_id": "123e4567-e89b-12d3-a456-426614174000",
              "name": "Self-Care",
              "uses_accrual_as_balance": false
            }
          ]
        },
        "properties": {
          "data": {
            "items": {
              "$ref": "#/components/schemas/LeavePolicyDetails"
            },
            "type": "array"
          }
        },
        "required": [
          "data"
        ],
        "title": "ListLeavePoliciesDetailsResponse",
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
      "LeavePolicyDetails": {
        "additionalProperties": false,
        "description": "Leave Policy Details",
        "example": {
          "custom": true,
          "leave_policy_variant_id": "123e4567-e89b-12d3-a456-426614174000",
          "name": "Self-Care",
          "uses_accrual_as_balance": false
        },
        "properties": {
          "custom": {
            "example": true,
            "type": "boolean"
          },
          "leave_policy_variant_id": {
            "anyOf": [
              {
                "example": "123e4567-e89b-12d3-a456-426614174000",
                "format": "uuid",
                "type": "string"
              },
              {
                "description": "The type of leave a time off record or leave policy represents.\n\nResponses may return any of these values. The set is a superset of the values\naccepted when creating a time off record (see `TimeoffType`): employments on the newer leave-type model can hold leave types that are not bookable by name.\n",
                "enum": [
                  "time_off",
                  "sick_leave",
                  "public_holiday",
                  "unpaid_leave",
                  "extended_leave",
                  "in_lieu_time",
                  "maternity_leave",
                  "paternity_leave",
                  "parental_leave",
                  "bereavement",
                  "military_leave",
                  "other",
                  "paid_time_off",
                  "custom_company_leave",
                  "rtt",
                  "casual_leave",
                  "rol",
                  "ex_festivita",
                  "civic_duty",
                  "adoption",
                  "caregiver",
                  "transfer",
                  "exam",
                  "monkhood",
                  "marriage",
                  "sterilization",
                  "celebration",
                  "blood_donation",
                  "health_day",
                  "special",
                  "career",
                  "study",
                  "voluntary",
                  "adv",
                  "public_duties",
                  "force_majeure",
                  "medical_visits",
                  "marriage_child",
                  "breastfeeding",
                  "maternity_paid",
                  "maternity_unpaid",
                  "paternity_paid",
                  "paternity_unpaid",
                  "pregnancy_leave",
                  "business_trip_eu",
                  "business_trip_non_eu",
                  "training",
                  "sustainable_employability"
                ],
                "example": "sick_leave",
                "title": "ResponseTimeoffType",
                "type": "string"
              }
            ],
            "description": "The ID of the leave policy variant"
          },
          "name": {
            "example": "Self-Care",
            "type": "string"
          },
          "uses_accrual_as_balance": {
            "description": "Whether leave balance is determined by accruals",
            "example": false,
            "type": "boolean"
          }
        },
        "required": [
          "leave_policy_variant_id",
          "custom",
          "name"
        ],
        "title": "LeavePolicyDetails",
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
      }
    },
    "securitySchemes": {
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
      },
      "OAuth2Assertion": {
        "description": "Authenticate as the employee using the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant in the OAuth2 protocol,\nwith an assertion whose subject is `urn:remote-api:employee:employment:<employment_id>`.\n\nOpenAPI has no flow type for this grant, so it is declared as a client credentials flow. Request the token\nfrom the token URL with this grant type and a signed assertion, not with `client_credentials`.\n\nRemote must allow the integration to act on behalf of users, and the integration must manage the employee's company.\nRemote can also limit an integration to grants that carry a user's consent, such as the Authorization Code flow;\nthis grant is then refused.\n\nThe same grant also issues company-manager tokens: see `OAuth2CompanyManagerAssertion`.\n",
        "flows": {
          "clientCredentials": {
            "scopes": {
              "address:read": "View addresses: Read employee residential address",
              "address:write": "Manage addresses: Create and update employee residential address",
              "all:read": "Read only: List and retrieve information about all resources",
              "all:write": "Full Access: Grant access to all scopes based on your current role permissions",
              "bank_account:read": "View bank accounts: Read employee bank account details",
              "bank_account:write": "Manage bank accounts: Create and update employee bank account details",
              "document:read": "View documents: Read and list documents",
              "document:write": "Manage documents: Write and update documents",
              "emergency_contact:read": "View emergency contacts: Read employee emergency contact",
              "emergency_contact:write": "Manage emergency contacts: Create and update employee emergency contact",
              "employment_documents": "Manage employment documents: Manage employment documents",
              "employment_payments": "Manage expenses: Manage expenses and incentives",
              "employments": "Manage employments: Create and manage employments",
              "expense:read": "View expenses: List and read expenses",
              "incentive:read": "View incentives: List incentives and recurring incentives",
              "payroll": "Manage payroll runs: Manage payroll runs and calendars",
              "payslip:read": "View payslips: List and show employee's payslip",
              "personal_detail:read": "View personal details: Read employee personal information",
              "personal_detail:write": "Manage personal details: Submit or update employee personal information (DOB, national ID, tax forms, etc.)",
              "time_and_attendance": "Manage timeoffs: Manage timeoffs, leave-policies and timesheets",
              "timeoff:read": "View timeoffs: Read and list timeoffs",
              "timeoff:write": "Manage timeoffs: Create, update and cancel timeoffs",
              "timesheet:read": "View timesheets: Read timesheets"
            },
            "tokenUrl": "/auth/oauth2/token",
            "x-grantType": "urn:ietf:params:oauth:grant-type:jwt-bearer"
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
          }
        },
        "type": "oauth2"
      }
    }
  },
  "info": {
    "title": "Time & Attendance",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/employee/leave-policies": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "List the leave policies for the current employee\n\n## Authentication\n\nThis endpoint accepts any one of the following token types:\n\n- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [OAuth Assertion](https://developer.remote.com/docs/authorization-method-oauth-assertion).\n- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained by the employee through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\nAny one of the scopes in a token type's row is enough. `all:read` and `all:write` work too.\n\n| Token type | Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|---|\n| Employee-scoped access token | Manage timeoffs (`time_and_attendance`) | View timeoffs (`timeoff:read`) | Manage timeoffs (`timeoff:write`) |\n| Company-scoped access token | Manage timeoffs (`time_and_attendance`) | View timeoffs (`timeoff:read`) | Manage timeoffs (`timeoff:write`) |",
        "operationId": "get_v1_employee_leave-policies",
        "parameters": [],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ListLeavePoliciesDetailsResponse"
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
          }
        },
        "security": [
          {
            "OAuth2Assertion": [
              "timeoff:read"
            ]
          },
          {
            "OAuth2Assertion": [
              "all:read"
            ]
          },
          {
            "OAuth2Assertion": [
              "all:write"
            ]
          },
          {
            "OAuth2AuthorizationCode": [
              "https://gateway.remote.com/employment.manage"
            ]
          },
          {
            "OAuth2AuthorizationCode": [
              "timeoff:read"
            ]
          },
          {
            "OAuth2AuthorizationCode": [
              "all:read"
            ]
          },
          {
            "OAuth2AuthorizationCode": [
              "all:write"
            ]
          }
        ],
        "summary": "List Employee Leave Policies",
        "tags": [
          "Leave Policies"
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
    "timeoff.approved": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timeoff is set as approved.",
        "operationId": "timeoff.approved",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.approved",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.approved",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timeoff.canceled": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timeoff has status changed to cancelled.",
        "operationId": "timeoff.canceled",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.canceled",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.canceled",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timeoff.cancellation_requested": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an approved timeoff cancellation is requested.",
        "operationId": "timeoff.cancellation_requested",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.cancellation_requested",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.cancellation_requested",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timeoff.date_changed": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timeoff has its date changed.",
        "operationId": "timeoff.date_changed",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.date_changed",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.date_changed",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timeoff.declined": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timeoff is declined",
        "operationId": "timeoff.declined",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.declined",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.declined",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timeoff.requested": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timeoff is requested",
        "operationId": "timeoff.requested",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.requested",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.requested",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timeoff.started": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timeoff has started.",
        "operationId": "timeoff.started",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.started",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.started",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timeoff.taken": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timeoff is set as taken.",
        "operationId": "timeoff.taken",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.taken",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.taken",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timeoff.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timeoff is updated.",
        "operationId": "timeoff.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timeoff.updated",
                  "timeoff_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timeoff_id": {
                    "description": "The unique identifier of the related time off record.",
                    "type": "string"
                  }
                },
                "required": [
                  "timeoff_id",
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
        "summary": "timeoff.updated",
        "tags": [
          "Time Off"
        ]
      }
    },
    "timesheet.submitted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a timesheet is submitted by an employee",
        "operationId": "timesheet.submitted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "timesheet.submitted",
                  "timesheet_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "timesheet_id": {
                    "description": "The unique identifier of the related timesheet.",
                    "type": "string"
                  }
                },
                "required": [
                  "timesheet_id",
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
        "summary": "timesheet.submitted",
        "tags": [
          "Timesheets"
        ]
      }
    }
  }
}
```