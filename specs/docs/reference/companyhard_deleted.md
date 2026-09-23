---
updatedAt: 2026-09-22T04:45:18.000Z
---

Fetch the complete documentation index at: https://developer.remote.com/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# company.hard_deleted

This event is triggered when a company is permanently erased from Remote, and means the
record is physically gone: a subsequent `GET /companies/{id}` returns 404 and the identifier
must not be queried again.

Every employment belonging to the company is erased in the same operation, so you may receive
an `employment.hard_deleted` event for each of them alongside this one. Their identifiers are
also permanently gone.

This event is delivered to integration-level callbacks — a single URL registered for all of
your companies. A callback registered against the deleted company itself is erased with it and
will not receive this event.

This event may be delivered more than once, so it is safe to process repeatedly.


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
    "title": "Companies",
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
    "company.hard_deleted": {
      "post": {
        "deprecated": false,
        "description": "This event is triggered when a company is permanently erased from Remote, and means the\nrecord is physically gone: a subsequent `GET /companies/{id}` returns 404 and the identifier\nmust not be queried again.\n\nEvery employment belonging to the company is erased in the same operation, so you may receive\nan `employment.hard_deleted` event for each of them alongside this one. Their identifiers are\nalso permanently gone.\n\nThis event is delivered to integration-level callbacks — a single URL registered for all of\nyour companies. A callback registered against the deleted company itself is erased with it and\nwill not receive this event.\n\nThis event may be delivered more than once, so it is safe to process repeatedly.\n",
        "operationId": "company.hard_deleted",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "company_id": "d2091b1e-b1a4-437a-91ea-2809ffbb6d59",
                  "event_type": "company.hard_deleted",
                  "hard_deleted_at": "2026-08-24T11:02:31Z"
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
                  "hard_deleted_at": {
                    "description": "The UTC timestamp at which the company was erased.",
                    "format": "date-time",
                    "type": "string"
                  }
                },
                "required": [
                  "event_type",
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
        "summary": "company.hard_deleted",
        "tags": [
          "Company Management"
        ]
      }
    }
  }
}
```