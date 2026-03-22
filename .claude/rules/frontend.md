---
paths:
  - "src/app/**"
  - "src/environments/**"
---

# Frontend Development Rules

## Angular Material First (MANDATORY)
- Before creating ANY UI component, check if Angular Material has it
- NEVER create custom implementations of: Button, Input, Select, Checkbox, Slide Toggle, Dialog, Snackbar, Table, Tabs, Card, Badge, Menu, Tooltip, Navigation, Sidenav, Breadcrumb, Progress Bar, Spinner
- Import Angular Material modules directly in standalone component imports array
- Custom components are ONLY for business-specific compositions that internally use Angular Material

## Import Pattern
```typescript
import { MatButtonModule } from '@angular/material/button';
import { MatCardModule } from '@angular/material/card';
import { MatInputModule } from '@angular/material/input';

@Component({
  standalone: true,
  imports: [MatButtonModule, MatCardModule, MatInputModule],
})
```

## Component Standards
- ALL components must be standalone (`standalone: true`)
- Use `inject()` function instead of constructor injection
- Use `OnPush` change detection for all components
- Use signals (`signal()`, `computed()`, `linkedSignal()`) for reactive state
- Use Tailwind CSS for custom layout/spacing (Angular Material for components)
- All components must be responsive (mobile 375px, tablet 768px, desktop 1440px)
- Implement loading states, error states, and empty states
- Use semantic HTML and ARIA labels for accessibility

## State Management
- Shared/cross-component state lives in Angular Services (`@Injectable({ providedIn: 'root' })`)
- Use `signal()` inside services for reactive state
- Component-local state may use `signal()` directly in the component
- NEVER use `BehaviorSubject` or `Observable` where signals suffice

## Forms (Angular Signal Forms)
- Use Angular Signal Forms for all form handling
- Define Zod schemas for validation logic
- Integrate Zod validation with Signal Forms via custom validators

## Auth Best Practices
- Use Angular Route Guards (`CanActivateFn`) to protect routes
- Store auth state in a dedicated `AuthService`
- Use `Router.navigate()` for post-login redirects
- Always handle loading state in all code paths (success, error, finally)
