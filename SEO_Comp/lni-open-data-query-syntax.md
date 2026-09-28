---
name: lni-open-data-query-syntax
description: The WA L&I contractor dataset's $q full-text search now returns null rows; query the ContractorLicenseNumber field or a $where clause instead
---

**Summary:** `data.wa.gov` dataset `m8qx-ubtq` no longer answers `?$q=GRIZZLC755LL` — it returns
rows whose every field is null. Two forms that do work as of 2026-09-17:

```
curl -s "https://data.wa.gov/resource/m8qx-ubtq.json?ContractorLicenseNumber=GRIZZLC755LL"
curl -s --get "https://data.wa.gov/resource/m8qx-ubtq.json" \
  --data-urlencode "\$where=upper(BusinessName) like '%GRIZZLY LANDSCAPE%'"
```

**Why it matters:** the earlier recorded method was the `$q` form, and a null result reads like
"licence not found" rather than "query syntax stopped working". That misreading would have been
recorded as a deregistration.

**How to apply:** always confirm a null L&I result with the field-filter form before concluding
anything about a contractor's status. The status field is `contractorlicensestatus`, and the row
carries no `suspend_date` key at all when the licence is ACTIVE.

---

**NAME COLLISION TRAP, added 2026-09-18.** A `like '%NAME%'` search can return a *different* company
and read as bad news. Searching `%STA-BUILT%` returns **STA-BUILT CONSTRUCTION LLC**, Rochester,
**OUT OF BUSINESS**, expired 2023-04-06 — which looks like the Lynnwood paver firm ranking in both
city packs has folded. It has not. That firm publishes **`Lic: STABUL*782LN`** on its own site,
which resolves to **STABUILT LLC, Lynnwood, ACTIVE**, effective 2022-06-15, expiring 2028-06-15 —
a different registration, found only by searching `%STABUILT%` without the hyphen.

**Always take the licence number off the competitor's own site and query that**, rather than
trusting a name match. Try hyphenated and unhyphenated spellings before concluding anything.
