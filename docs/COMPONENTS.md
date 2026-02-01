# Components

## Layout

| Component | Path | Description |
|-----------|------|-------------|
| **Header** | `components/layout/Header.tsx` | Sticky header: logo, desktop nav, Search/Wishlist/Cart/User; mobile hamburger (MobileMenu) |
| **Footer** | `components/layout/Footer.tsx` | Links, contact, social, copyright |
| **Container** | `components/layout/Container.tsx` | Max-width wrapper, optional padding |
| **Breadcrumb** | `components/layout/Breadcrumb.tsx` | Auto breadcrumb from pathname (used in shop layout) |
| **MobileMenu** | `components/layout/MobileMenu.tsx` | Hamburger menu: portal to body, backdrop, slide-in panel; profile, nav links, Collections submenu, secondary links, social, Sign In/Out |
| **BottomNav** | `components/layout/BottomNav.tsx` | Fixed bottom bar (&lt;768px): Home, Collections, Search, Wishlist, Account |
| **SearchBar** | `components/layout/SearchBar.tsx` | Search input + dropdown (suggestions, recent, popular); full-screen on mobile; uses SearchOpenContext |

---

## Product

| Component | Path | Description |
|-----------|------|-------------|
| **ProductCard** | `components/product/ProductCard.tsx` | Card: image, badges (NEW/SALE), wishlist, quick actions, name, rating, price; responsive; `highlightTerm` for search |
| **ProductGrid** | `components/product/ProductGrid.tsx` | Grid of ProductCards; loading skeletons, empty state, lazy load (Intersection Observer), stagger animation |
| **CollectionFilters** | `components/product/CollectionFilters.tsx` | Sidebar filters: price, size, color, material, rating, availability; Apply/Reset |
| **CollectionFiltersTrigger** | (same file) | Mobile/tablet “Filters” button + sheet/drawer |
| **CollectionToolbar** | (same file) | Sort dropdown + grid/list view toggle |
| **ProductSort** | `components/product/ProductSort.tsx` | Sort options (e.g. Best Selling, Price, Newest) |
| **ProductFilters** | `components/product/ProductFilters.tsx` | Legacy/shared filter state types (DEFAULT_FILTERS, ProductFiltersState) |

---

## Cart & Wishlist

| Component | Path | Description |
|-----------|------|-------------|
| **CartSummary** | `components/cart/CartSummary.tsx` | Order summary block (subtotal, shipping, total, promo) |
| **WishlistSummary** | `components/wishlist/WishlistSummary.tsx` | Wishlist count/summary for header/sidebar |

Cart page and checkout use inline sections (not always these components); cart state from cartStore.

---

## Shared

| Component | Path | Description |
|-----------|------|-------------|
| **Providers** | `components/shared/Providers.tsx` | SessionProvider, QueryClientProvider, SearchOpenContext, ToastProvider |
| **LoginForm** | `components/shared/LoginForm.tsx` | Email/password or social login form |
| **ResponsiveImage** | `components/shared/ResponsiveImage.tsx` | Wrapper around next/image with sizes/priority |

---

## UI (shadcn-style)

In `components/ui/`: **button**, **input**, **card**, **accordion**, **dropdown-menu**, **select**, **sheet**, **skeleton**, **toast**. Used across shop, checkout, account, and modals.

---

## Usage Notes

- **ProductCard** — Receives `product` and optional `highlightTerm`; wishlist state from wishlistStore; client-only wishlist icon to avoid hydration mismatch.
- **ProductGrid** — Receives `products`, `loading`, optional `highlightTerm`; handles empty and loading.
- **MobileMenu** — Rendered inside Header; menu panel portaled to `document.body` so it overlays full viewport; body scroll locked when open.
- **SearchBar** — Open state from `useSearchOpen()`; BottomNav “Search” triggers same open.
- **Breadcrumb** — Rendered once in `(shop)/layout.tsx`; do not add a second Breadcrumb on contact or collection detail pages.
