# Fitness App - AI Agent Instructions

## Project Overview
React + Vite fitness application with Firebase hosting integration. Early-stage project with architectural preferences defined but minimal implementation.

## Architecture Principles

### Component Organization 
- **Strict separation of concerns**: Components handle only presentation and UI structure
- **No business logic in components**: Extract all logic into utility functions
- **Action-based organization**: Group utilities by action type in dedicated files:
  - `userActions.js` - user-related operations
  - `dataActions.js` - data manipulation
  - `formatActions.js` - formatting utilities
- Components call these utilities for events, API calls, and computations

**Example pattern:**
```jsx
// ❌ Avoid - logic in component
function UserProfile() {
  const handleSubmit = (data) => {
    const formatted = data.name.trim().toLowerCase();
    fetch('/api/users', { method: 'POST', body: JSON.stringify(formatted) });
  }
}

// ✅ Preferred - delegate to actions
import { submitUser } from './actions/userActions';
function UserProfile() {
  const handleSubmit = (data) => submitUser(data);
}
```

### UI Design System 
- **Component library**: Use shadcn basic UI components for all UI elements
- **Typography**: Poppins for headings, Inter for body text
- **Fitness-themed color palette**:
  ```css
  --primary: #16A34A        /* emerald green */
  --secondary: #22C55E      /* light green accent */
  --background: #0F172A     /* dark navy */
  --surface: #1E293B        /* slate gray panels */
  --text-primary: #F8FAFC   /* almost white */
  --text-secondary: #94A3B8 /* muted gray */
  ```
- **Spacing & styling**: Generous spacing, rounded corners (2xl), subtle shadows for depth

## Tech Stack
- **Frontend**: React 19.1.1, Vite 7.1.7
- **Backend/Hosting**: Firebase (hosting config in `firebase.json`, initialized in `src/firebase/index.js`)
- **Linting**: ESLint 9 with React Hooks plugin
- **Build tool**: Vite with HMR

## Key Commands
```bash
npm run dev       # Start dev server with HMR
npm run build     # Production build
npm run lint      # Run ESLint
npm run preview   # Preview production build
```

## Development Workflows

### Firebase Deployment
- Region: `europe-west1` (configured in `firebase.json`)
- Firebase config is public-facing (in `src/firebase/index.js`)
- Use Firebase CLI for deployment: `firebase deploy`

### ESLint Configuration
- Custom rule: Unused variables with uppercase or underscore prefix are allowed (`varsIgnorePattern: '^[A-Z_]'`)
- React Hooks rules enforced at recommended-latest level
- Targets ES2020+ with browser globals

## File Structure Conventions
```
src/
  actions/           # Business logic utilities (user/data/format actions)
  components/        # Presentation components only
  firebase/          # Firebase initialization and config
  assets/            # Static resources
```

## Important Notes
- Firebase API keys are committed to repo (public client keys)
- No TypeScript - pure JavaScript/JSX codebase
- React Compiler not enabled (per README performance considerations)
- ESM modules throughout (`"type": "module"` in package.json)
