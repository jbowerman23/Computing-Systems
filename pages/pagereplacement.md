# Page Replacement
---
## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7B79070ACA-526F-4174-A39E-52339BC49040%7D&file=5-page-replacement.pptx&action=edit&mobileredirect=true)
---

# Memory Management - Page Replacement
---

## Policies
- Thus far we looked at mechanisms (how) for page-oriented management
- There are several policy when) questions to consider
  - Which page frame should a new page be allocated to?
  - Which page should be removed/replaced if no free page frames are available?
  - Which page table entries should be place in TLB?

- Which page frame should a new page be allocated to?
  - All page frames are of same size
  - So any empty page frame can be used for a new page

- What if there is no empty frame?
  - Choose a page to evict from our main memory
  - Write back the page to the disk that is to be evicted
    - Only really needed if page has been modified since being loaded
    - Allocate new page to the now free frame
- Which page should be evicted?

---

## Example
- Assume main memory has only 3 page frames
- Assume a program request pages needed in the following order
  - 7, 0, 1, 2, 0, 3, 0, 4, 2, 3

## Optimal Page Replacement
- Ideally we would evict the page that won't be needed in the near future
- If the memory reference patters of a process are known
  - Then... evict the page that will not be used for the longest time in the future
  - This is called <font color="#A72608">optimal</font> page replacement policy
  - Optimal but impractical

## First in First Out (FIFO)
- Evict the page that has been in main memory the longest
- Pros: 
  - simple
  - Provides fairness
- Cons:
  - Doesn't really look at page usage

## Second Chance
- Maintain FIFO list of pages; keep reference bit for each page
- When eviction is needed
  - Check reference bit of oldest page (beginning of list)
  - If 0 (not referenced), evict page
  - If 1, set bit to 0, put page at end of list and repeat steps

## Least Recently Used
- Evict page that has not been used recently
- Works reasonable well if program has locality of reference
  - If a program uses a particular memory location (page) it is likely to use pages close to it or the same page again in the near future

