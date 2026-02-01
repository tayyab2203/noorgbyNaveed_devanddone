# Architecture

## Overview

NOOR-G is a Next.js 16 App Router application with three main route groups: **(shop)**, **(auth)**, and **(user)**. Data is served via API routes backed by mock data; auth is handled by NextAuth (Auth.js v5).

---

## Route Groups

| Group | Path | Purpose |
|-------|------|---------|
| **(shop)** | `/`, `/shop`, `/collections`, `/products`, `/cart`, `/checkout`, `/about`, `/contact`, `/search`, `/wishlist` | Public storefront |
| **(auth)** | `/login`, error/loading | Login and auth UI |
| **(user)** | `/account/*` | Protected dashboard, orders, addresses, wishlist |

Layouts:
- Root: `app/layout.tsx` — Header, main, Footer, BottomNav, Providers
- Shop: `app/(shop)/layout.tsx` — Breadcrumb, Container
- User: `app/(user)/layout.tsx` — Sidebar (desktop) / tabs (mobile)

---

## Data Flow

1. **Products & Collections**
   - Source: `src/lib/mockData.ts` (MOCK_PRODUCTS, MOCK_COLLECTIONS, COLLECTION_PRODUCT_IDS)
   - API: `GET /api/products`, `GET /api/collections`, `GET /api/collections/[slug]`
   - Client: React Query (useQuery) with keys like `["products"]`, `["collections"]`, `["collection", slug]`

2. **Cart**
   - Client state: Zustand `cartStore` (persisted to `localStorage`, key `noor-g-cart`)
   - API: `/api/cart`, `/api/cart/items/[itemId]` (can sync with backend later)
   - Cart page and checkout read from store + API as needed

3. **Wishlist**
   - Client state: Zustand `wishlistStore` (persisted to `noor-g-wishlist`)
   - No dedicated API; product data from `/api/products` or collection APIs

4. **Orders**
   - Mock: `src/lib/mockOrders.ts`
   - API: `GET/POST /api/orders`, `GET /api/orders/[id]`
   - Checkout creates order via POST; user orders from GET

5. **User & Auth**
   - NextAuth session (useSession) for user identity
   - API: `/api/user/profile`, `/api/user/addresses`, `/api/user/addresses/[id]`
   - Auth provider wraps app in `Providers` (SessionProvider + QueryClient + SearchOpenContext + Toast)

---

## Auth

- **Provider:** NextAuth v5 (Auth.js) — `app/api/auth/[...nextauth]/route.ts`
- **Strategy:** Google OAuth (AUTH_GOOGLE_ID, AUTH_GOOGLE_SECRET)
- **Session:** JWT (default); `AUTH_SECRET` required
- **Usage:** `useSession()`, `signIn("google")`, `signOut()` from `next-auth/react`
- **Protected routes:** `/account/*` — check session in layout/page; redirect to login if needed
- **Guest checkout:** Checkout allows “Continue as Guest” without account

---

## State Summary

| State | Where | Persistence |
|-------|--------|-------------|
| Products / Collections | React Query | In-memory (cache) |
| Cart | Zustand cartStore | localStorage |
| Wishlist | Zustand wishlistStore | localStorage |
| User profile / Addresses | React Query + API | Server (mock API) |
| Session | NextAuth | Cookie |
| Search overlay open | React Context (SearchOpenContext) | No |
| Toast notifications | React Context (ToastProvider) | No |

---

## Key Files

- **Constants & routes:** `src/lib/constants.ts`
- **Mock data:** `src/lib/mockData.ts`, `src/lib/mockOrders.ts`
- **Types:** `src/types/index.ts`
- **Providers:** `src/components/shared/Providers.tsx`
- **Root layout:** `src/app/layout.tsx`
