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
- **Stage**: Chapter 7 — Fetching Data (completed)
- **Framework**: Next.js (latest), React (latest), TypeScript, Tailwind CSS
- **New for this project**: TypeScript (`.tsx` files), Tailwind CSS, postgres, bcrypt, next-auth, zod
- **Deployment**: Vercel (auto-deploys from GitHub `main` branch), Postgres database hosted in cloud (Neon/Supabase via Vercel)
- **What exists**: Landing page, root layout with Inter font, dashboard layout with SideNav, dashboard page with live data (revenue chart, latest invoices, summary cards), two placeholder pages (invoices, customers), pre-built UI components in `app/ui/`, data layer in `app/lib/`, seeded database with all four tables populated
- **Routes**: `/` (landing), `/dashboard`, `/dashboard/invoices`, `/dashboard/customers`
- **Pre-built UI components**: Dashboard (sidenav, nav-links, revenue-chart, cards, latest-invoices), Invoices (table, create/edit forms, pagination, buttons, breadcrumbs, status), Customers (table), search, skeletons, login-form, button, acme-logo

## Quiz progress
- 240 questions across 24 rounds (130 from React Foundations + 110 in this project)
- Score trend: 5.5 -> 5 -> 5.5 -> 7 -> 6.5 -> 6 -> 5.5 -> 8 -> 6 -> 5.5 -> 7 -> 6 -> 7.5 -> 4.5 -> 6.5 -> 6 -> 6.5 -> 7.5 -> 9 -> 7.5 -> 7.5 -> 9.5 -> 5 -> 6
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

### Topics now understood (from Rounds 14-24):
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

### Topics that need revisiting (from Rounds 14-23):
- **TypeScript `!` (non-null assertion)**: Tells TS "trust me, this won't be null" — compile-time only, no runtime effect
- **TypeScript union types**: `'pending' | 'paid'` restricts to specific values — TS feature, not Next.js
- **Tagged template literals**: `sql\`...\`` calls `sql` as a function with template parts — not just regular template literals
- **Skeletons = loading placeholders**: Show page structure during data fetch for perceived performance, not for showcasing capabilities
- **`ILIKE` vs `LIKE`**: `ILIKE` is case-insensitive (PostgreSQL-specific)
- **Raw SQL vs ORM disadvantage**: Portability and maintenance, not manual sanitization — tagged template literals auto-parameterize
- **Seed route using GET is a shortcut**: Writing data should be POST; tutorial uses GET for browser convenience
- **bcrypt salt rounds**: The `10` = cost factor (2^10 iterations), not password length
- **Search/pagination state in URL params**: Not React state — URL is bookmarkable, shareable, survives refresh, server-readable
- **Nested layouts**: Dashboard layout nests *inside* root layout (not extends) — layouts stack like nesting dolls
- **Middleware for auth**: `middleware.ts` at project root intercepts every request — not per-page checks (like Express `app.use(authCheck)`)
- **`Omit<Type, 'field'>` utility**: TypeScript built-in — copies a type minus specified fields
- **Dynamic nav links in database**: For permission-based navigation (different users see different links), not for displaying data on hover
- **Server sets invoice date**: Server Action generates the date, not user input — prevents backdating
- **`<Image>` benefits too vague**: Need to name specific features (optimization, lazy loading, layout shift prevention) not just "extra features"
- **Server components fetch data directly**: Understood in discussion but missed on quiz — the component itself is async and calls data functions, no route handler middleman
- **`async` on server components**: Needed so the function can use `await` for data fetching — only server components can be async (client components must stay responsive for re-renders)
- **Promises fire immediately**: `sql\`...\`` sends the query and returns a promise right away — `Promise.all` doesn't start them, it waits for them to finish
- **`Promise.all` as checkpoint**: Waits for all promises to resolve before continuing — doesn't cause parallelism, just collects results
- **TypeScript generics (`sql<Revenue[]>`)**: Type hint telling TS what shape the returned data will be — no runtime effect, just compile-time checking
- **TypeScript prop typing**: `{ revenue }: { revenue: Revenue[] }` — left side destructures props, right side declares their types
- **Waterfall blocks entire page**: Sequential `await`s in page component mean nothing renders until all data is ready — user sees blank page
- **Client components can't be async**: They need to return JSX immediately for re-renders and interactivity — `async` would pause the function, blocking the UI. Server components run once and are done, so pausing is fine
- **`Promise.all` fails fast**: Rejects immediately if any promise fails, but successful queries already ran and their effects stay. `sql.begin` rolls back all queries if any fail — true "all or nothing"
- **TypeScript generics get stripped**: `sql<Revenue[]>` is erased entirely at compile time — the compiled JS has no angle brackets, just `sql\`...\``
- **Page fetching for children is a weakness**: Consolidating all fetches in the page creates waterfall — better pattern is each component fetching its own data (Suspense)

### Needs revisiting (carried from React Foundations):
- Duplicate keys (rendering bugs vs errors)
- Expressions vs statements in JSX
- Unused props silently ignored
- Props object always `{}` not `undefined`
- Hooks call order (why no conditionals)
- Lifting state up (pass setter as prop not import)
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
