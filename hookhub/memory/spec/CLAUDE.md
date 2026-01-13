# HookHub MVP Specification

## Overview
HookHub is a web application for discovering and browsing open-source cloud hooks (webhooks). The MVP focuses on displaying a curated collection of hooks in an intuitive grid layout.

## Tech Stack
- **Framework:** Next.js 16.1.1
- **UI:** React 19.2.3
- **Styling:** Tailwind CSS v4
- **Language:** TypeScript

## Data Model

### Hook Entity
```typescript
interface Hook {
  id: string;
  name: string;
  category: Category;
  description: string;
  repoUrl: string;
}

type Category =
  | "Webhooks Gateway"
  | "Webhook Testing"
  | "Webhook Infrastructure"
  | "Automation"
  | "Cloud Integration";
```

## MVP Features

### 1. Main Page - Hook Grid Display
**Route:** `/` (home page)

**Components:**
- **Header** - Simple branding with "HookHub" title
- **CategoryFilter** - Horizontal list of category pills for filtering
- **HookGrid** - Responsive grid displaying hook cards
- **HookCard** - Individual card showing:
  - Hook name (prominent)
  - Category badge
  - Description (truncated to 2-3 lines)
  - "View Repo" button/link to GitHub

**Grid Layout:**
- Desktop (lg+): 3 columns
- Tablet (md): 2 columns
- Mobile: 1 column
- Gap: 24px between cards

### 2. Category Filtering
- Click a category pill to filter hooks
- "All" option to show everything
- Active category visually highlighted

### 3. Data Source
Static TypeScript file with hook data:
```
/data/hooks.ts
```

Initial seed data includes popular open-source webhook projects:
- Hook0 - Webhooks Gateway
- Convoy - Webhooks Gateway
- Webhook.site - Webhook Testing
- adnanh/webhook - Automation
- Svix - Webhook Infrastructure
- Outpost - Webhook Infrastructure

## File Structure

```
hookhub/
├── app/
│   ├── page.tsx          # Main grid page
│   └── layout.tsx        # Root layout
├── components/
│   ├── Header.tsx
│   ├── CategoryFilter.tsx
│   ├── HookGrid.tsx
│   └── HookCard.tsx
├── data/
│   └── hooks.ts          # Static hook data
├── types/
│   └── hook.ts           # TypeScript interfaces
└── spec/
    └── CLAUDE.md         # This file
```

## Implementation Steps

1. **Create type definitions** (`types/hook.ts`)
   - Define `Hook` interface
   - Define `Category` type
   - Export `CATEGORIES` array

2. **Add seed data** (`data/hooks.ts`)
   - Create array of 6-8 initial hooks with real data from popular webhook projects

3. **Build components:**
   - `Header.tsx` - Simple header with logo/title
   - `HookCard.tsx` - Card component displaying individual hook
   - `HookGrid.tsx` - Grid container with responsive layout
   - `CategoryFilter.tsx` - Filter pills with state management

4. **Update main page** (`app/page.tsx`)
   - Import components
   - Add category filter state
   - Render header, filter, and grid

## UI Design Notes

- Clean, minimal aesthetic
- Dark mode support (already in Tailwind config)
- Cards with subtle shadow and rounded corners
- Hover effects on cards and buttons
- Category badges with color coding per category

## Out of Scope (Future Iterations)
- Search functionality
- User submissions
- Backend/database
- Authentication
- Pagination
- Sorting options

## Verification
1. Run `npm run dev` in the hookhub directory
2. Navigate to http://localhost:3000
3. Verify:
   - Grid displays all hooks
   - Category filter works correctly
   - Cards show name, category, description, and repo link
   - Responsive layout works on different screen sizes
   - Dark mode toggle works
