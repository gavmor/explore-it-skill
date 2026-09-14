# Test Heuristics Cheat Sheet Reference

Detailed reference guide for cognitive heuristics during exploratory test execution, adapted from *Explore It!* by Elisabeth Hendrickson.

## 1. Input & Data Heuristics

### Goldilocks (Too Small, Too Big, Just Right)
- **Numerical values:** Negative numbers, zero, maximum integer ($2^{31}-1$, $2^{63}-1$), fractional values (`0.0000001`).
- **Strings:** Empty string (`""`), 1 character, 255 characters, 65,536 characters, 1MB string.
- **Files:** 0-byte file, 1-byte file, exact max-size limit, 1 byte over max-size limit, corrupted headers.

### Zero, One, Many
- **Collections:** Empty array (`[]`), single element (`[x]`), thousands of elements (`[x1...xn]`).
- **Pagination:** Page 0, Page 1, Page with 0 items, Page past maximum total pages.
- **Counts:** 0 items found, 1 item found, 999+ items found.

### Some, None, All
- **Selections:** No checkboxes selected, all checkboxes selected, odd subset selected.
- **Permissions:** Account with zero permissions (verify it doesn't default to superuser!), account with all permissions.

### Violate Data Format Rules
- **Encodings:** Valid UTF-8, multi-byte emojis (👨‍👩‍👧‍👦), zero-width spaces (`\u200B`), non-ASCII characters.
- **Syntactic Violations:** Missing `@` in emails, letters in phone numbers, invalid IP octets (`256.0.0.1`), unescaped quotes (`'`, `"`).
- **Injection Strings:** SQL (`' OR '1'='1`), XSS (`<script>alert(1)</script>`), Template injection (`{{7*7}}`).

---

## 2. Sequence & Flow Heuristics

### Beginning, Middle, End
- Insert, edit, or delete items at index 0, mid-index, and last-index.
- Look for off-by-one errors and array truncation.

### Reverse
- Step backward through wizards using browser or UI back buttons.
- Execute undo/redo chains repeatedly.
- Accept default values to the final step, then navigate backward to change the very first field.

### Interrupt
- Kill processes mid-write (`kill -9`).
- Disconnect network while uploading or downloading.
- Put laptop to sleep or trigger session timeout during checkout.

---

## 3. Structural & Architectural Heuristics

### Follow the Data
Trace data across system boundaries:
1. Input via web form or API.
2. Read directly from database table.
3. Verify background worker queue ingestion.
4. Check search index reflection (Elasticsearch/Solr).
5. Inspect generated CSV/PDF export reports.

### Starve
- Saturated CPU (100% load).
- Low memory (simulate OOM conditions).
- Read-only or 100% full filesystem.
- Blocked socket connections or restricted file descriptors.
