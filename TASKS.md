# Documentation Tasks & Discrepancies Report

**Generated:** 2025-01  
**Status:** Active development

> **Summary**: This report tracks discrepancies between documentation and implementation in the General Bots codebase. Key fixes applied: keywords now use spaces (not underscores), ON ERROR RESUME NEXT implemented, DELETE unified.

---

## ✅ COMPLETED

### Stub Files Now Have Content
- [x] `keyword-soap.md` - SOAP web service integration
- [x] `keyword-merge-pdf.md` - PDF merging (now `MERGE PDF` with space)
- [x] `keyword-kb-statistics.md` - Overall KB statistics
- [x] `keyword-kb-collection-stats.md` - Per-collection statistics
- [x] `keyword-kb-documents-count.md` - Document count
- [x] `keyword-kb-documents-added-since.md` - Recent document tracking
- [x] `keyword-kb-list-collections.md` - Collection listing
- [x] `keyword-kb-storage-size.md` - Storage monitoring

### Code Changes Applied
- [x] `SEND MAIL` - Changed from `SEND_MAIL` to space-separated
- [x] `GENERATE PDF` - Changed from `GENERATE_PDF` to space-separated
- [x] `MERGE PDF` - Changed from `MERGE_PDF` to space-separated
- [x] `ON ERROR RESUME NEXT` - Implemented in `errors/on_error.rs`
- [x] `DELETE` - Unified keyword (auto-detects HTTP/DB/File)
- [x] `PROMPT.md` - Updated with keyword naming rules

---

## ✅ COMPLETED: Model Name Updates

Model names updated to current versions (2025-01):

| File | Updated To |
|------|------------|
| `appendix-external-services/README.md` | `claude-sonnet-4.5` |
| `appendix-external-services/hosting-dns.md` | `GPT-5, o3`, `Claude Sonnet 4.5, Opus 4.5` |
| `appendix-external-services/llm-providers.md` | `DeepSeek-R3, Claude Sonnet 4.5` |
| `chapter-04-gbui/how-to/create-first-bot.md` | `claude-sonnet-4.5` |
| `chapter-04-gbui/how-to/monitor-sessions.md` | `LLM active` (generic) |
| `chapter-04-gbui/suite-manual.md` | `Claude Sonnet 4.5`, `Claude Opus 4.5`, `Gemini Pro`, `Llama 3.3` |
| `chapter-06-gbdialog/keyword-model-route.md` | `claude-sonnet-4.5`, `gemini-flash`, `claude-opus-4.5` |
| `chapter-06-gbdialog/basic-vs-automation-tools.md` | `GPT-5, o3`, `Claude Sonnet 4.5, Opus 4.5` |
| `chapter-07-gbapp/architecture.md` | `GPT-5 and o3`, `Claude Sonnet 4.5 and Opus 4.5` |
| `chapter-08-config/llm-config.md` | `claude-sonnet-4.5` |
| `chapter-08-config/secrets-management.md` | `claude-sonnet-4.5` |
| `chapter-11-features/ai-llm.md` | `GPT-5`, `o3`, `Claude Sonnet 4.5` |
| `chapter-11-features/core-features.md` | `GPT-5, o3`, `Claude Sonnet 4.5, Opus 4.5` |
| `executive-vision.md` | `GPT-5, o3`, `Claude Sonnet 4.5, Opus 4.5` |

### Naming Convention Applied
- OpenAI: `GPT-5`, `GPT-5 mini`, `o3`
- Anthropic: `Claude Sonnet 4.5`, `Claude Opus 4.5`
- Google: `Gemini Pro`, `Gemini Flash`
- Meta: `Llama 3.3`
- DeepSeek: `DeepSeek-V3`, `DeepSeek-R3`
- Local: `model.gguf`, `local-model`

---

## ✅ RESOLVED: Keyword Syntax Clarifications

### Keywords Now Use Spaces (NOT Underscores)

| ✅ Correct | ❌ Wrong |
|-----------|----------|
| `SEND MAIL` | `SEND_MAIL` |
| `GENERATE PDF` | `GENERATE_PDF` |
| `MERGE PDF` | `MERGE_PDF` |
| `SET HEADER` | `SET_HEADER` |
| `CLEAR HEADERS` | `CLEAR_HEADERS` |
| `ON ERROR RESUME NEXT` | N/A |
| `KB STATISTICS` | `KB_STATISTICS` |

### Keyword Mappings (Documentation Aliases)

| Documented Pattern | Actual Keyword |
|-------------------|----------------|
| `GENERATE FROM TEMPLATE file WITH data` | `FILL data, template` |
| `GENERATE WITH PROMPT prompt` | `LLM prompt` |
| `DELETE HTTP url` | `DELETE url` (unified) |
| `DELETE FILE path` | `DELETE path` (unified) |
| `SEND EMAIL TO addr WITH body` | `SEND MAIL addr, subject, body, []` |

### Unified DELETE Keyword

The `DELETE` keyword now auto-detects context:

```basic
' HTTP DELETE - detects URL
DELETE "https://api.example.com/resource/123"

' Database DELETE - table + filter
DELETE "customers", "status = 'inactive'"

' File DELETE - path without URL prefix
DELETE "temp/report.pdf"
```

---

## ✅ IMPLEMENTED: Error Handling

### ON ERROR RESUME NEXT (VB-Style)

Now fully implemented in `src/basic/keywords/errors/on_error.rs`:

```basic
ON ERROR RESUME NEXT    ' Enable error trapping
result = RISKY_OPERATION()
IF ERROR THEN
    TALK "Error: " + ERROR MESSAGE
END IF
ON ERROR GOTO 0         ' Disable error trapping
CLEAR ERROR             ' Clear error state
```

### Available Error Keywords

| Keyword | Description |
|---------|-------------|
| `ON ERROR RESUME NEXT` | Enable error trapping |
| `ON ERROR GOTO 0` | Disable error trapping |
| `ERROR` | Returns true if error occurred |
| `ERROR MESSAGE` | Get last error message |
| `ERR` | Get error number |
| `CLEAR ERROR` | Clear error state |
| `THROW "msg"` | Raise an error |
| `ASSERT cond, "msg"` | Assert condition |

---

## 🟡 CONFIG PARAMETERS

### Verified in Source Code ✅

```
llm-key, llm-url, llm-model
llm-cache, llm-cache-ttl, llm-cache-semantic, llm-cache-threshold
llm-server, llm-server-* (all server params)
embedding-url, embedding-model
email-from, email-server, email-port, email-user, email-pass
custom-server, custom-port, custom-database, custom-username, custom-password
image-generator-*, video-generator-*
botmodels-enabled, botmodels-host, botmodels-port
episodic-memory-threshold, episodic-memory-history
oauth-*-enabled, oauth-*-client-id, oauth-*-client-secret
website-max-depth, website-max-pages
```

### In Code But Missing from Default config.csv

| Parameter | Used In |
|-----------|---------|
| `llm-temperature` | console/status_panel.rs |
| `llm-server-reasoning-format` | llm/local.rs |
| `email-read-pixel` | email/mod.rs |
| `server-url` | email/mod.rs |
| `teams-app-id`, `teams-*` | core/bot/channels/teams.rs |
| `whatsapp-api-key`, `whatsapp-*` | core/bot/channels/whatsapp.rs |
| `twilio-*`, `aws-*`, `vonage-*` | basic/keywords/sms.rs |
| `qdrant-url` | vector database connection |

### In config.csv But Status Unknown

| Parameter | Status |
|-----------|--------|
| `website-expires` | ❓ Not found in search |
| `default-generator` | ❓ Not found in search |

---

## 📋 REMAINING TASKS

### Priority 1 - Documentation Updates
- [ ] Update all model names to generic/current versions (17 files)
- [ ] Update keyword examples to use spaces not underscores
- [ ] Fix `SEND EMAIL` examples to use `SEND MAIL` syntax
- [ ] Document unified `DELETE` keyword behavior
- [ ] Add `ON ERROR RESUME NEXT` to error handling docs

### Priority 2 - New Documentation Needed
- [ ] Full config.csv parameter reference
- [ ] SMS provider configuration (Twilio, Vonage, etc.)
- [ ] Teams/WhatsApp channel setup
- [ ] SOAP authentication configuration

### Priority 3 - Consider Implementing
- [ ] `POST url, data WITH headers` - HTTP with inline headers
- [ ] `GET url WITH params` - Query parameters support
- [ ] `WITH ... END WITH` blocks for object initialization

---

## 📊 Quick Reference

### Keyword Implementation Files

| Category | Source File |
|----------|-------------|
| Email | `send_mail.rs` → `SEND MAIL`, `SEND TEMPLATE` |
| PDF | `file_operations.rs` → `GENERATE PDF`, `MERGE PDF` |
| Data | `data_operations.rs` → `DELETE`, `INSERT`, `UPDATE`, `FILL` |
| HTTP | `http_operations.rs` → `POST`, `PUT`, `GRAPHQL`, `SOAP` |
| Errors | `errors/on_error.rs` → `ON ERROR RESUME NEXT` |
| KB Stats | `kb_statistics.rs` → `KB STATISTICS`, etc. |
| LLM | `llm_keyword.rs` → `LLM` |

### Summary Statistics

| Category | Count |
|----------|-------|
| Files with old model names | 17 |
| Stub files completed | 8 |
| Keywords fixed (underscore→space) | 6 |
| Error handling keywords added | 7 |
| Config params documented | 30+ |

---

## Architecture Notes

- **Language**: Rust with Rhai scripting engine
- **Keywords**: Registered via `register_custom_syntax()` in Rhai
- **Preprocessing**: `basic/compiler/mod.rs` normalizes some syntax
- **Config**: CSV files parsed by `ConfigManager`
- **Vector DB**: Qdrant
- **Relational DB**: PostgreSQL
- **File Storage**: MinIO/SeaweedFS