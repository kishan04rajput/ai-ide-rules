If you modified `src/utils.ts` to add a date helper and `src/components/Header.tsx` to use it:

## Add date formatting helper and update Header component

src/utils.ts
- Added `formatDate` function to handle ISO date strings

src/components/Header.tsx
- Imported `formatDate` from utils
- Updated timestamp display to use new helper
