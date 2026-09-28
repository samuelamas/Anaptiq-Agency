---
name: verify-similarity-numbers-twice
description: Two shell idioms I used silently doubled a content-similarity figure and inflated word counts by 10%; measure twice before reporting either
---

**Summary:** on 2026-09-17 I reported Grizzly's city pages as "97% identical, 26 differing tokens of
926". A fresh-context verification agent re-measured and got **13 differing tokens of 833, 98.4%
identical**. Two idioms were at fault:

```bash
# DOUBLES the real difference — each substitution emits both a '<' and a '>' line
diff <(tr ' ' '\n' < a.txt) <(tr ' ' '\n' < b.txt) | grep -c '^[<>]'

# INFLATES word count ~10% — counts <script> and <style> content as words
sed 's/<[^>]*>/ /g' page.html | tr -s ' \n' ' ' | wc -w
```

**Why it matters:** both errors ran in the same direction — they made the site look better than it
is. An error that flatters the subject is the one least likely to be questioned. The corrected
figure also changed a conclusion: at the real numbers, the Edmonds page that was hand-built from the
localisation spec is still **96% identical** to a page about a different city, which the inflated
figure had disguised.

**How to apply:** for any similarity or word-count figure that will appear in a client deliverable,
run a second independent measurement — `difflib.SequenceMatcher` on the token lists, and a word
count taken after stripping script/style — before writing the number down. See
[[grizzly-city-pages-are-near-duplicates]].
