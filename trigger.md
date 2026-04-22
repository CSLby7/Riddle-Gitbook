---
icon: bolt-lightning
---

# Trigger

## Top-K Pattern

When you see

* need "top k" / "best k" / "most frequent k"
* OR answer depends only on a subset of size k
* AND elements are changing (sliding window / updates / frequency changes)

Think: Maintain a boundary between selected (top k) and unselected

Decide:

* Static or only insertion → heap (LC 347)
* Dynamic updates:
  * Only need top element OR lazy deletion is acceptable → **Heap** (lazy deletion)
  * Need exact top k set OR frequent arbitrary removal → **Two balanced sets/treeSets** (LC 3321)
  * Need median / split into two halves → Two heaps

