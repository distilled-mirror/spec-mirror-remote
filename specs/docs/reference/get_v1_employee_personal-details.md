---
updatedAt: 2026-06-02T13:57:39.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# Show employee personal details

Returns the authenticated employee's personal details.

This endpoint requires country-specific data. Query the
[Show form schema](#tag/Countries/operation/get_show_form_country) endpoint with `personal_details`
as the form name to discover the schema for a given country.

## Authentication

This endpoint accepts any one of the following token types:

- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [OAuth Assertion](https://developer.remote.com/docs/authorization-method-oauth-assertion).
- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained by the employee through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

Any one of the scopes in a token type's row is enough. `all:read` and `all:write` work too.

| Token type | Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|---|
| Employee-scoped access token | Manage employments (`employments`) | View personal details (`personal_detail:read`) | Manage personal details (`personal_detail:write`) |
| Company-scoped access token | Manage employments (`employments`) | View personal details (`personal_detail:read`) | - |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "UserStatus": {
        "description": "The status of the user account associated with this employment.\n\n- `active`: The user account is active and the user can log in.\n- `created`: The user account has been created but the user hasn't been invited yet.\n- `invited`: The user has been invited but has not accepted the invitation yet.\n- `initiated`: The user has been invited but has not completed registration.\n- `cancelled`: The user account was cancelled before activation.\n- `inactive`: The user account has been deactivated (e.g., after offboarding).\n- `deleted`: The user account has been deleted.\n",
        "enum": [
          "active",
          "created",
          "invited",
          "initiated",
          "cancelled",
          "inactive",
          "deleted"
        ],
        "example": "active",
        "title": "UserStatus",
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
      "EmploymentStatus": {
        "description": "The current status of the employment record.\n\n- `active`: The employee is fully onboarded and actively working.\n- `created`: The employment has been created but onboarding has not started.\n- `pre_hire`: A pre-hire employment record, created before formal onboarding begins.\n- `created_awaiting_reserve`: The employment is created but waiting for a risk reserve deposit to be paid.\n- `created_reserve_paid`: The risk reserve has been paid and the employment can proceed with onboarding.\n- `initiated`: Onboarding has been started by the employer.\n- `invited`: The employee has been invited to complete their self-enrollment on Remote.\n- `pending`: The employment is pending review or further action before it can become active.\n- `review`: The employment is under review by Remote (e.g., contract or compliance review).\n- `job_title_review`: The job title is pending verification by Remote; once approved, the employment returns to `created`.\n- `pending_post_self_enrollment_actions`: Self-enrollment is complete, but some actions are still missing before the employment can be activated.\n- `archived`: The employment has been terminated or offboarded.\n- `deleted`: The employment record has been deleted.\n",
        "enum": [
          "active",
          "created",
          "created_awaiting_reserve",
          "created_reserve_paid",
          "initiated",
          "invited",
          "pending",
          "pre_hire",
          "review",
          "job_title_review",
          "pending_post_self_enrollment_actions",
          "archived",
          "deleted"
        ],
        "example": "active",
        "title": "EmploymentStatus",
        "type": "string"
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
      "EmploymentDetailsOnlyResponse": {
        "description": "Response containing only the updated details struct plus base employment fields (id, status, type, updated_at, user_status). Exactly one of the details properties is present per response.",
        "example": {
          "data": {
            "employment": {
              "contract_origin": "remote_contract",
              "id": "20a72f86-employment-id-9e4942a902ff",
              "personal_details": {},
              "status": "created",
              "type": "employee",
              "updated_at": "2024-01-15T10:30:00Z",
              "user_status": "active"
            }
          }
        },
        "properties": {
          "data": {
            "properties": {
              "employment": {
                "properties": {
                  "address_details": {
                    "description": "Home address information. Its properties may vary depending on the country. Null if the employee has not submitted their address yet.",
                    "nullable": true,
                    "type": "object"
                  },
                  "administrative_details": {
                    "description": "Administrative information. Its properties may vary depending on the country.",
                    "type": "object"
                  },
                  "bank_account_details": {
                    "items": {
                      "description": "List of bank account information. Its properties may vary depending on the country.",
                      "type": "object"
                    },
                    "type": "array"
                  },
                  "basic_information": {
                    "description": "Basic information. Its properties may vary depending on the country.\n\nWhen present, `login_email` indicates which address the employee logs in with:\n`\"personal\"` or `\"work\"`.\n",
                    "type": "object"
                  },
                  "billing_address_details": {
                    "description": "Billing address information. Its properties may vary depending on the country.",
                    "type": "object"
                  },
                  "contract_details": {
                    "description": "Contract details information. Its properties may vary depending on the country.",
                    "type": "object"
                  },
                  "contract_origin": {
                    "description": "Origin of the employment contract. Returned by the basic information endpoint.",
                    "enum": [
                      "remote_contract",
                      "custom_remote_contract",
                      "provided_by_customer"
                    ],
                    "nullable": true,
                    "type": "string"
                  },
                  "emergency_contact_details": {
                    "description": "Emergency contact information. Its properties may vary depending on the country. Null if the employee has not submitted their emergency contact yet.",
                    "nullable": true,
                    "type": "object"
                  },
                  "id": {
                    "description": "The unique identifier (UUID) of the employment.",
                    "type": "string"
                  },
                  "personal_details": {
                    "description": "Personal details information. Its properties may vary depending on the country. Null if the employee has not submitted their personal details yet.",
                    "nullable": true,
                    "type": "object"
                  },
                  "pricing_plan_details": {
                    "description": "Pricing plan information.",
                    "type": "object"
                  },
                  "status": {
                    "$ref": "#/components/schemas/EmploymentStatus"
                  },
                  "type": {
                    "description": "The type of employment.",
                    "enum": [
                      "employee",
                      "contractor",
                      "direct_employee",
                      "global_payroll_employee"
                    ],
                    "type": "string"
                  },
                  "updated_at": {
                    "description": "The timestamp when this employment record was last updated.",
                    "type": "string"
                  },
                  "user_status": {
                    "$ref": "#/components/schemas/UserStatus"
                  }
                },
                "required": [
                  "id",
                  "status",
                  "type",
                  "updated_at",
                  "user_status"
                ],
                "type": "object"
              }
            },
            "type": "object"
          }
        },
        "required": [
          "data"
        ],
        "title": "EmploymentDetailsOnlyResponse",
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
    "title": "Employments",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
  "paths": {
    "/v1/employee/personal-details": {
      "get": {
        "callbacks": {},
        "deprecated": false,
        "description": "Returns the authenticated employee's personal details.\n\nThis endpoint requires country-specific data. Query the\n[Show form schema](#tag/Countries/operation/get_show_form_country) endpoint with `personal_details`\nas the form name to discover the schema for a given country.\n\n## Authentication\n\nThis endpoint accepts any one of the following token types:\n\n- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [OAuth Assertion](https://developer.remote.com/docs/authorization-method-oauth-assertion).\n- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained by the employee through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\nAny one of the scopes in a token type's row is enough. `all:read` and `all:write` work too.\n\n| Token type | Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|---|\n| Employee-scoped access token | Manage employments (`employments`) | View personal details (`personal_detail:read`) | Manage personal details (`personal_detail:write`) |\n| Company-scoped access token | Manage employments (`employments`) | View personal details (`personal_detail:read`) | - |",
        "operationId": "get_v1_employee_personal-details",
        "parameters": [
          {
            "description": "Version of the personal_details form schema",
            "example": 1,
            "in": "query",
            "name": "personal_details_json_schema_version",
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
          }
        ],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/EmploymentDetailsOnlyResponse"
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
            "OAuth2Assertion": [
              "personal_detail:read"
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
              "personal_detail:read"
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
        "summary": "Show employee personal details",
        "tags": [
          "Employee Personal Details"
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
    "background_check.status.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a background check request status is updated.",
        "operationId": "background_check.status.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "background_check_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "company_id": "ba310525-9282-40c9-8977-14d844bf891a",
                  "employment_id": "e966a8b8-1076-11ee-a5f2-9b3997a968f6",
                  "event_type": "background_check.status.updated"
                },
                "properties": {
                  "background_check_id": {
                    "description": "The unique identifier of the background check.",
                    "type": "string"
                  },
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
                  "background_check_id",
                  "company_id",
                  "employment_id"
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
        "summary": "background_check.status.updated",
        "tags": [
          "Background Checks"
        ]
      }
    },
    "employment.account.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an employment account email is updated.",
        "operationId": "employment.account.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.account.updated"
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
        "summary": "employment.account.updated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.administrative_details.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the administrative details of an employment are updated.",
        "operationId": "employment.administrative_details.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_slug": "f2a1b3c4-d5e6-7f8g-9h0i-j1k2l3m4n5o6",
                  "event_type": "employment.administrative_details.updated"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_slug": {
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
                  "employment_slug",
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
        "summary": "employment.administrative_details.updated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.details.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an employment `department` or `manager` is updated.",
        "operationId": "employment.details.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.details.updated"
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
        "summary": "employment.details.updated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.employment_agreement.available": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment agreement is available for a user",
        "operationId": "employment.employment_agreement.available",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.employment_agreement.available",
                  "file_id": "0073fcb5-b669-4e4a-b963-2a47744e75a1"
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
                  "file_id": {
                    "description": "The unique identifier of the related file.",
                    "type": "string"
                  }
                },
                "required": [
                  "file_id",
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
        "summary": "employment.employment_agreement.available",
        "tags": [
          "Employments"
        ]
      }
    },
    "employment.eor_hiring.invoice_created": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a invoice report is created for a employment.",
        "operationId": "employment.eor_hiring.invoice_created",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "f2a1b3c4-d5e6-7f8g-9h0i-j1k2l3m4n5o6",
                  "employment_id": "f8e9d2c7-3a1b-4f5c-9e6d-8b7a2c1d0e3f",
                  "event_type": "employment.eor_hiring.invoice_created",
                  "invoice_report_id": "c7f8e9d2-3a1b-4f5c-9e6d-8b7a2c1d0e3f"
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
                  "invoice_report_id": {
                    "description": "The unique identifier of the invoice report.",
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
        "summary": "employment.eor_hiring.invoice_created",
        "tags": [
          "Employments"
        ]
      }
    },
    "employment.eor_hiring.proof_of_payment_accepted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a proof of payment is accepted.",
        "operationId": "employment.eor_hiring.proof_of_payment_accepted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "f2a1b3c4-d5e6-7f8g-9h0i-j1k2l3m4n5o6",
                  "employment_id": "f8e9d2c7-3a1b-4f5c-9e6d-8b7a2c1d0e3f",
                  "event_type": "employment.eor_hiring.proof_of_payment_accepted",
                  "proof_of_payment_id": "c7f8e9d2-3a1b-4f5c-9e6d-8b7a2c1d0e3f"
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
                  "proof_of_payment_id": {
                    "description": "The unique identifier of the proof of payment.",
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
        "summary": "employment.eor_hiring.proof_of_payment_accepted",
        "tags": [
          "Employments"
        ]
      }
    },
    "employment.eor_hiring.proof_of_payment_submitted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a proof of payment is submitted (uploaded) for an EOR hiring onboarding.",
        "operationId": "employment.eor_hiring.proof_of_payment_submitted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "f2a1b3c4-d5e6-7f8g-9h0i-j1k2l3m4n5o6",
                  "employment_id": "f8e9d2c7-3a1b-4f5c-9e6d-8b7a2c1d0e3f",
                  "event_type": "employment.eor_hiring.proof_of_payment_submitted",
                  "proof_of_payment_id": "c7f8e9d2-3a1b-4f5c-9e6d-8b7a2c1d0e3f"
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
                  "proof_of_payment_id": {
                    "description": "The unique identifier of the proof of payment.",
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
        "summary": "employment.eor_hiring.proof_of_payment_submitted",
        "tags": [
          "Employments"
        ]
      }
    },
    "employment.hard_deleted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment is permanently erased from Remote, and means the\nrecord is physically gone: a subsequent `GET /employments/{id}` returns 404 and the identifier\nmust not be queried again.\n\nAn employment that is hard deleted has often already been soft deleted, which triggered\n`employment.onboarding.cancelled`. You may therefore receive `employment.onboarding.cancelled`\nfirst and this event weeks later.\n\nThis event may be delivered more than once, so it is safe to process repeatedly.\n",
        "operationId": "employment.hard_deleted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "102172fe-4e09-480c-bd70-09cfeb34022a",
                  "event_type": "employment.hard_deleted",
                  "hard_deleted_at": "2026-08-24T11:02:31Z"
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
                  "hard_deleted_at": {
                    "description": "The UTC timestamp at which the employment was erased.",
                    "format": "date-time",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
                  "employment_id",
                  "hard_deleted_at",
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
        "summary": "employment.hard_deleted",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.job_title_review.approved": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a job title review completes with approval: the\nemployment returns to the created status and it is safe to invite the employee.\nNote this event is delivered asynchronously and its order relative to\n`employment.status.updated` is not guaranteed.\n",
        "operationId": "employment.job_title_review.approved",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.job_title_review.approved"
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
        "summary": "employment.job_title_review.approved",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.job_title_review.rejected": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a job title review completes with rejection: the\nemployment is archived and will not proceed to onboarding. The employer can\ncontest the decision through Remote support. Note this event is delivered\nasynchronously and its order relative to `employment.status.updated` is not\nguaranteed.\n",
        "operationId": "employment.job_title_review.rejected",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.job_title_review.rejected"
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
        "summary": "employment.job_title_review.rejected",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.job_title_review.started": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment enters the job title review status:\nRemote flagged the role for human review before onboarding can continue. The\nemployee cannot be invited until the review completes. Wait for\n`employment.job_title_review.approved` (safe to invite) or\n`employment.job_title_review.rejected`. If the onboarding is cancelled while\nthe review is pending, no job title review event is emitted. Note this event\nis delivered asynchronously and its order relative to\n`employment.status.updated` is not guaranteed.\n",
        "operationId": "employment.job_title_review.started",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.job_title_review.started"
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
        "summary": "employment.job_title_review.started",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.no_longer_eligible_for_onboarding_cancellation": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment is no longer eligible for onboarding cancellation.",
        "operationId": "employment.no_longer_eligible_for_onboarding_cancellation",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_slug": "ba310525-9282-40c9-8977-14d844bf891a"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "employment_slug": {
                    "description": "The unique identifier of the related employment.",
                    "type": "string"
                  }
                },
                "required": [
                  "employment_slug",
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
        "summary": "employment.no_longer_eligible_for_onboarding_cancellation",
        "tags": [
          "Employments"
        ]
      }
    },
    "employment.onboarding.cancelled": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment onboarding is cancelled.",
        "operationId": "employment.onboarding.cancelled",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "f8e9d2c7-3a1b-4f5c-9e6d-8b7a2c1d0e3f",
                  "event_type": "employment.onboarding.cancelled"
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
        "summary": "employment.onboarding.cancelled",
        "tags": [
          "Employments"
        ]
      }
    },
    "employment.onboarding.completed": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment onboarding is completed and the\nemployment is set to `active`.\n\nAn onboarding is considered complete when the employee finishes their self-enrollment\nand has completed all the onboarding tasks assigned to them (Personal profile, Administrative details,\nEmergency contact, Supporting documentation, etc).\n",
        "operationId": "employment.onboarding.completed",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.onboarding.completed"
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
        "summary": "employment.onboarding.completed",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.onboarding.started": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment onboarding is started.\n",
        "operationId": "employment.onboarding.started",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.onboarding.started"
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
        "summary": "employment.onboarding.started",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.onboarding_task.completed": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered everytime an employment onboarding task\n(Personal profile, Administrative details, Emergency contact,\nSupporting documentation, etc) is completed by an employee during\nthe self-enrollment.\n",
        "operationId": "employment.onboarding_task.completed",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "97c7ce7e-ca67-11ed-bce5-3bb70cbb9f9e",
                  "completed_task": {
                    "action": "administrative_details",
                    "completed_at": "2023-03-23T03:21:23Z",
                    "description": "description for administrative details",
                    "name": "Administrative details",
                    "required": true,
                    "status": "completed"
                  },
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.onboarding_task.completed"
                },
                "properties": {
                  "company_id": {
                    "description": "The unique identifier of the related company.",
                    "type": "string"
                  },
                  "completed_task": {
                    "properties": {
                      "action": {
                        "description": "The action identifier for this task.",
                        "enum": [
                          "additional_documents",
                          "administrative_details",
                          "business_information",
                          "emergency_contact",
                          "home_address",
                          "i9_verification",
                          "identity_verification",
                          "payment_details",
                          "review_compensation",
                          "safetywing_enrollment",
                          "user_details",
                          "employment_eligibility"
                        ],
                        "type": "string"
                      },
                      "completed_at": {
                        "description": "The timestamp when the task was completed.",
                        "format": "datetime",
                        "type": "string"
                      },
                      "description": {
                        "description": "A description of what this onboarding task covers.",
                        "type": "string"
                      },
                      "name": {
                        "description": "The name of the completed onboarding task (e.g., \"Personal details\").",
                        "type": "string"
                      },
                      "required": {
                        "description": "Whether this task was required for onboarding completion.",
                        "type": "boolean"
                      },
                      "status": {
                        "description": "The status of the task.",
                        "enum": [
                          "created",
                          "completed"
                        ],
                        "type": "string"
                      }
                    },
                    "required": [
                      "name",
                      "description",
                      "required",
                      "completed_at",
                      "action",
                      "status"
                    ]
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
                  "company_id",
                  "employment_id"
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
        "summary": "employment.onboarding_task.completed",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.personal_information.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an employment personal details is updated. Personal details includes personal informations, home address and emergency contact.",
        "operationId": "employment.personal_information.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.personal_information.updated"
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
        "summary": "employment.personal_information.updated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.start_date.changed": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the start date of an employment is changed",
        "operationId": "employment.start_date.changed",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.start_date.changed"
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
        "summary": "employment.start_date.changed",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.status.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the employment status is updated",
        "operationId": "employment.status.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.status.updated"
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
        "summary": "employment.status.updated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment is updated.\n",
        "operationId": "employment.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.updated"
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
        "summary": "employment.updated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.user_status.activated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an employment user is updated to the active status.",
        "operationId": "employment.user_status.activated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.user_status.activated"
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
        "summary": "employment.user_status.activated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.user_status.deactivated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an employment user is updated to the inactive status.",
        "operationId": "employment.user_status.deactivated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.user_status.deactivated"
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
        "summary": "employment.user_status.deactivated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.user_status.initiated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an employment user is updated to the initiated status.",
        "operationId": "employment.user_status.initiated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.user_status.initiated"
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
        "summary": "employment.user_status.initiated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.user_status.invited": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment user status is updated to invited.",
        "operationId": "employment.user_status.invited",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.user_status.invited"
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
        "summary": "employment.user_status.invited",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment.work_email.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when an employment work email is updated.\n",
        "operationId": "employment.work_email.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment.work_email.updated"
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
        "summary": "employment.work_email.updated",
        "tags": [
          "Employment Management"
        ]
      }
    },
    "employment_basic_information.updated": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when the basic information for an employment is updated",
        "operationId": "employment_basic_information.updated",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "employment_basic_information.updated"
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
        "summary": "employment_basic_information.updated",
        "tags": [
          "Employments"
        ]
      }
    },
    "identity_verification.verification_required": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered whenever an identity verification is required for an employment.",
        "operationId": "identity_verification.verification_required",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "employment_id": "2614f814-b08e-4c8e-8c4d-ddbcc4692d99",
                  "event_type": "identity_verification.verification_required"
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
        "summary": "identity_verification.verification_required",
        "tags": [
          "Identity Verification"
        ]
      }
    }
  }
}
```