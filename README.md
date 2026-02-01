# NOOR-G E-Commerce

E-commerce frontend for **NOOR-G** — premium cotton & lawn fashion. Built with Next.js App Router, React Query, NextAuth, Tailwind CSS, and Zustand.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Setup & Installation](#setup--installation)
- [Environment Variables](#environment-variables)
- [Routes & Pages](#routes--pages)
- [State Management](#state-management)
- [API Routes](#api-routes)
- [Brand & Theming](#brand--theming)
- [Scripts](#scripts)
- [Documentation](#documentation)

---

## Features

### Shop
- **Home** — Hero, Featured Collections, Bestsellers, Testimonials, Newsletter
- **Shop** — Product grid with filters, sort, pagination, lazy loading
- **Collections** — Landing page + collection detail (Lawn, Cotton, Linen, Festive, Ready-to-Wear, New Arrivals) with sidebar filters
- **Product Detail** — Image gallery (zoom, lightbox), variants (size/color/quantity), add to cart/wishlist, accordions (description, material, shipping), reviews, related products
- **Search** — Full-screen search overlay, autocomplete (suggestions, recent, popular), results page with filters
- **Cart** — Item cards, quantity controls, order summary, promo code, checkout CTA
- **Checkout** — Multi-step flow: Auth → Shipping → Review → Confirmation; progress indicator, form validation
- **About** — Brand story, mission & values, fabric philosophy
- **Contact** — Contact form, FAQ accordion, contact info

### User
- **Account Dashboard** — Welcome, quick stats (orders, spent, wishlist, addresses), recent orders, quick actions
- **Orders** — List with filters/search, order detail with timeline, tracking, invoice
- **Addresses** — Saved addresses CRUD
- **Wishlist** — Saved products (Zustand + localStorage)

### Auth
- **NextAuth (Auth.js v5)** — Google OAuth; session used for account, orders, addresses
- **Guest checkout** — Checkout without account

### UI/UX
- **Responsive** — Breakpoints: mobile (&lt;768px), tablet (768–1023px), desktop (1024px+)
- **Mobile** — Bottom nav (&lt;768px), hamburger menu (slide-in from right, portal), full-screen search, touch-friendly tap targets
- **Accessibility** — Focus rings (gold), aria-labels, skip link, reduced-motion support
- **Animations** — Framer Motion: staggered entrances, slide/fade, ripple; CSS shimmer for skeletons

---

## Tech Stack

| Category        | Technology |
|----------------|------------|
| Framework      | Next.js 16 (App Router) |
| Language       | TypeScript |
| Styling        | Tailwind CSS |
| Data Fetching  | React Query (TanStack Query v3) |
| Auth           | NextAuth.js v5 (Auth.js) |
| State          | Zustand (cart, wishlist, user — with persist for cart/wishlist) |
| Forms          | React Hook Form + Zod |
| UI Primitives  | Radix UI (Accordion, Dialog, Dropdown, Select, Sheet) |
| Animation      | Framer Motion |
| Icons          | Lucide React |

---

## Project Structure

```
src/
├── app/
│   ├── (auth)/          # Login, error, loading
│   ├── (shop)/          # Home, shop, collections, products, cart, checkout, about, contact, search, wishlist
│   ├── (user)/          # Account dashboard, orders, addresses, wishlist (protected)
│   ├── api/             # Auth, products, collections, cart, orders, user
│   ├── layout.tsx       # Root layout
│   ├── robots.ts
│   └── sitemap.ts
├── components/
│   ├── cart/            # CartSummary
│   ├── layout/          # Header, Footer, Breadcrumb, Container, MobileMenu, BottomNav, SearchBar
│   ├── product/         # ProductCard, ProductGrid, CollectionFilters, ProductSort, ProductFilters
│   ├── shared/          # Providers, LoginForm, ResponsiveImage
│   ├── ui/              # Button, Input, Accordion, etc. (shadcn-style)
│   └── wishlist/        # WishlistSummary
├── hooks/               # useMediaQuery, etc.
├── lib/
│   ├── api/             # API client, products, cart, orders, user
│   ├── validations/     # Zod schemas
│   ├── constants.ts     # ROUTES, SITE_NAME, ORDER_STATUS, COLORS, etc.
│   ├── mockData.ts      # MOCK_PRODUCTS, MOCK_COLLECTIONS, COLLECTION_PRODUCT_IDS
│   ├── mockOrders.ts
│   ├── metadata.ts
│   ├── productFilters.ts
│   └── utils.ts
├── store/               # cartStore, wishlistStore, userStore (Zustand)
├── styles/
│   └── globals.css
└── types/
    └── index.ts         # Product, CartItem, User, etc.
```

---

## Setup & Installation

### Prerequisites

- Node.js 18+
- npm or yarn

### Steps

```bash
# Clone the repository
git clone <your-repo-url>
cd al_noor_fab

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env.local

# Edit .env.local (see Environment Variables)
# - AUTH_SECRET (run: npm run auth-secret)
# - AUTH_GOOGLE_ID, AUTH_GOOGLE_SECRET (Google OAuth)

# Run development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

### Build & Production

```bash
npm run build
npm start
```

---

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `AUTH_SECRET` | Secret for Auth.js (generate with `npm run auth-secret`) | Yes |
| `AUTH_GOOGLE_ID` | Google OAuth Client ID | For Google Sign In |
| `AUTH_GOOGLE_SECRET` | Google OAuth Client Secret | For Google Sign In |
| `NEXT_PUBLIC_SITE_URL` | Site URL (e.g. `https://yoursite.com`) | For sitemap/robots in production |

See `.env.example` for reference.

---

## Routes & Pages

| Route | Description |
|-------|-------------|
| `/` | Home — hero, featured collections, bestsellers, testimonials, newsletter |
| `/shop` | All products with filters & sort |
| `/collections` | Collections landing |
| `/collections/[slug]` | Collection detail (e.g. lawn, cotton) with filters |
| `/products/[slug]` | Product detail page |
| `/search` | Search results (query param `q`) |
| `/cart` | Shopping cart |
| `/checkout` | Multi-step checkout |
| `/wishlist` | Wishlist page |
| `/about` | About Us |
| `/contact` | Contact form & info |
| `/login` | Login (NextAuth) |
| `/account` | User dashboard (protected) |
| `/account/orders` | Order history |
| `/account/orders/[id]` | Order detail |
| `/account/addresses` | Saved addresses |
| `/account/wishlist` | Account wishlist |

Constants are in `src/lib/constants.ts` (`ROUTES`).

---

## State Management

- **Zustand**
  - `cartStore` — cart items (persisted to `localStorage` key `noor-g-cart`)
  - `wishlistStore` — product IDs (persisted to `noor-g-wishlist`)
  - `userStore` — user profile/addresses (key `noor-g-user`)
- **React Query** — products, collections, search, collection by slug (cached on client)
- **NextAuth** — session (useSession, signIn, signOut)

---

## API Routes

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/products` | List products (from mockData) |
| GET | `/api/collections` | List collections with product counts |
| GET | `/api/collections/[slug]` | Single collection with products |
| GET/POST | `/api/cart` | Cart CRUD |
| GET/PATCH/DELETE | `/api/cart/items/[itemId]` | Cart item by ID |
| GET/POST | `/api/orders` | Orders list / create |
| GET | `/api/orders/[id]` | Order by ID |
| GET/PATCH | `/api/user/profile` | User profile |
| GET/POST | `/api/user/addresses` | Addresses list / create |
| GET/PATCH/DELETE | `/api/user/addresses/[id]` | Address by ID |
| * | `/api/auth/[...nextauth]` | NextAuth handlers (session, signIn, etc.) |

Data source: `src/lib/mockData.ts` (MOCK_PRODUCTS, MOCK_COLLECTIONS, COLLECTION_PRODUCT_IDS) and mock orders.

---

## Brand & Theming

- **Primary dark:** `#333333`
- **Gold accent:** `#C4A747`
- **Cream:** `#F5F3EE`
- **Sage:** `#5BA383`

Defined in `src/lib/constants.ts` (COLORS) and `tailwind.config.ts` / `src/styles/globals.css`.

---

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start dev server (Turbopack) |
| `npm run build` | Production build |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run auth-secret` | Generate AUTH_SECRET for .env |

---

## Documentation

- **[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)** — App structure, data flow, auth
- **[docs/FEATURES.md](docs/FEATURES.md)** — Feature list and UX details
- **[docs/COMPONENTS.md](docs/COMPONENTS.md)** — Main components and usage
- **[docs/DATA_AND_IMAGES.md](docs/DATA_AND_IMAGES.md)** — Mock data, adding product/collection images

---

## License

Private. All rights reserved.
