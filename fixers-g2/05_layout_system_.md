# Chapter 5: Layout System

In [Chapter 4: Global Application Providers](04_global_application_providers_.md), we saw how to equip our application with essential background services like translation and data fetching. Now, let's turn our attention to the visual structure: how do we organize the different parts of our user interface on the screen? This is where the **Layout System** comes into play.

## The Blueprint of Your App's Interface

Imagine you're designing a house. You wouldn't just throw rooms, doors, and windows together randomly. You'd need an architectural blueprint to define where the main entrance is, where the living room goes, how hallways connect different areas, and where the bedrooms are.

**The Problem:** Without a consistent way to arrange UI elements, every page in your application could look drastically different.
*   The navigation bar might be on top on one page, and on the side on another.
*   Headers might have different styles and placements.
*   Content areas could vary wildly, making the app feel disjointed and confusing for users.

**The Solution: A Layout System!**
The `fixers-g2` project provides a set of components that act as an architectural blueprint for your application's UI. These components, such as `AppLayout`, `Page`, `Section`, and `Header`, provide consistent containers and arrangements for:
*   Navigation (like a top app bar or a side drawer).
*   Main content areas where specific page information is displayed.
*   Headers and footers for pages or sections.

This ensures a predictable and organized user experience as users navigate through different parts of your application.

**Our Use Case:** We want to build a simple "User Dashboard" page. This page should:
1.  Have a main application bar at the top (for branding or global actions).
2.  Display a clear title for the dashboard, like "User Dashboard".
3.  Have a dedicated area for the dashboard's content, perhaps a section for "Profile Summary".

Let's see how `fixers-g2` layout components help us build this.

## Core Layout Components: The Building Blocks

The layout system provides several key components. Let's explore the most common ones.

### 1. `AppLayout`: The Master Skeleton

Think of `AppLayout` as the main frame or skeleton of your entire application. It typically defines the persistent parts of your UI, like:
*   A top **App Bar** (for the application title, logo, or global navigation/actions).
*   A side **Drawer** (for more detailed navigation, often collapsible).
*   A main **content area** where the content of individual pages will be displayed.

You usually wrap your entire application's page content with `AppLayout` (or a component like `App` which uses `AppLayout`).

```jsx
// Simplified example of using AppLayout
import { AppLayout } from '@komune-io/g2-layout';
import { Typography } from '@mui/material'; // For simple text

function MyAppShell({ children }) {
  return (
    <AppLayout
      appBarContent={<Typography variant="h6">My App</Typography>}
      drawerContent={<p>Navigation Links Here</p>}
      open={true} // Let's assume the drawer is open
    >
      {/* Page content will go here */}
      {children}
    </AppLayout>
  );
}
```
**Explanation:**
*   `import { AppLayout } from '@komune-io/g2-layout';`: We import the main layout component.
*   `appBarContent`: We provide content for the top app bar (e.g., the app's name).
*   `drawerContent`: We provide content for the side navigation drawer.
*   `open={true}`: This prop would typically control whether the drawer is visible.
*   `{children}`: This is where the content of the current page (like our "User Dashboard") will be rendered.

**Output:** This sets up a basic application structure with a top bar saying "My App", an open side drawer with "Navigation Links Here", and a main area ready for specific page content.

The `App` component (`packages/layout/src/App/App.tsx`) is a more feature-rich component built upon `AppLayout`, often used as a convenient way to set up the entire application shell with menus, titles, and toolbars.

### 2. `Page`: Structuring Individual Views

While `AppLayout` defines the global shell, the `Page` component is used to structure the content of a single, specific view or screen within your application. It often includes its own header area for the page title or page-specific actions.

```jsx
// Using Page inside our AppLayout
import { Page, Header } from '@komune-io/g2-layout';
import { Typography } from '@mui/material';

function UserDashboardPage() {
  return (
    <Page
      headerProps={{
        content: [{ leftPart: [<Typography variant="h5">User Dashboard</Typography>] }]
      }}
    >
      <p>Welcome to your dashboard!</p>
      {/* More dashboard content will go here */}
    </Page>
  );
}
```
**Explanation:**
*   `import { Page, Header } from '@komune-io/g2-layout';`: We import `Page`. (Note: `Header` is often used by `Page` via `headerProps`).
*   `headerProps`: This prop allows us to configure a `Header` component that belongs to this `Page`.
    *   `content: [...]`: We're defining what the header should display. Here, a "User Dashboard" title on the left.
*   `{children}`: The main content of the User Dashboard page (e.g., "Welcome to your dashboard!").

**Output:** Inside the main content area provided by `AppLayout`, this `Page` component would render. It would have its own header section displaying "User Dashboard", and below that, the text "Welcome to your dashboard!".

### 3. `Header`: Titles, Actions, and Tabs

The `Header` component is versatile. It can be used:
*   Within a `Page` (as seen above, configured via `headerProps`) for page titles, actions, or tabs.
*   Within a `Section` (see below) for section-specific headers.
*   Sometimes standalone, if needed.

It helps organize information at the top of a content block.

```jsx
// A more direct look at Header, though often used via Page/Section
import { Header } from '@komune-io/g2-layout';
import { Button, Typography } from '@mui/material';

function MyCustomHeader() {
  return (
    <Header
      content={[{
        leftPart: [<Typography variant="h6">Section Title</Typography>],
        rightPart: [<Button size="small">Edit</Button>]
      }]}
      withBottomDivider={true} // Adds a line below the header
    />
  );
}
```
**Explanation:**
*   `content`: An array defining lines in the header. Each object can have `leftPart` and `rightPart`.
    *   `leftPart`: Displays "Section Title".
    *   `rightPart`: Displays an "Edit" button.
*   `withBottomDivider`: Adds a subtle visual separator.

**Output:** This would render a header area with "Section Title" on the left, an "Edit" button on the right, and a line underneath.

### 4. `Section`: Grouping Content Visually

A `Section` component is typically used within a `Page` to group related content into visually distinct blocks, often styled like a card or a panel. It can also have its own `Header`.

```jsx
// Using Section inside our UserDashboardPage
import { Section, Header } from '@komune-io/g2-layout'; // Header can be used by Section too
import { Typography } from '@mui/material';

function UserDashboardPageContent() {
  return (
    <>
      <p>Welcome to your dashboard!</p>
      <Section
        headerProps={{
          content: [{ leftPart: [<Typography variant="subtitle1">Profile Summary</Typography>] }]
        }}
        sx={{ marginTop: 2 }} // Add some space above the section
      >
        <p>Name: John Doe</p>
        <p>Email: john.doe@example.com</p>
      </Section>
    </>
  );
}
```
**Explanation:**
*   `import { Section } ...`: We import the `Section` component.
*   `headerProps`: Similar to `Page`, `Section` can have its own `Header` configured. Here, it's for the "Profile Summary" title.
*   `sx={{ marginTop: 2 }}`: We add a bit of styling for spacing.
*   `{children}`: The actual content of the profile summary.

**Output:** Below the "Welcome to your dashboard!" message, this `Section` would appear as a distinct block (often with a subtle background or border). It would have its own header "Profile Summary", followed by the name and email.

## Solving Our Use Case: The "User Dashboard"

Now let's combine these components to build our "User Dashboard" page structure.

```jsx
// Full structure for UserDashboardPage within an AppLayout
import { AppLayout, Page, Section, Header } from '@komune-io/g2-layout';
import { Typography, Button } from '@mui/material';

function UserDashboard() {
  return (
    <AppLayout
      appBarContent={<Typography variant="h6">MyApp Central</Typography>}
      open={false} // Let's say drawer is closed by default
    >
      <Page
        headerProps={{
          content: [{
            leftPart: [<Typography variant="h5">User Dashboard</Typography>],
            rightPart: [<Button variant="outlined">Settings</Button>]
          }]
        }}
      >
        <Typography variant="body1" sx={{ marginBottom: 2 }}>
          Welcome, User! Here's your overview.
        </Typography>
        <Section
          headerProps={{
            content: [{ leftPart: [<Typography variant="subtitle1">Profile Summary</Typography>] }]
          }}
        >
          <p>Name: Alex Query</p>
          <p>Email: alex@example.com</p>
          <p>Status: Active</p>
        </Section>
        {/* You could add more Sections here for other dashboard items */}
      </Page>
    </AppLayout>
  );
}
```
**Output/Effect:**
This code would render a complete page structure:
1.  A top app bar with the title "MyApp Central".
2.  The main content area would be occupied by the "User Dashboard" `Page`.
3.  This `Page` would have its own header displaying "User Dashboard" on the left and a "Settings" button on the right.
4.  Below the page header, a welcome message "Welcome, User! Here's your overview."
5.  Below the welcome message, a `Section` titled "Profile Summary" would appear, containing the user's name, email, and status.

This creates a well-structured, consistent, and easy-to-understand layout for the user.

## Under the Hood: How Layout Components Fit Together

These layout components are designed to nest and work together. `AppLayout` provides the outer shell, `Page` fits into `AppLayout`'s content area, and `Section`s fit within a `Page`.

**Step-by-Step (Conceptual):**

1.  **`AppLayout` Renders:** It sets up its app bar, a space for the drawer, and a main content placeholder.
2.  **`Page` Renders into `AppLayout`:** The `Page` component (passed as `children` to `AppLayout`) fills the main content placeholder.
3.  **`Page`'s `Header` Renders:** If `headerProps` are provided to `Page`, it renders its own `Header` component at the top of its own content area.
4.  **`Page`'s Content Renders:** The children of the `Page` component (like text or `Section`s) are rendered below its header.
5.  **`Section` Renders into `Page`:** If a `Section` is a child of `Page`, it renders as a distinct block.
6.  **`Section`'s `Header` Renders:** If `headerProps` are provided to `Section`, it renders its own `Header` at the top of its content.
7.  **`Section`'s Content Renders:** The children of the `Section` are rendered within it.

Here's a simplified diagram of this nesting:

```mermaid
graph TD
    A[AppLayout] --> B{App Bar}
    A --> C{Drawer Area}
    A --> D[Main Content Area]

    subgraph D [Main Content Area]
        P[Page]
    end

    subgraph P [Page]
        PH[Page Header (via headerProps)]
        PC[Page Children]
    end

    subgraph PC [Page Children]
        S[Section]
        T[Other Text/Components]
    end

    subgraph S [Section]
        SH[Section Header (via headerProps)]
        SC[Section Content]
    end
```

### A Glimpse into Component Code

Let's look at *very simplified* snippets to understand their structure.

**Simplified `AppLayout.tsx` (from `packages/layout/src/AppLayout/AppLayout.tsx`):**
```tsx
// Simplified AppLayout
export const AppLayout = (props) => {
  const { appBarContent, drawerContent, children, open, showAppBar = true } = props;
  // ... logic to handle drawer open/close, styles ...

  return (
    <>
      {showAppBar && (
        <AppBarLayout /* ... props ... */ >
          {appBarContent}
        </AppBarLayout>
      )}
      <Drawer open={open} /* ... props ... */ >
        {drawerContent}
      </Drawer>
      <main className={open ? "content-shifted" : "content-normal"}>
        {children} {/* Where Page component goes */}
      </main>
    </>
  );
};
```
**Explanation:**
*   It receives `appBarContent`, `drawerContent`, and `children` as props.
*   It renders an `AppBarLayout` (another layout helper for the app bar itself) and a `Drawer`.
*   The `children` prop is rendered inside a `<main>` HTML element, which acts as the primary content area. Styles might shift this `main` area when the drawer `open` state changes.

**Simplified `Page.tsx` (from `packages/layout/src/Page/Page.tsx`):**
```tsx
// Simplified Page
export const Page = (props) => {
  const { headerProps, children, sx, ...other } = props;

  return (
    <Box sx={{ padding: 3, ...sx }} {...other}>
      {headerProps && <Header {...headerProps} strongPadding />}
      {children} {/* Where Sections or other content goes */}
    </Box>
  );
};
```
**Explanation:**
*   It accepts `headerProps` to configure its `Header`.
*   It renders the `Header` if `headerProps` are provided.
*   It then renders its `children` (the main content of the page, like `Section`s).
*   `Box` is a general-purpose layout component from Material UI, used here for padding.

**Simplified `Section.tsx` (from `packages/layout/src/Section/Section.tsx`):**
```tsx
// Simplified Section
export const Section = (props) => {
  const { headerProps, children, sx, ...other } = props;

  return (
    <Paper elevation={0} sx={{ overflow: 'hidden', ...sx }} {...other}>
      {headerProps && <Header bgcolor="#ffffff" {...headerProps} />}
      <Box sx={{ padding: 2 }}>
        {children} {/* Content of the section */}
      </Box>
    </Paper>
  );
};
```
**Explanation:**
*   It often uses `Paper` (from Material UI) to give it a card-like appearance.
*   Like `Page`, it can have its own `Header` via `headerProps`.
*   The `children` are rendered within a padded `Box`.

All these layout components, and more, are typically exported from the main `index.ts` file of the layout package (`packages/layout/src/index.ts`), making them easy to import and use:
```typescript
// Simplified from: packages/layout/src/index.ts
export { AppLayout } from './AppLayout';
export { Page } from './Page';
export { Header } from './Header';
export { Section } from './Section';
// ... and other layout components
```

## Conclusion

The Layout System in `fixers-g2` provides the essential tools (`AppLayout`, `Page`, `Header`, `Section`, etc.) to define the overall structure and arrangement of UI elements within your application. Like an architect's blueprint, these components ensure a consistent, organized, and predictable user experience across different views.

By using these layout "building blocks," you can construct interfaces that are not only functional but also feel coherent and professionally designed.

With our application's structure and global services in place, we often need to collect input from users. Let's explore how `fixers-g2` simplifies this in [Chapter 6: Form Abstraction](06_form_abstraction_.md).

---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)