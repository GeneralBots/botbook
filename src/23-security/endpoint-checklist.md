# Endpoint Security Checklist

When adding new endpoints to the `.gbai` and BotServer APIs, ensure you adhere to this standard security checklist. All state-changing endpoints (those using `POST`, `PUT`, `PATCH`, or `DELETE` methods) must be protected against common Web vulnerabilities, including CSRF.

## 1. CSRF Protection for State-Changing Endpoints

Cross-Site Request Forgery (CSRF) protection must be applied to any endpoint that alters system state. Evaluate if the endpoint falls under one of the following exemptions:

*   **Exemptions:**
    *   API endpoints exclusively utilizing **Bearer Token** authentication (stateless requests that do not rely on cookies).
    *   Webhooks from external systems that provide their own authentication mechanisms (e.g., HMAC signatures like WhatsApp/Meta).
    *   Publicly fully accessible endpoints that do not affect any user data or system state.
*   **Requirements:**
    *   All web-facing or cookie-authenticated endpoints must enforce CSRF checks.
    *   Tokens must be bound to the user session.
    *   Utilize double-submit cookie pattern or header-based token verification via the `CsrfManager`.

## 2. Authentication & Authorization (RBAC) Requirements

Do not expose new endpoints without explicitly defining their necessary permissions.

*   Ensure the endpoint is behind the `require_authentication_middleware` or similar authentication flow unless it is strictly intended to be public (e.g., `/api/auth/login`).
*   Assign appropriate RBAC (Role-Based Access Control) permissions and ensure `require_role_middleware` is validated.
*   Validate resource ownership. If a user tries to edit or delete an entity (e.g., a Bot, Document, or File), the backend must confirm they own the entity or possess tenant/admin privileges.

## 3. Strict Security Headers

All HTTP responses returning HTML content must include standard security headers.

*   Ensure the router uses `security_headers_middleware`.
*   Mandatory Headers:
    *   `Content-Security-Policy`: Must clearly restrict `script-src`, `connect-src`, and `frame-ancestors`.
    *   `X-Frame-Options: DENY` (or `SAMEORIGIN` if absolutely necessary for the suite).
    *   `X-Content-Type-Options: nosniff`.
    *   `Strict-Transport-Security` (HSTS).
    *   `Referrer-Policy: strict-origin-when-cross-origin`.

## 4. Input Validation & Sanitization

Do not rely exclusively on client-side validation.

*   Validate the schema, length, and format of all incoming request payloads (`JSON`, `Query`, `Form`).
*   Sanitize inputs that might be used inside SQL queries, though using ORMs (like Diesel) or parameterized queries safely mitigates straightforward SQL injection. Avoid dynamic SQL string formatting.
*   Sanitize any output bound for HTML parsing to prevent Stored or Reflected XSS.

## 5. Rate Limiting

Endpoints must prevent brute force and DDoS abuse.

*   Apply or ensure that globally the `rate_limit_middleware` covers the new route.
*   Authentication endpoints (like login forms) should have significantly stricter rate limits.
*   Consider adding secondary quotas per underlying resource if dealing with expensive generation tasks (like LLM interactions).

## 6. Secure Error Handling

Never leak internal traces or paths.

*   Do not `unwrap()`, `expect()`, or `panic!()`. Use Rust's `?` operator.
*   Use `ErrorSanitizer` logic, or return generalized application errors like `(StatusCode::INTERNAL_SERVER_ERROR, "An internal error occurred")` instead of specific database schema details.

---

### Process for Review

When submitting a PR incorporating new endpoints, mention that you have completed this checklist in your PR description.
