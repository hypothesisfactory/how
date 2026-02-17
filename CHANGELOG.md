# Changelog

All notable changes to this project will be documented in this file.

## [1.0.2] - 2026-02-16

### Changed

#### API Migration: google.generativeai → google.genai
- **Deprecated Package Removed:** Migrated from `google-generativeai` (end-of-life) to `google-genai` (active support)
  - The `google.generativeai` package is no longer receiving updates or bug fixes
  - Switched to `google.genai` for ongoing maintenance and new features

#### Python Version Requirements
- **Minimum Python:** Updated from `>=3.8` to `>=3.14`
  - Aligns with current `google-genai` package requirements
  - Ensures compatibility with latest dependency versions

#### Code Updates

**Package Dependencies:**
- Replaced `google-generativeai` with `google-genai` in `pyproject.toml`
- Updated `requires-python` constraint to `>=3.14`

**API Implementation Changes:**

1. **Client Initialization**
   - Old: `genai.configure(api_key=api_key)`
   - New: `client = genai.Client(api_key=api_key)`

2. **Model API Calls**
   - Old: 
     ```python
     model = genai.GenerativeModel(MODEL_NAME)
     response = model.generate_content(prompt, request_options={"timeout": TIMEOUT})
     ```
   - New:
     ```python
     client = genai.Client(api_key=api_key)
     response = client.models.generate_content(model=MODEL_NAME, contents=prompt)
     ```

3. **Exception Handling**
   - Old: Caught specific exception types (`genai.types.BlockedPromptException`, `genai.types.StopCandidateException`)
   - New: Generic exception handling with string-based filtering for "blocked" and "stopped" messages
   - Rationale: New API uses different exception hierarchy

### Deprecated

- `google.generativeai` package (no longer maintained)

### Notes

- All functionality preserved with new API
- No breaking changes to user-facing CLI interface
- Improved long-term maintainability with active dependency support
