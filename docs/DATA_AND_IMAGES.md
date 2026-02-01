# Data & Images

## Mock Data

- **Products:** `src/lib/mockData.ts` — `MOCK_PRODUCTS` array. Each product has: id, name, slug, categoryId, description, price, salePrice, material, rating, SKU, status, **images**, variants.
- **Collections:** `src/lib/mockData.ts` — `MOCK_COLLECTIONS` array. Each collection has: id, name, slug, description, **image**, displayOrder.
- **Collection → Products:** `src/lib/mockData.ts` — `COLLECTION_PRODUCT_IDS`. Keys = collection slug; values = array of product IDs in that collection.
- **Orders (mock):** `src/lib/mockOrders.ts` — used for order history / order detail when no real backend.

API routes (`/api/products`, `/api/collections`, `/api/collections/[slug]`) read from these; no database required for current setup.

---

## Adding Product Images

1. **Put image files** in `public/`, e.g.:
   - `public/product-1.jpg`
   - `public/products/lawn-kurti-1.jpg`

2. **Update product in** `src/lib/mockData.ts` — in the product’s `images` array:
   ```ts
   images: [
     { url: "/product-1.jpg", altText: "Classic Cotton Tee", order: 0 },
     { url: "/products/lawn-kurti-1.jpg", altText: "Lawn Kurti back", order: 1 },
   ],
   ```
   - `url`: path from `public/` (must start with `/`).
   - `altText`: short description for accessibility.
   - `order`: display order (0, 1, 2…).

---

## Adding Collection Images

1. **Put image files** in `public/`, e.g.:
   - `public/collections/lawn.jpg`
   - `public/collection-cotton.jpg`

2. **Option A — Collections list & collection detail:**  
   In `src/lib/mockData.ts`, in `MOCK_COLLECTIONS`, set each collection’s `image`:
   ```ts
   { id: "col-lawn", name: "Lawn", slug: "lawn", ..., image: "/collections/lawn.jpg", displayOrder: 1 },
   ```

3. **Option B — Home “Featured Collections” only:**  
   In `src/app/(shop)/page.tsx`, update the `FEATURED_COLLECTIONS` array:
   ```ts
   const FEATURED_COLLECTIONS = [
     { slug: "lawn", name: "Lawn", description: "...", image: "/collections/lawn.jpg" },
     // ...
   ];
   ```
   Home page uses this; collections list/detail use `MOCK_COLLECTIONS` from API.

---

## Summary

| What | Where to add/change |
|------|----------------------|
| Product images | `src/lib/mockData.ts` → product `images[]`; files in `public/` |
| Collection image (list & detail) | `src/lib/mockData.ts` → `MOCK_COLLECTIONS[].image`; files in `public/` |
| Home featured collection images | `src/app/(shop)/page.tsx` → `FEATURED_COLLECTIONS[].image`; files in `public/` |
| Hero image | `src/app/(shop)/page.tsx` → `HERO_IMAGE`; file in `public/` (e.g. `/hero-banner.jpg`) |

All image paths are relative to `public/` and must start with `/`.
