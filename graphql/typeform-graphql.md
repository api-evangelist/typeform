# Typeform GraphQL Schema

## Overview

This is a conceptual GraphQL schema for the Typeform developer platform. Typeform exposes four primary REST API surfaces — Create API, Responses API, Webhooks API, and an Embed SDK — plus deep workspace and account endpoints. This schema models the full domain as a unified GraphQL graph.

- Provider: Typeform
- API surface: Create API, Responses API, Webhooks API, Embed SDK
- REST reference: https://www.typeform.com/developers/create/reference/
- GitHub: https://github.com/Typeform
- Schema file: typeform-schema.graphql

## Domain Model

### Forms

The `Form` type is the central resource. Each form contains ordered `FormField` nodes, optional `WelcomeScreen` and `ThankYouScreen` nodes, a `Theme`, branching `Logic`, `Variable` declarations, and `HiddenField` definitions.

### Fields

`FormField` supports 17 field types via the `FieldType` enum (SHORT_TEXT, LONG_TEXT, MULTIPLE_CHOICE, PICTURE_CHOICE, DROPDOWN, YES_NO, EMAIL, DATE, NUMBER, RATING, OPINION_SCALE, RANKING, MATRIX, FILE_UPLOAD, PAYMENT, WEBSITE, PHONE_NUMBER, STATEMENT, GROUP, LEGAL). Each field carries a `FieldProperties` bag that is interpreted based on type, plus server-side `FieldValidations`.

### Choices and Lists

Choice-based fields reference `Choice` nodes inline or via a reusable `ChoiceList`. Choices may carry an `Attachment` (image). The `OtherSettings` type captures the free-text "other" option label.

### Logic

Branching logic is expressed through `Logic` -> `Action` -> `ConditionGroup` -> `Condition` -> `ConditionVar` chains. `LogicJump` represents a direct skip-to navigation. The `LogicActionType` enum covers JUMP, ADD, SUBTRACT, MULTIPLY, and DIVIDE (for score calculations).

### Variables and Hidden Fields

`Variable` holds form-level numeric or text accumulators used in scoring or piping. `HiddenField` carries external metadata (e.g., CRM IDs) into a response without being displayed.

### Themes and Branding

`Theme` defines color palette (`ThemeColors`), font (`Font`), and optional background `Image`. `BrandKit` aggregates logos, colors, and fonts into a reusable brand identity. `FontFamily` catalogs all available web fonts.

### Workspaces

`Workspace` is the organizational container owning forms and `Collaborator` members. `SharedWorkspace` represents a workspace shared with the calling user. `Team` groups collaborators.

### Responses

`Response` holds a submission: timestamps, metadata, `Answer` list, hidden-field values, and a `Calculation` result. Each `Answer` references its field via `AnswerFieldRef` and carries a polymorphic `AnswerValue` (text, number, boolean, choice, file, payment). `Completion` aggregates conversion statistics. `Responder` links a respondent identity to multiple responses.

### Webhooks

`Webhook` describes a subscription (URL, secret, SSL verification flag). `WebhookEvent` is the push payload delivered to that URL on each submission.

### Publishing and Embeds

`SurveyPublishing` tracks a form's live/draft/closed state plus shareable URLs. `Collector` models distinct distribution channels. `TypeformEmbed` and `ModalLayout` capture Embed SDK configuration.

### Account and Security

`AppSettings` holds per-form notification rules, tracking pixel IDs, redirect URL, and branding flags. `APIToken` models personal access tokens with scoped `Permission` grants. `Tag` provides organizational labeling.

## Named Types (55+)

| Type | Category |
|---|---|
| Form | Core |
| FormField | Core |
| FieldType | Enum |
| FieldProperties | Core |
| FieldValidations | Core |
| ChoiceList | Core |
| Choice | Core |
| DateSettings | Field settings |
| RatingSettings | Field settings |
| ScaleSettings | Field settings |
| ScaleLabels | Field settings |
| OtherSettings | Field settings |
| Attachment | Media |
| AttachmentProperties | Media |
| FocalPoint | Media |
| Layout | Visual |
| WelcomeScreen | Screen |
| ThankYouScreen | Screen |
| ScreenProperties | Screen |
| Button | Screen |
| Logic | Logic |
| LogicJump | Logic |
| Action | Logic |
| ActionDetails | Logic |
| ConditionGroup | Logic |
| Condition | Logic |
| ConditionVar | Logic |
| ConditionGroupOperator | Enum |
| ConditionOperator | Enum |
| LogicActionType | Enum |
| Variable | Logic |
| VariableRef | Logic |
| HiddenField | Logic |
| Calculation | Logic |
| Reference | Logic |
| Theme | Branding |
| ThemeColors | Branding |
| ThemeColor | Branding |
| ThemeColorKey | Enum |
| Image | Branding |
| BrandKit | Branding |
| Font | Branding |
| FontFamily | Branding |
| FontFamilyCategory | Enum |
| Workspace | Org |
| WorkspaceFormsSummary | Org |
| WorkspaceSelf | Org |
| WorkspaceRole | Enum |
| SharedWorkspace | Org |
| Collaborator | Org |
| Team | Org |
| Response | Responses |
| FormDefinitionSnapshot | Responses |
| ResponseMetadata | Responses |
| Answer | Responses |
| AnswerFieldRef | Responses |
| AnswerValue | Responses |
| AnswerChoices | Responses |
| PaymentAnswer | Responses |
| Completion | Responses |
| Responder | Responses |
| Webhook | Webhooks |
| WebhookEvent | Webhooks |
| WebhookStatus | Enum |
| SurveyPublishing | Publishing |
| Collector | Publishing |
| TypeformEmbed | Publishing |
| ModalLayout | Publishing |
| EmbedMode | Enum |
| PublishingStatus | Enum |
| AppSettings | Account |
| FormMeta | Account |
| Notification | Account |
| APIToken | Account |
| Permission | Account |
| PermissionScope | Enum |
| Tag | Account |
| FormLinks | Core |
| FormPage | Pagination |
| WorkspacePage | Pagination |
| ResponsePage | Pagination |
| ThemePage | Pagination |

## Queries

- `form(id)` — single form
- `forms(page, pageSize, search, workspaceId)` — paginated form list
- `workspace(id)` — single workspace
- `workspaces(page, pageSize)` — paginated workspace list
- `responses(formId, ...)` — paginated responses with filtering
- `webhooks(formId)` — all webhooks for a form
- `webhook(formId, tag)` — single webhook
- `theme(id)` — single theme
- `themes(page, pageSize)` — paginated theme list
- `image(id)` — single image
- `completion(formId)` — completion statistics
- `apiTokens` — account API tokens

## Mutations

- `createForm / updateForm / deleteForm`
- `createWebhook / updateWebhook / deleteWebhook`
- `createTheme / updateTheme / deleteTheme`
- `uploadImage`
- `createWorkspace / updateWorkspace / deleteWorkspace`
