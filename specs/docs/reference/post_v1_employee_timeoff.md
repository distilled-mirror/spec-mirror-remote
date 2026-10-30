---
updatedAt: 2026-05-27T21:29:57.000Z
agentTools:
  projectIndex: https://developer.remote.com/llms.txt
---

# Create a Pending Time Off

Creates a pending Time Off record

## Authentication

This endpoint accepts any one of the following token types:

- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [OAuth Assertion](https://developer.remote.com/docs/authorization-method-oauth-assertion).
- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained by the employee through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).

## Scopes

Any one of the scopes in a token type's row is enough. `all:write` works too.

| Token type | Category | Read only Scope | Write only Scope (read access implicit) |
|---|---|---|---|
| Employee-scoped access token | Manage timeoffs (`time_and_attendance`) | - | Manage timeoffs (`timeoff:write`) |
| Company-scoped access token | Manage timeoffs (`time_and_attendance`) | - | Manage timeoffs (`timeoff:write`) |

# OpenAPI definition

```json
{
  "components": {
    "schemas": {
      "CreateEmployeeTimeoffParams": {
        "description": "Employee timeoff creation params",
        "example": {
          "end_date": "2021-12-21",
          "leave_policy_variant_id": "paid_time_off",
          "start_date": "2021-12-20",
          "timeoff_days": [
            {
              "day": "2021-12-20",
              "hours": 8
            },
            {
              "day": "2021-12-21",
              "hours": 8
            }
          ],
          "timezone": "Asia/Kolkata"
        },
        "properties": {
          "document": {
            "$ref": "#/components/schemas/TimeoffDocumentParams"
          },
          "end_date": {
            "$ref": "#/components/schemas/Date"
          },
          "leave_policy_variant_id": {
            "nullable": false,
            "type": "string"
          },
          "notes": {
            "type": "string"
          },
          "start_date": {
            "$ref": "#/components/schemas/Date"
          },
          "timeoff_days": {
            "items": {
              "$ref": "#/components/schemas/TimeoffDaysParams"
            },
            "type": "array"
          },
          "timezone": {
            "$ref": "#/components/schemas/Timezone"
          }
        },
        "required": [
          "start_date",
          "end_date",
          "leave_policy_variant_id",
          "timezone",
          "timeoff_days"
        ],
        "title": "CreateEmployeeTimeoffParams",
        "type": "object"
      },
      "NullableDateTime": {
        "description": "Optional UTC date time in YYYY-MM-DDTHH:mm:ss format",
        "example": "2021-07-15T18:18:17",
        "format": "datetime",
        "nullable": true,
        "title": "NullableDateTime",
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
      "Timezone": {
        "description": "[TZ identifier](https://www.iana.org/time-zones)",
        "example": "Etc/UTC",
        "title": "Timezone",
        "type": "string"
      },
      "File": {
        "additionalProperties": false,
        "description": "A file associated with an employment, such as a contract, tax document, or identity document.",
        "example": {
          "id": "9880b711-file-id-ecf8f551bd78",
          "inserted_at": "2021-07-15T18:18:17Z",
          "name": "id.pdf",
          "sub_type": "personal_id",
          "type": "id"
        },
        "properties": {
          "id": {
            "description": "The unique identifier (UUID) of the file.",
            "type": "string"
          },
          "inserted_at": {
            "$ref": "#/components/schemas/DateTimeIso8601"
          },
          "name": {
            "description": "The file name including extension (e.g., \"id.pdf\", \"contract.pdf\").",
            "type": "string"
          },
          "sub_type": {
            "description": "A more specific classification of the file within its type (e.g., \"personal_id\" within type \"id\", or \"ir_35\" within type \"contract\"). Null if no sub-type applies.",
            "nullable": true,
            "type": "string"
          },
          "type": {
            "description": "The broad category of the file (e.g., \"id\", \"contract\", \"tax_document\").",
            "type": "string"
          }
        },
        "required": [
          "id",
          "inserted_at",
          "name",
          "type"
        ],
        "title": "File",
        "type": "object"
      },
      "NullableApproverId": {
        "description": "The field matches the `id` of a user in the\nRemote Platform that has permission to approve time off\nrequests. [Available users][] can be found fetching\nthe [List Company Manager][] endpoint.\n\n[Available users]: https://support.remote.com/hc/en-us/articles/360054668651-Approving-Declining-time-off-requests#h_01G0014GZKZ3EMN6P7C99HAK55\n[List Company Manager]: https://gateway.remote.com/v1/docs/openapi.html#tag/Company-Managers\n",
        "example": "51546f60-dd71-4223-9312-4efede68a497",
        "nullable": true,
        "title": "NullableApproverId",
        "type": "string"
      },
      "TimeoffDaysParams": {
        "description": "Timeoff days params",
        "example": {
          "day": "2021-12-20",
          "hours": 8
        },
        "properties": {
          "day": {
            "$ref": "#/components/schemas/Date"
          },
          "hours": {
            "type": "integer"
          }
        },
        "title": "TimeoffDaysParams",
        "type": "object"
      },
      "TimeoffDocumentParams": {
        "description": "Timeoff document params",
        "example": {
          "content": "base64 encoded content",
          "name": "document.pdf"
        },
        "properties": {
          "content": {
            "description": "The binary content of the file encoded with base64",
            "type": "string"
          },
          "name": {
            "description": "The file name of the document",
            "type": "string"
          }
        },
        "required": [
          "content",
          "name"
        ],
        "title": "TimeoffDocumentParams",
        "type": "object"
      },
      "ResponseTimeoffType": {
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
      },
      "TimeoffResponse": {
        "description": "Timeoff response",
        "example": {
          "data": {
            "timeoff": {
              "automatic": false,
              "document": {
                "id": "9880b711-file-id-ecf8f551bd78",
                "inserted_at": "2021-07-15T18:18:17Z",
                "name": "id.pdf",
                "sub_type": "personal_id",
                "type": "id"
              },
              "employment_id": "5e55386e-4f4f-4def-92f4-bdc19a5ce77d",
              "end_date": "2021-12-21",
              "id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
              "leave_policy": {
                "leave_policy_variant_slug": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
                "leave_type": "sick_leave",
                "name": "Self-Care"
              },
              "notes": "Some notes",
              "start_date": "2021-12-20",
              "status": "approved",
              "timeoff_days": [
                {
                  "day": "2021-12-20",
                  "hours": 8,
                  "minutes": 480
                },
                {
                  "day": "2021-12-21",
                  "hours": 8,
                  "minutes": 480
                }
              ],
              "timeoff_type": "paid_time_off",
              "timezone": "Asia/Kolkata",
              "total_minutes": 960
            }
          }
        },
        "properties": {
          "data": {
            "properties": {
              "timeoff": {
                "$ref": "#/components/schemas/Timeoff"
              }
            },
            "required": [
              "timeoff"
            ],
            "type": "object"
          }
        },
        "required": [
          "data"
        ],
        "title": "TimeoffResponse",
        "type": "object"
      },
      "LeavePolicy": {
        "additionalProperties": false,
        "description": "The leave policy associated with a time off request. Policies define the rules and entitlements for specific types of leave.",
        "example": {
          "leave_policy_variant_slug": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
          "leave_type": "sick_leave",
          "name": "Self-Care"
        },
        "properties": {
          "leave_policy_variant_slug": {
            "description": "The unique identifier (slug) of the specific policy variant.",
            "type": "string"
          },
          "leave_type": {
            "$ref": "#/components/schemas/ResponseTimeoffType"
          },
          "name": {
            "description": "The display name of the leave policy (e.g., \"Self-Care\", \"Annual Leave\").",
            "nullable": false,
            "type": "string"
          }
        },
        "required": [
          "name",
          "leave_type",
          "leave_policy_variant_slug"
        ],
        "title": "LeavePolicy",
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
      "TimeoffDay": {
        "description": "A single day within a time off request, specifying the date and the number of hours taken off that day.",
        "example": {
          "day": "2021-01-01",
          "hours": 8,
          "minutes": 480
        },
        "properties": {
          "day": {
            "$ref": "#/components/schemas/Date"
          },
          "hours": {
            "description": "The number of hours taken off on this day (e.g., 8 for a full day, 4 for a half day). For minute-precision durations (e.g., 7 hours 30 minutes), use `minutes`.",
            "type": "integer"
          },
          "minutes": {
            "description": "The number of minutes taken off on this day (e.g., 480 for a full 8-hour day, 450 for 7 hours 30 minutes). Minute-precision counterpart of `hours`.",
            "maximum": 1440,
            "minimum": 0,
            "type": "integer"
          }
        },
        "required": [
          "day",
          "hours",
          "minutes"
        ],
        "title": "TimeoffDay",
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
      "DateTimeIso8601": {
        "description": "UTC date time in [ISO 8601][] format.\n\n[ISO 8601]: https://en.wikipedia.org/wiki/ISO_8601\n",
        "example": "2021-07-15T18:18:17Z",
        "format": "date-time",
        "title": "DateTimeIso8601",
        "type": "string"
      },
      "Date": {
        "description": "UTC date in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format",
        "example": "2021-07-01",
        "format": "date",
        "title": "Date",
        "type": "string"
      },
      "Timeoff": {
        "additionalProperties": false,
        "description": "A time off record for an employee, representing a period of leave (e.g., vacation, sick leave, parental leave).",
        "example": {
          "automatic": false,
          "document": {
            "id": "9880b711-file-id-ecf8f551bd78",
            "inserted_at": "2021-07-15T18:18:17Z",
            "name": "id.pdf",
            "sub_type": "personal_id",
            "type": "id"
          },
          "employment_id": "5e55386e-4f4f-4def-92f4-bdc19a5ce77d",
          "end_date": "2021-12-21",
          "id": "0073fcb5-b669-4e4a-b963-2a47744e75a1",
          "leave_policy": {
            "leave_policy_variant_slug": "663e0b79-c893-45ff-a1b2-f6dcabc098b5",
            "leave_type": "sick_leave",
            "name": "Self-Care"
          },
          "notes": "Some notes",
          "start_date": "2021-12-20",
          "status": "approved",
          "timeoff_days": [
            {
              "day": "2021-12-20",
              "hours": 8,
              "minutes": 480
            },
            {
              "day": "2021-12-21",
              "hours": 8,
              "minutes": 480
            }
          ],
          "timeoff_type": "paid_time_off",
          "timezone": "Asia/Kolkata",
          "total_minutes": 960
        },
        "properties": {
          "approved_at": {
            "description": "The timestamp when the time off was approved. Null if not yet approved.",
            "format": "date-time",
            "nullable": true,
            "type": "string"
          },
          "approver_id": {
            "$ref": "#/components/schemas/NullableApproverId"
          },
          "automatic": {
            "description": "Whether this time off was automatically created by the system (e.g., public holidays) rather than requested by the employee.",
            "type": "boolean"
          },
          "cancel_reason": {
            "description": "The reason provided when the time off was cancelled. Null if not cancelled.",
            "nullable": true,
            "type": "string"
          },
          "cancelled_at": {
            "$ref": "#/components/schemas/NullableDateTime"
          },
          "document": {
            "$ref": "#/components/schemas/File"
          },
          "employment_id": {
            "description": "The unique identifier (UUID) of the employment this time off belongs to.",
            "type": "string"
          },
          "end_date": {
            "description": "The last day of the time off period (ISO 8601 date).",
            "format": "date",
            "type": "string"
          },
          "id": {
            "description": "The unique identifier (UUID) of the time off record.",
            "type": "string"
          },
          "leave_policy": {
            "$ref": "#/components/schemas/LeavePolicy"
          },
          "leave_policy_variant_id": {
            "description": "Identifier of the leave policy this time off was booked against. For employments on the leave-type model this is the leave type's UUID, the same value `GET /leave-policies/details/{employment_id}` returns and `POST /timeoff` accepts. Otherwise it is the UUID of the custom company leave policy variant, and is null for standard leave types.",
            "format": "uuid",
            "nullable": true,
            "type": "string"
          },
          "notes": {
            "description": "Optional notes provided by the employee when requesting the time off.",
            "nullable": true,
            "type": "string"
          },
          "start_date": {
            "description": "The first day of the time off period (ISO 8601 date).",
            "format": "date",
            "type": "string"
          },
          "status": {
            "description": "The current status of a time off request.\n\n- `requested`: The employee has submitted a time off request and it is awaiting approval.\n- `approved`: The time off request has been approved by a manager.\n- `cancelled`: The time off request was cancelled by the employee or an admin.\n- `declined`: The time off request was declined by a manager.\n- `taken`: The approved time off has been taken (the dates have passed).\n- `cancel_requested`: The employee has requested cancellation of a previously approved time off, pending manager approval.\n",
            "enum": [
              "requested",
              "approved",
              "cancelled",
              "declined",
              "taken",
              "cancel_requested"
            ],
            "type": "string"
          },
          "timeoff_days": {
            "description": "The individual days and hours within this time off period.",
            "items": {
              "$ref": "#/components/schemas/TimeoffDay"
            },
            "type": "array"
          },
          "timeoff_type": {
            "$ref": "#/components/schemas/ResponseTimeoffType"
          },
          "timezone": {
            "$ref": "#/components/schemas/Timezone"
          },
          "total_minutes": {
            "description": "The total number of minutes taken off across all `timeoff_days`. Always equals the sum of the per-day `minutes` values.",
            "minimum": 0,
            "type": "integer"
          }
        },
        "required": [
          "id",
          "employment_id",
          "status",
          "start_date",
          "end_date",
          "timeoff_days",
          "total_minutes",
          "timeoff_type",
          "leave_policy",
          "timezone"
        ],
        "title": "Timeoff",
        "type": "object"
      },
      "TimeoffErrorResponse": {
        "description": "A single consistent envelope for every validation error on time off write endpoints.",
        "example": {
          "errors": {
            "timeoff_days/hours": [
              "must be greater than or equal to 0",
              "must be less than or equal to 8"
            ]
          },
          "field_errors": [
            {
              "code": "parameter_value_unknown",
              "field": "timeoff_days/hours",
              "message": "must be greater than or equal to 0"
            },
            {
              "code": "parameter_value_unknown",
              "field": "timeoff_days/hours",
              "message": "must be less than or equal to 8"
            }
          ],
          "message": "Unprocessable Entity"
        },
        "properties": {
          "errors": {
            "additionalProperties": {
              "items": {
                "type": "string"
              },
              "type": "array"
            },
            "description": "Present only for a field-named failure, kept for compatibility with the shape this envelope replaced: a map of field name to that field's message(s). New consumers should read `field_errors` instead — this key may be absent.",
            "nullable": true,
            "type": "object"
          },
          "field_errors": {
            "description": "The structured, per-error list. Always present — read this, not `errors`.",
            "items": {
              "properties": {
                "code": {
                  "description": "An error code that describes the nature of the error.",
                  "type": "string"
                },
                "field": {
                  "description": "The request field this error relates to, or null for a request-level failure.",
                  "nullable": true,
                  "type": "string"
                },
                "message": {
                  "description": "A developer-friendly message describing this specific error.",
                  "type": "string"
                }
              },
              "required": [
                "field",
                "code",
                "message"
              ],
              "type": "object"
            },
            "type": "array"
          },
          "message": {
            "description": "A flat, human-readable summary of the failure.",
            "type": "string"
          }
        },
        "required": [
          "message",
          "field_errors"
        ],
        "title": "TimeoffErrorResponse",
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
    "/v1/employee/timeoff": {
      "post": {
        "callbacks": {},
        "deprecated": false,
        "description": "Creates a pending Time Off record\n\n## Authentication\n\nThis endpoint accepts any one of the following token types:\n\n- **Employee-scoped access token** (`OAuth2Assertion`) — obtained through the `urn:ietf:params:oauth:grant-type:jwt-bearer` grant. See [OAuth Assertion](https://developer.remote.com/docs/authorization-method-oauth-assertion).\n- **Company-scoped access token** (`OAuth2AuthorizationCode`) — obtained by the employee through the Authorization Code flow or the Refresh Token flow. See [Authentication for partners](https://developer.remote.com/docs/authentication-for-partners).\n\n## Scopes\n\nAny one of the scopes in a token type's row is enough. `all:write` works too.\n\n| Token type | Category | Read only Scope | Write only Scope (read access implicit) |\n|---|---|---|---|\n| Employee-scoped access token | Manage timeoffs (`time_and_attendance`) | - | Manage timeoffs (`timeoff:write`) |\n| Company-scoped access token | Manage timeoffs (`time_and_attendance`) | - | Manage timeoffs (`timeoff:write`) |",
        "operationId": "post_v1_employee_timeoff",
        "parameters": [],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/CreateEmployeeTimeoffParams"
              }
            }
          },
          "description": "Timeoff",
          "required": true
        },
        "responses": {
          "201": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/TimeoffResponse"
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
                  "$ref": "#/components/schemas/TimeoffErrorResponse"
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
            "OAuth2Assertion": [
              "timeoff:write"
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
              "timeoff:write"
            ]
          },
          {
            "OAuth2AuthorizationCode": [
              "all:write"
            ]
          }
        ],
        "summary": "Create a Pending Time Off",
        "tags": [
          "Employee Time Off"
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