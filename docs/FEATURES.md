# Features

## Shop

### Home (`/`)
- **Hero** — Full-bleed image (`/hero-banner.jpg`), headline, CTA (Shop Now, Explore Collections)
- **Featured Collections** — Grid of collection cards (Lawn, Cotton, Linen, Festive, Ready-to-Wear) with image, name, description, “View Collection” link
- **Bestsellers** — First 4 products from API, ProductCard grid, “View All” to `/shop`
- **Testimonials** — Carousel (mobile 1, tablet 2, desktop 3), auto-rotate
- **Newsletter** — Email signup (dark section), form with validation

### Shop (`/shop`)
- Product grid (ProductGrid) with filters (ProductFilters) and sort (ProductSort)
- Lazy loading, loading skeletons, empty state with “Clear Filters”
- Responsive columns (e.g. 4 → 3 → 2 by breakpoint)

### Collections
- **Landing (`/collections`)** — Hero “Our Collections”, grid of all collections (from API), optional featured banner after 6th
- **Detail (`/collections/[slug]`)** — Header (name, description, count), sidebar filters (CollectionFilters), toolbar (sort, view), ProductGrid, pagination/infinite scroll

### Product Detail (`/products/[slug]`)
- **Gallery** — Main image (zoom on hover), thumbnails, image counter, lightbox on click
- **Info** — Breadcrumb, title, rating/reviews, price (sale/original), SKU/material/availability, size/color/quantity selectors, Add to Cart, Add to Wishlist
- **Accordions** — Description, Material & Care, Shipping & Returns
- **Trust badges** — Authentic, Secure Checkout, Support
- **Reviews** — Summary, distribution, review cards
- **Related** — “You May Also Like” carousel

### Search
- **SearchBar (Header)** — Desktop: pill input with dropdown (suggestions, recent, popular, “View all results”). Mobile: full-screen overlay
- **Search page (`/search?q=...`)** — Same filters/grid as collection, relevance sort, suggested/recent/popular if no results

### Cart (`/cart`)
- Two-column (desktop): cart items (65%) + sticky order summary (35%)
- Item card: image, name, variant, price, quantity controls, line total, remove (with confirm)
- Summary: subtotal, shipping, discount, total, promo code, Secure Checkout button, trust badges
- Empty state: illustration, “Start Shopping”
- Mobile: summary on top, then items; fixed bottom bar with total + Checkout

### Checkout (`/checkout`)
- **Steps:** 1) Auth (Sign in / Guest), 2) Shipping (form + saved addresses), 3) Review (edit links, terms checkbox), 4) Confirmation (order number, delivery, actions)
- Progress indicator at top
- Order summary sidebar (desktop) or collapsible (mobile)
- Form validation (React Hook Form + Zod)

### Static
- **About (`/about`)** — Story, mission & values, fabric philosophy, team quote
- **Contact (`/contact`)** — Form, contact info, FAQ accordion

### Wishlist (`/wishlist`)
- Grid of ProductCards for wishlist IDs (from wishlistStore), empty state

---

## User (Account)

- **Dashboard (`/account`)** — Welcome, quick stats (orders, spent, wishlist, addresses), recent orders, quick actions (profile, addresses, wishlist)
- **Orders (`/account/orders`)** — List with filters/search, cards with thumbnails, status, View/Track/Reorder
- **Order Detail (`/account/orders/[id]`)** — Timeline, shipping info, items, invoice/support/cancel
- **Addresses (`/account/addresses`)** — CRUD saved addresses
- **Wishlist (`/account/wishlist`)** — Same as shop wishlist page, under account

Layout: desktop sidebar (Dashboard, Orders, Addresses, Wishlist, Settings, Logout); tablet collapsed sidebar; mobile top tabs.

---

## Auth

- **Login (`/login`)** — NextAuth sign-in (e.g. Google); redirect after login
- **Session** — Used in Header (user menu), MobileMenu, BottomNav, account routes, checkout (optional sign-in)
- **Guest** — Checkout and shop work without account

---

## UI/UX

- **Responsive** — Mobile-first; breakpoints 640, 768, 1024, 1280
- **Mobile** — Bottom nav (&lt;768px), hamburger menu (portal, slide from right), full-screen search, touch targets ≥44px
- **Accessibility** — Skip link, focus ring (gold), aria-labels, reduced-motion
- **Animations** — Framer Motion (stagger, slide, fade); CSS shimmer for skeletons; ripple-style feedback
- **Breadcrumbs** — Global in shop layout; no duplicate on contact/collection pages
- **Toast** — ToastProvider for success/error messages (e.g. add to cart, checkout)

---

## Images & Content

- **Product images** — In `src/lib/mockData.ts` per product `images[]`; place files in `public/`, use path like `/product-1.jpg`
- **Collection images** — In `mockData` for each collection (`image`); home Featured Collections use same or override in `app/(shop)/page.tsx` (FEATURED_COLLECTIONS)
- **Hero** — `HERO_IMAGE` in home page (e.g. `/hero-banner.jpg` in `public/`)
