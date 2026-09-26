# Security and Privacy Guidance

Project Rehydrate stores continuity context. That makes information hygiene important.

## Do not place secrets in context files

Never store:

- passwords;
- API keys;
- access tokens;
- private keys;
- authentication cookies;
- recovery codes;
- database connection strings containing credentials.

Use a secrets manager, environment variables, or another purpose-built secret store instead.

## Minimize sensitive operational data

A continuity file should contain only what is required to resume work safely.

Prefer:

- logical system names;
- sanitized examples;
- internal IDs only when genuinely required;
- redacted screenshots;
- generalized network information in public examples.

Avoid copying raw customer, employee, patient, financial, or otherwise sensitive datasets into continuity records.

## Public repositories

Before publishing any context, inspect it for:

- organization names;
- usernames;
- email addresses;
- hostnames;
- IP addresses;
- URLs containing private identifiers;
- credentials;
- private file paths;
- customer or employee information;
- proprietary schemas or business logic.

Sanitize first. Publish second.

## Integrity is not confidentiality

A SHA256 hash can help detect whether a file changed. It does not encrypt or protect the contents of the file.

## Human review remains required

Project Rehydrate should never be used to justify autonomous production changes. Canonical context improves continuity; it does not remove the need for engineering judgment.