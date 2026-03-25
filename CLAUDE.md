# Project: Next.js Dashboard App

## Context
The user is learning web development by following the official Next.js Dashboard App tutorial (https://nextjs.org/learn/dashboard-app/getting-started). This is their second Next.js project — they previously completed React Foundations in a separate repo (`react-foundations-next`), where they built up from CDN-based React to a basic Next.js App Router setup.

**Learning path so far:** Express/Node.js (MDN Local Library) -> React Foundations -> **Next.js Dashboard App (current)**

## Learning style
- Prefers **short answer** quiz questions, not multiple choice
- Learns by building and being quizzed on what was built
- Responds well to targeted drilling on missed concepts
- Wants questions to stay focused on what's in the codebase — skip topics not yet covered in reading
- Asks good conceptual "why" questions between quiz rounds — engage with these fully

## Prior knowledge
### From Express project
- Strong grasp of: MVC, HTTP methods, middleware, forms, validation/sanitization, Mongoose/MongoDB, template rendering, server-side concepts
- JavaScript fundamentals: truthiness, equality operators, async/await, Promises

### From React Foundations (130 questions across 13 rounds)
- **Solid on**: Components, JSX, props (destructuring, read-only, data flow), state (`useState`, batching, functional updaters), event handlers, keys in lists, `.map()` rendering, fragments, `createElement` internals, server vs client components, `'use client'` directive, file-based routing, `layout.js`/`page.js` conventions, `metadata` export, hydration
- **Needs revisiting**: Duplicate keys (rendering bugs vs errors), expressions vs statements in JSX, unused props silently ignored, props object always `{}` not `undefined`, hooks call order (why no conditionals), lifting state up (pass setter as prop not import), reconciliation (virtual DOM diffing), state updates as const snapshots (not DOM reads), `useState()` with no arg = `undefined`
- **Conceptual**: Babel compilation pipeline, React as abstraction over DOM APIs, server components don't ship JS, `??` vs `||`

## Current project status
- **Stage**: Chapter 11 — Mutating Data (completed)
- **Framework**: Next.js (latest), React (latest), TypeScript, Tailwind CSS
- **New for this project**: TypeScript (`.tsx` files), Tailwind CSS, postgres, bcrypt, next-auth, zod
- **Deployment**: Vercel (auto-deploys from GitHub `main` branch), Postgres database hosted in cloud (Neon/Supabase via Vercel)
- **What exists**: Landing page, root layout with Inter font, dashboard layout with SideNav, dashboard page with streaming (Suspense boundaries around revenue chart, latest invoices, and cards), `loading.tsx` with skeleton in `(overview)` route group, invoices page with search/pagination/table and full CRUD (create/edit/delete via Server Actions), Zod validation in actions, one placeholder page (customers), data layer in `app/lib/` (data.ts for fetching, actions.ts for mutations), seeded database with all four tables populated
- **Routes**: `/` (landing), `/dashboard`, `/dashboard/invoices`, `/dashboard/invoices/create`, `/dashboard/invoices/[id]/edit`, `/dashboard/customers`
- **Pre-built UI components**: Dashboard (sidenav, nav-links, revenue-chart, cards, latest-invoices), Invoices (table, create/edit forms, pagination, buttons, breadcrumbs, status), Customers (table), search, skeletons, login-form, button, acme-logo

## Quiz progress
- 341 questions across 29 rounds (130 from React Foundations + 211 in this project)
- Score trend: 5.5 -> 5 -> 5.5 -> 7 -> 6.5 -> 6 -> 5.5 -> 8 -> 6 -> 5.5 -> 7 -> 6 -> 7.5 -> 4.5 -> 6.5 -> 6 -> 6.5 -> 7.5 -> 9 -> 7.5 -> 7.5 -> 9.5 -> 5 -> 6 -> 7.5 -> 5.25 -> 6.375 -> 6.5 -> 6.75
- Round 14: 4.5/10 (high-level architecture — first round in new project, many new concepts)
- Round 15: 6.5/10 (architecture deep dive — data layer, SQL, server-side patterns)
- Round 16: 6/10 (system architecture — database design, data flow, Next.js patterns)
- Round 17: 6.5/10 (components, forms, user journey — strong on Express-overlapping concepts)
- Round 18: 7.5/10 (CSS styling — Tailwind, CSS Modules, clsx)
- Round 19: 9/10 (all-encompassing review)
- Round 20: 7.5/10 (all-encompassing review)
- Round 21: 7.5/10 (layouts and routes — strong on nesting/scoping, gaps in Tailwind layout utilities)
- Round 22: 9.5/10 (database setup & deployment — new personal best)
- Round 23: 5/10 (data fetching — new chapter, many new concepts: promises, TypeScript generics, waterfall problem)
- Round 24: 6/10 (data fetching reinforcement — waterfall/parallel solid, gaps in client vs server async, Promise.all vs transactions)
- Round 25: 7.5/10 (streaming & Suspense — strong on architecture/streaming concepts, gaps in Suspense mechanics)
- Round 26: 5.25/10 (search & pagination — 20 hard questions; strong on SQL/database side, gaps in URL mechanics and client-side patterns)
- Round 27: 6.375/10 (full revisit round — 41 questions covering all "needs revisiting" items; strong on SQL/database, React fundamentals, URL params; gaps in TypeScript features, controlled vs uncontrolled inputs, replace vs push, bcrypt)
- Round 28: 6.5/10 (mutating data — Chapter 11; solid on Zod, revalidatePath/redirect, dynamic routes, FormData, progressive enhancement; gaps in Server Actions vs server components, .bind() pattern, server-generated fields, form client component reasoning)
- Round 29: 6.75/10 (mutation architecture — strong on practical flow decisions: redirect logic, page/form split, data needs; tendency to default to "reduces complexity" instead of naming specific benefits like security, reusability, framework integration)

### Topics now understood (from Rounds 14-29):
- Four data entities: users (login), customers (invoiced), invoices, revenue — separate tables for separate roles
- `route.ts` with exported `GET`/`POST` creates API routes at that path
- File-based routing requires `page.tsx` — `ui/` folder is just component organization, not routes
- Creating a route = folder + `page.tsx`
- `Promise.all` for parallel independent queries — performance benefit
- Forms with Server Actions for mutations (sign out button in `<form>`)
- Storing money in cents avoids floating point precision errors — convert at display layer
- JOINs connect foreign keys to human-readable data (like Mongoose `.populate()`)
- `LIMIT` + `OFFSET` = database-level pagination
- Request flow: navigate -> skeleton shows -> server component awaits data -> HTML streams to browser replacing skeleton
- Environment variables for secrets (same as Express)
- `@/` path alias = project root shortcut
- `global.css` must be explicitly imported in layout — initializes Tailwind via `@tailwind` directives
- Orphaned foreign keys: deleting a customer leaves invoices pointing to nothing — need FK constraints
- Multiple small queries > one big query: enables independent loading per section + parallel execution
- Database transactions (`sql.begin`) = atomic `Promise.all` — all succeed or all roll back
- Data transformation (cents -> "$14.95") belongs in data-fetching layer, not SQL or UI
- No API layer advantage: simplicity — server component calls data function directly, one layer instead of route+controller+fetch+loading
- `<a>` tags cause full page reloads — `<Link>` enables client-side navigation (keeps layout mounted)
- Page components fetch data, pass to child components as props — children just render
- Client-side validation (required, minLength) insufficient — users can bypass via devtools or raw requests
- `name` attribute on form inputs becomes the key in submitted form data (same as Express `req.body`)
- `<Link>` for navigation-only actions (like cancel buttons) — simpler than onClick + useRouter
- Hooks need client components because server components run once and are gone — hooks need a component that stays alive in the browser and can re-run
- User journey: landing page (`/`) -> login (`/login`) -> dashboard (`/dashboard`) -> invoices -> create invoice
- **Tailwind**: Utility-class system — predefined single-purpose CSS classes (`flex`, `p-6`, `bg-blue-500`), each maps to one CSS property, assembled inline in JSX
- **CSS Modules**: Scoped traditional CSS — write regular CSS in `*.module.css` files, import as object, auto-generates unique class names to prevent collisions
- **`clsx`**: Combines class names with conditional logic — works with Tailwind, CSS Modules, or any class names
- **`@tailwind` directives** in `global.css` inject Tailwind's CSS rules — without them, Tailwind classes do nothing
- **`md:` prefix**: Responsive breakpoint — style applies at medium screens (768px+) and above
- CSS Modules scope by file — two files can define `.shape` without conflict
- **`className` history**: HTML `class` = CSS styling, JS `class` = object blueprints. JS DOM API used `className` to avoid keyword conflict. React mirrors JS DOM API, so JSX uses `className`
- `className` assigns CSS class labels to elements; actual style definitions live in Tailwind's library, CSS Module files, or global CSS
- DOM API is not a separate language — it's browser-provided tools (functions/objects) added on top of JavaScript for interacting with HTML
- **`next/font`**: Downloads fonts at build time, bundles with app — no runtime dependency on Google's servers, no flash of unstyled text
- **`font.className`**: Font function returns an object, not a string — `.className` extracts the generated class name string
- **`<Image>` vs `<img>`**: Auto-optimization (compression, WebP), lazy loading, prevents layout shift, responsive sizing
- **`/public` folder**: Static file root — `src="/hero-desktop.png"` maps directly to `public/hero-desktop.png`, always (not a fallback)
- **Responsive image swap**: `hidden md:block` + `block md:hidden` shows different images per screen size
- **`antialiased`**: Tailwind class for smoother font rendering
- **Server Actions under the hood**: Next.js assigns unique ID to each action at build time → form submits POST to current URL with action ID + form data → Next.js routes to correct function → function receives `FormData` object → uses `.get('name')` to extract values (like Express `req.body.name`)
- **GET vs POST**: GET sends data in URL params (search queries), POST sends data in request body (form mutations) — same as Express
- **Express vs Next.js data flow**: Express has 3 layers (route → controller → template), Next.js has 2 (server component → data function) — component is both controller and template
- **Nested layouts stack**: Root layout (html/body/font) → dashboard layout (SideNav + content area) → page. Each adds its own piece, they don't replace each other.
- **`children` is a special React prop**: Content between component tags automatically becomes `children` — can't rename it
- **Next.js auto-wires layouts**: Reads folder structure and plugs pages into the nearest layout's `{children}` — no manual wiring
- **SideNav and `{children}` are siblings**: SideNav doesn't call or control `{children}` — they sit side by side in the layout. SideNav links trigger navigation, Next.js swaps `{children}`
- **Same function name across files**: No conflict — each file is its own module, names are scoped. Next.js only cares about `default export`
- **CSS font inheritance**: Inter font on `<body>` inherits down to all nested layouts and pages — no need to redeclare
- **`flex-none`**: Prevents element from growing or shrinking in flexbox — SideNav stays fixed at `w-64` (256px)
- **`overflow-hidden` + `overflow-y-auto`**: Parent clips to viewport (no page scroll), child content area scrolls independently — keeps SideNav fixed in place
- **Component libraries**: Most devs use pre-made components (shadcn/ui, MUI, Chakra) and customize — building from scratch is for learning
- **Deployment architecture**: Local app + Vercel app are separate instances, connected by GitHub (code) and the same cloud database (data)
- **Cloud database**: Accessible from anywhere with credentials — both local and deployed app connect independently
- **Region colocation**: Database and app in same region (D.C.) reduces query latency
- **CI/CD**: CI = automated tests/checks before deploy, CD = automatic deployment on push. This project has CD only (Vercel auto-deploys)
- **GitHub as bridge**: If GitHub goes down, local dev works, deployed app keeps running, but can't push or auto-deploy
- **Empty database needs setup**: `CREATE TABLE` defines structure, `INSERT` populates data — new databases have nothing
- **Sequential awaits = waterfall**: Each `await` blocks the next — independent queries should run in parallel
- **SQL COUNT returns strings**: Need `Number()` to convert for JavaScript use
- **SQL can't run JS functions**: Data transformation (e.g., `formatCurrency`) must happen in JS after the query returns
- **Data functions in shared files for reusability**: `app/lib/data.ts` lets multiple pages import the same fetch functions
- **Waterfall = sequential awaits**: Total time = sum of all queries; parallel = total time is slowest query
- **Rewriting waterfall to parallel**: Use `Promise.all` with array destructuring to await all fetches concurrently
- **`data[0][0].count`**: First `[0]` = first promise result from `Promise.all`, second `[0]` = first row of SQL result (SQL always returns array of rows)
- **Blank page during slow fetch**: Sequential awaits in page component block all rendering until every query finishes
- **`loading.tsx`**: Next.js convention — automatically wraps page in Suspense boundary with the exported component as fallback
- **`<Suspense>`**: Wraps individual components — shows `fallback` skeleton while async component inside loads, swaps in real content when ready
- **`loading.tsx` vs `<Suspense>`**: `loading.tsx` = whole page loading state, `<Suspense>` = fine-grained per-component loading
- **Route groups `(name)`**: Parenthesized folders are invisible to URL, scope special files like `loading.tsx` to only pages inside. Name can be anything
- **Streaming**: Server sends HTML chunks as each Suspense boundary resolves — user sees content progressively instead of waiting for everything
- **Components fetch their own data**: Each component calls its own fetch function, wrapped in Suspense — loads independently instead of waterfall
- **Next.js special files**: `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`, `not-found.tsx`, `route.ts`, `middleware.ts`
- **Skeletons prevent layout shift**: Match the shape/grid of real content so the page doesn't jump when data swaps in
- **Expressions vs statements in JSX**: Curly braces `{}` in JSX only allow expressions (produce a value), not statements like `const x = ...` or `await`
- **TypeScript union types**: `'pending' | 'paid'` restricts to specific values — TS feature, not Next.js (confirmed Round 27)
- **`ILIKE` vs `LIKE`**: `ILIKE` is case-insensitive, PostgreSQL-specific (confirmed Round 27)
- **Search/pagination state in URL params**: Not React state — URL is bookmarkable, shareable, survives refresh, server-readable (confirmed Round 27)
- **Server sets invoice date**: Server Action generates the date, not user input — prevents backdating (confirmed Round 27)
- **Promises fire immediately**: `sql\`...\`` sends the query and returns a promise right away — `Promise.all` doesn't start them, it waits for them to finish (confirmed Round 27)
- **TypeScript prop typing**: `{ revenue }: { revenue: Revenue[] }` — left side destructures props, right side declares their types (confirmed Round 27)
- **`Promise.all` fails fast**: Rejects immediately if any promise fails, but successful queries already ran and their effects stay. `sql.begin` rolls back all queries if any fail (confirmed Round 27)
- **Page fetching for children is a weakness**: Consolidating all fetches in the page creates waterfall — better pattern is each component fetching its own data (Suspense) (confirmed Round 27)
- **Suspense doesn't make functions complete faster**: It shows a fallback while the component loads — the async work takes the same time (confirmed Round 27)
- **Suspense needs a component**: Can't wrap raw JS/fetch calls in Suspense — the fetching must happen inside the component that Suspense wraps (confirmed Round 27)
- **`new URLSearchParams(searchParams)`**: Creates mutable copy — `useSearchParams()` returns read-only params (confirmed Round 27)
- **Non-clickable pagination items**: Active page and `...` ellipsis render as `<div>` not `<Link>` — nothing to navigate to (confirmed Round 27)
- **Search resets page to 1**: New search might have fewer results — requesting old page number could return nothing (confirmed Round 27)
- **Pagination offset formula**: `(currentPage - 1) * ITEMS_PER_PAGE` — database returns only the slice of rows needed (confirmed Round 27)
- **`useSearchParams`/`usePathname`/`useRouter`**: Client-side hooks for reading URL params, path, and navigating (confirmed Round 27)
- **Search component is client, Table is server**: Search handles user input (needs hooks), Table fetches from database (needs server) (confirmed Round 27)
- **SQL filtering with `ILIKE`**: Database does the filtering, not JavaScript — searches across multiple columns with `OR` (confirmed Round 27)
- **Unused props silently ignored**: No error, no warning — props just get ignored (confirmed Round 27)
- **Lifting state up**: Parent passes setter function as prop to child — child calls it, doesn't import it (confirmed Round 27)
- **Expressions vs statements in JSX (React Foundations)**: Expressions evaluate to a value (allowed in `{}`), statements don't (not allowed) (confirmed Round 27)
- **Duplicate keys**: Console warning not error — causes rendering bugs (wrong items update, reorder, lose state) (confirmed Round 27)
- **Zod validation**: Validates and coerces form data (strings to correct types) before database operations — server-side validation (confirmed Round 28)
- **`revalidatePath`**: Clears cached page data after mutations so fresh data shows on next request (confirmed Round 28)
- **`redirect` after revalidation**: Called after `revalidatePath` so user lands on page with fresh data, not stale cache (confirmed Round 28)
- **Dynamic routes `[id]`**: Bracket folders create dynamic route segments — different IDs hit same page component (confirmed Round 28)
- **Zod `.omit()` for server-generated fields**: `CreateInvoice` omits `id` (database generates) and `date` (server generates) from validation schema (confirmed Round 28)
- **`formData.get('fieldName')`**: Extracts individual values from FormData, field name matches input's `name` attribute (confirmed Round 28)
- **Delete action has no redirect**: User is already on invoices list — just revalidate to refresh data in place (confirmed Round 28)
- **`'use server'` file-level vs function-level**: File-level marks all exported functions as Server Actions; function-level marks only that function (confirmed Round 28)
- **Progressive enhancement**: Forms with Server Actions work without JavaScript — native HTML form submission sends POST, Server Action still processes it (confirmed Round 28)
- **Server page + client form split**: Pages are server components (fetch data from DB), forms are client components (need interactivity) — each uses the rendering mode it needs (confirmed Round 29)
- **Redirect depends on current route**: Delete = no redirect (already on list page), create/update = redirect (on separate pages that need to be left) (confirmed Round 29)
- **`revalidatePath` + `redirect` are both needed**: `redirect` alone lands on stale cached page — `revalidatePath` invalidates cache first (confirmed Round 29)
- **Edit page fetches customers list**: Customer select dropdown needs all customers as options so user can change the invoice's customer (confirmed Round 29)

### Topics that need revisiting (from Rounds 14-29):
- **TypeScript `!` (non-null assertion)**: Tells TS "trust me, this won't be null" — compile-time only, **zero runtime effect** (no protection if actually null). Partially known Round 27
- **Tagged template literals**: `sql\`...\`` calls `sql` as a **JavaScript function** with template parts — not just regular template literals. The function handles parameterization and sends query. Partially known Round 27
- **Skeletons = loading placeholders**: Show page structure during data fetch for **perceived performance**, not decoration. Partially known Round 27
- **Raw SQL vs ORM disadvantage**: **Portability and maintenance**, not injection risk — tagged template literals auto-parameterize. Missed Round 27
- **Seed route using GET is a shortcut**: Writing data should be POST (HTTP semantics); tutorial uses GET for browser convenience. Partially known Round 27
- **bcrypt salt rounds**: The `10` = **cost factor** (2^10 iterations), not password length or character count. Missed Round 27
- **Nested layouts**: Dashboard layout nests *inside* root layout — layouts **stack like nesting dolls**, each adds its piece. Partially known Round 27
- **Middleware for auth**: `middleware.ts` at project root intercepts every request — not per-page checks (like Express `app.use(authCheck)`). Skipped Round 27 (not yet built)
- **`Omit<Type, 'field'>` utility**: TypeScript built-in — **copies a type minus specified fields**, doesn't bypass restrictions. Missed Round 27
- **Dynamic nav links in database**: For **permission-based navigation** (different users see different links), not just dynamic updates. Partially known Round 27
- **`<Image>` benefits**: Auto-optimization (compression, WebP), lazy loading, layout shift prevention — name specific features. Partially known Round 27
- **Client components can't be async**: Must return JSX **immediately** for re-renders — `async` would pause the function, blocking the UI. Server components run once, so pausing is fine. Partially known Round 27
- **TypeScript generics (`sql<Revenue[]>`)**: **Compile-time type hint** telling TS the data shape — completely stripped at runtime, no effect on actual data. Missed Round 27
- **Waterfall blocks entire page**: The **page function itself** can't return any JSX until all `await`s finish — it's the page that's blocked, not child components blocking upward. Partially known Round 27
- **`replace` vs `push`**: About **browser history**, not performance — `replace` swaps current entry (no back-button clutter), `push` adds new entry. Search uses `replace`. Missed Round 27
- **`defaultValue` vs `value`**: About **control**, not performance — `defaultValue` = uncontrolled (browser manages), `value` = controlled (React manages, needs `useState`). Missed Round 27
- **Suspense `key` prop**: Changing the key destroys and remounts the component — triggers fallback skeleton for new search/page
- **`fetchInvoicesPages` not in Suspense**: Fast `COUNT(*)` query awaited directly; slow table fetch wrapped in Suspense — tradeoff based on **query speed**. Partially known Round 27
- **Debouncing**: Each keystroke **resets the timer** — fires after a pause (300ms) of no input, not a fixed delay from first keystroke. Partially known Round 27
- **Full search/pagination data flow**: User types → debounce → URL updates → server re-renders → SQL queries with params → components re-render
- **`'use server'` vs default server code**: Default server code runs during rendering. `'use server'` creates a **callable endpoint** that client components can invoke (via forms). Without it, client components can't trigger server functions. Missed Round 28
- **Server Actions vs server components**: Server components = reading/rendering, Server Actions = writing/mutating. Actions are the POST/PUT/DELETE handlers, components are the GET handlers. Form → Server Action directly, no API route middleman. Missed Round 28
- **`.bind(null, id)` pattern**: Pre-fills first argument into a Server Action when the data isn't in the form (e.g., ID from URL/props, not user input). `null` is for `this` context. Missed Round 28
- **Server-generated invoice date**: `new Date().toISOString().split('T')[0]` in the Server Action — not from form or page. Prevents backdating. Missed Round 28
- **Why forms are client components**: Need interactivity (inputs, selects, radio buttons respond to user events) — not about URL manipulation. The Server Action runs on server, but the form UI needs client-side interactivity. Missed Round 28
- **`.bind()` vs hidden form fields**: `.bind()` keeps ID out of DOM HTML (encrypted by Next.js), hidden fields are visible in source and editable via devtools. Partially known Round 28
- **Amount conversion two steps**: Zod `.coerce.number()` converts string → number, then `amount * 100` converts dollars → cents. Partially known Round 28
- **Server Actions eliminate two layers**: No API route definition and no client-side fetch needed — form `action` connects directly to server function. Express needs route + controller + client fetch; Next.js needs just the Server Action. Missed Round 29
- **Server-only execution = security**: SQL queries, database credentials, business logic never ship to browser bundle — client just submits data. Not just "reduces complexity." Missed Round 29
- **Client-side validation is bypassable**: Users can skip via devtools or raw requests — server-side validation (Zod in Server Action) is the security gate. Best practice is both: client for UX, server for security. Partially known Round 29
- **Amount stored in cents to avoid floating point errors**: Not just "simple conversion" — integers prevent precision bugs (e.g., `0.1 + 0.2 !== 0.3`). Partially known Round 29
- **`<form action>` = framework-managed pipeline**: Next.js handles submission, server invocation, error handling, revalidation as one system — with `onSubmit` + `fetch` you'd DIY all of that. Not just "less complexity." Partially known Round 29
- **Separating reads/writes into different files**: Separation of concerns (different triggers), reusability (multiple pages import same functions), security clarity (`'use server'` = callable from client, `data.ts` = rendering only). Partially known Round 29
- **Tendency to answer "reduces complexity"**: Name the *specific* benefit — security, reusability, framework integration, etc. "Reduces complexity" is usually true but rarely the full answer. Feedback from Round 29

### Needs revisiting (carried from React Foundations):
- Props object always `{}` not `undefined` — partially known Round 27 (knew it works, didn't know it's `{}`)
- Hooks call order (why no conditionals) — React tracks hooks by **call order**, conditionals could skip a hook and shift the order. Missed Round 27
- Reconciliation (virtual DOM diffing)
- State updates as const snapshots (not DOM reads)
- `useState()` with no arg = `undefined`

## Topics to cover in this project
- TypeScript basics (as encountered in the codebase)
- Tailwind CSS utility classes
- CSS Modules vs Tailwind
- Optimizing fonts and images (`next/font`, `next/image`)
- Nested layouts and pages (dashboard route group)
- Navigation with `<Link>` component and `usePathname`
- Database setup (postgres) and seeding
- Data fetching in server components (async components)
- Static vs dynamic rendering
- Streaming with `loading.js` and `<Suspense>`
- Search and pagination (URL search params)
- Server Actions for data mutations (forms)
- Error handling (`error.js`, `not-found.js`)
- Form validation with zod
- Authentication with next-auth
- Metadata API
