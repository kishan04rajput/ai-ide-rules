---
name: coding-in-react-native-expo
description: Best practices and rules for coding in React Native Expo projects, specifically using Expo Router.
---

# Coding in React Native (Expo)

Follow these rules and best practices when working on React Native projects with Expo and Expo Router.

## 1. Project Structure & Routing (Expo Router)

*   **File-Based Routing**: Use the `app/` directory. Files in `app/` become routes.
    *   `index.tsx` -> `/`
    *   `settings.tsx` -> `/settings`
    *   `(tabs)/_layout.tsx` -> Layout for a tab group.
    *   `[id].tsx` -> Dynamic route (e.g., `/user/123`).
*   **Layouts**: Use `_layout.tsx` to define navigation structure (Stack, Tabs, Drawer) and wrap screens.
    *   Example: `export default function Layout() { return <Stack />; }`
*   **Link**: Use `<Link href="/path" asChild>` from `expo-router` for navigation.

## 2. Components & Styling

*   **Core Components**: Use `View`, `Text`, `Image`, `TouchableOpacity` from `react-native`. **Do not use HTML tags** (`div`, `p`, `img`).
*   **Reusability**: Break UI into small, focused components. If a component is used in **2 or more files**, move it to a shared `src/components/` directory and import it.
*   **Styling**:
    *   **NativeWind (Tailwind)**: If configured, use `className` props.
    *   **StyleSheet**: Otherwise, use `StyleSheet.create`. Avoid inline styles for performance.
*   **Responsive**: Use `useWindowDimensions` for responsive logic if needed, but prefer flexible layouts (Flexbox).
*   **SafeArea**: Use `SafeAreaView` from `react-native-safe-area-context` to handle notches and navigation bars properly.

## 3. UI/UX Best Practices

*   **Platform Specifics**: Use `Platform.OS` or `.ios.tsx` / `.android.tsx` extensions for platform-specific variations.
*   **Gestures**: Use `react-native-gesture-handler` for advanced gestures.
*   **Swiping**: Use the `react-native-pager-view` package for gesture-based swiping.
*   **Images**: Use `expo-image` for optimized image loading.
*   **Pull to Refresh**: **Compulsory on all Screens**. Use the `refreshControl` prop on `ScrollView`.
*   **Skeleton Loaders**: **Compulsory for Data Loading**. When loading data, always show skeleton loading with shimmers effect, do not show spinner.
    *   **Creation**: If a page lacks a skeleton loader, create one that mirrors the page's layout.
    *   **Sync Maintenance**: When updating a page's UI, simultaneously update its skeleton loader to maintain visual consistency.

## 4. State & Logic

*   **Hooks**: Use Functional Components with Hooks (`useState`, `useEffect`, `useCallback`).
*   **Async Storage**: Use logic inside `useEffect` or event handlers.
*   **Custom Hooks**: Extract reusable logic into distinct hook files (e.g., `src/hooks/useAuth.ts`).
*   **State Management**: If a state variable is used in **2 or more files**, create a Context (`createContext`) to manage it. Always create a custom hook (e.g., `useMyContext`) to consume the context easily. Avoid excessive prop drilling.
    *   **API Integration**: If context state relies on an API response, **make the API call inside the Context**. Expose the state so all consuming files are updated simultaneously with fresh data.
*   **Component Structure**: strict order inside components:
    1.  State declarations & Hooks
    2.  Helper functions & Event handlers
    3.  `useEffect` **with** dependencies
    4.  `useEffect` **without** dependencies
    5.  `return` (UI JSX)

## 5. Performance

*   **Lists**: ALWAYS use `FlatList` or `SectionList` for long lists. Never `map` inside a `ScrollView`.
*   **Memoization**: Use `React.memo`, `useMemo`, and `useCallback` to prevent unnecessary re-renders.

## 6. Expo APIs

*   **Installation**: Use `npx expo install package-name` to ensure version compatibility.
*   **Permissions**: Handle permissions properly using Expo's permission hooks (e.g., `useCameraPermissions`).
*   **Fonts**: Load fonts in the root layout using `useFonts`.

## 7. API & Data Fetching

*   **Centralization**: All API calls must be made from the `src/services/api/` directory.
*   **Organization**: Group endpoints by feature (e.g., `src/services/api/profile.ts`).
*   **Separation**: Do not invoke `fetch` or `axios` directly in UI components; import functions from the services.
*   **Priority**: **Prefer making API calls in a Context** if the data is even slightly likely to be shared. Only make calls in individual files if the data is strictly local and ephemeral.
*   **Null Safety**: ALWAYS handle cases where API response data is `null` or empty in UI components. Show loading states or empty placeholders; never assume data exists.

## 8. Naming Conventions

*   **Files**:
    *   **Screens/Routes (`app/`)**: `kebab-case` (e.g., `src/app/handover-to-rider.tsx`).
    *   **Components**: `PascalCase` (e.g., `src/components/UserProfile.tsx`).
    *   **Hooks**: `camelCase`, prefixed with `use` (e.g., `src/hooks/useAuth.ts`).
    *   **Utilities/Services**: `camelCase` (e.g., `src/services/apiService.ts`, `src/utils/dateUtils.ts`).
*   **Code**:
    *   **Component Names**: `PascalCase` (e.g., `function UserProfile() {}`).
    *   **Variables/Functions**: `camelCase` (e.g., `updatedUser`, `fetchData()`).
    *   **Constants**: `UPPER_SNAKE_CASE` for global constants (e.g., `API_URL`).
    *   **Types/Interfaces**: `PascalCase` (e.g., `UserData`, `AuthResponse`).

## 9. Code Quality & Principles

*   **Minimalism**: Always code with the minimum amount of code that will make the feature working or resolve the bug, do not make the code bulky.
*   **DRY (Don't Repeat Yourself)**:
    *   **Logic**: If you copy-paste logic 2+ times, extract it into a utility function or custom hook.
    *   **UI**: If you copy-paste JSX 2+ times, extract it into a reusable component.
    *   **Constants**: Hardcoded strings/numbers used multiple times must be moved to a constants file.
    *   **Utility Functions**: If a function in a file is a utility function (pure logic, no UI, reusable), generalize its name and parameters, create it in the `src/utils/` folder (e.g., `src/utils/dateUtils.ts`, `src/utils/stringUtils.ts`), and import it where needed.

## 10. Common Pitfalls to Avoid

*   ❌ Don't use `window` or `document` objects (unless inside a web-only check).
*   ❌ Don't default to hardcoded pixel values for layout; use Flexbox.
*   ❌ Don't leave `console.log` in production code.
