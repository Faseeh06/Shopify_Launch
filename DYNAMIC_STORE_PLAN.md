# Comprehensive Plan for a "Fully Dynamic" Shopify Store

Making a Shopify store "Fully Dynamic" means minimizing hardcoded content and maximizing the ability to control layout, content, and functionality directly from the Shopify Admin (Theme Editor) and Data Sources (Metafields).

## Phase 1: Architecture & Data Structure (The "Brain")
This phase ensures that unique data can be stored for products/collections without creating specific templates for each one.

### 1.1 Metafield Strategy
Instead of generic descriptions, we will define structured data points for Products and Collections.
*   **Products**:
    *   `custom.ingredients` (Multi-line text or Reference)
    *   `custom.how_to_use` (Rich text)
    *   `custom.video_highlight` (File/Video)
    *   `custom.pairs_well_with` (Product List Reference - useful for cross-selling)
    *   `custom.feature_badges` (List of images/icons)
*   **Collections**:
    *   `custom.banner_image` (Image file - different from the main collection image)
    *   `custom.promo_text` (Single line text for specific announcements)

### 1.2 Dynamic Sources
Update all `{% schema %}` in sections to support "Dynamic Sources". This allows you to click a "Connect dynamic source" button in the editor to bind a setting (like an Image) to a Metafield instead of selecting a static image.

## Phase 2: Section Modularity (The "Body")
Ensure that every part of the site is built as a reusable, drag-and-drop section.

### 2.1 "Everywhere" Sections
Ensure high-value sections are available on **all** templates, not just the Homepage.
*   **Hero Banners**: Should be usable on Collection pages (displaying collection meta-fields) or Product pages.
*   **Testimonials / Trusted Stories**: Make this a reusable section that can filter reviews based on the current product using tags or metafields.
*   **FAQ Section**: A block-based accordion that can either show static FAQs or pull from a `product.metafields.custom.faqs`.

### 2.2 Intelligent Components
*   **Header/Mega Menu**:
    *   Build a Mega Menu that renders sub-collections and promotional images dynamically based on the Menu structure in Navigation settings.
*   **Product Card**:
    *   Show "New", "Sale", or "Best Seller" badges automatically based on inventory age, price comparison, or tags.
    *   Add a "Quick Add" button that opens a drawer or modal.

## Phase 3: Interactivity & User Experience (The "Behavior")
Make the site feel "app-like" with seamless interactions.

### 3.1 AJAX & State Management
*   **Cart Drawer**: Implement a slide-out cart that updates immediately when an item is added, without refreshing the page.
*   **Variant Switching**: When a user clicks a color swatch, the main image gallery should smoothly slide/fade to the relevant images for that variant (filtering the media gallery).

### 3.2 Dynamic Recommendations
*   **"You May Also Like"**: Use the Shopify Recommendations API (JavaScript) to fetch related products client-side on Product and Cart pages.
*   **Recently Viewed**: Store viewed product IDs in local storage and fetch their data to display a "Recently Viewed" bar.

### 3.3 Enhanced Filtering
*   Implement **Faceted Search** on Collection pages. Allow users to filter by Price, Availability, and Custom Metafields (e.g., "Skin Type", "Concern") dynamically.

## Phase 4: Implementation Roadmap

| Step | Action Item | Technical Task |
| :--- | :--- | :--- |
| **1** | **Audit Schemas** | Review `schema` in top 5 sections. Enable `dynamic` support. |
| **2** | **Define Metafields** | Create definitions in *Settings > Custom Data*. |
| **3** | **Product Page 2.0** | Rebuild `main-product.liquid` to use blocks for *every* element (Title, Price, Buy Buttons, Accordions). |
| **4** | **Cart Drawer** | Build/Refine `cart-drawer.liquid` for real-time updates. |
| **5** | **Collection Filtering**| Implement `facets.liquid` using the new Storefront Filtering system. |

## Immediate Next Steps for Us
1.  **Select a Pilot Page**: recommending the **Product Page**. We can make the "Description", "Ingredients", and "How to Use" tabs fully dynamic using metafields.
2.  **Define the Data**: What specific attributes do your products have? (e.g., Skin Type, Ingredients).
3.  **Execute**: I will code the schema changes and liquid logic to connect them.
