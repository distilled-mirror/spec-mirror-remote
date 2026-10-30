---
updatedAt: 2026-04-20T19:12:53.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# employment.administrative_details.updated

This event is triggered when the administrative details of an employment are updated.

# OpenAPI definition

```json
{
  "components": {
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
      }
    }
  },
  "info": {
    "title": "Employments",
    "version": "2.0.0"
  },
  "openapi": "3.1.0",
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
    }
  }
}
```