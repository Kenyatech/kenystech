# KenyaTech.co.ke — Website Files

## 📁 Folder Structure

```
kenyatech/
├── index.html    ← Page structure and content (HTML)
├── style.css     ← All visual styling (colours, layout, typography)
├── script.js     ← All interactivity (products, cart, checkout, animations)
└── README.md     ← This file
```

> **How they connect:**
> `index.html` links to `style.css` via `<link>` in the `<head>`,
> and to `script.js` via `<script>` just before `</body>`.
> All three files must be in the **same folder** to work correctly.

---

## 🚀 Quick Start

Open `index.html` in any browser — no server required for local testing.

To go live, upload all three files to your hosting provider (e.g. Anything.com)
in the same folder. Keep the filenames exactly as-is.

---

## ✏️ Common Edits

### Change the brand name / logo
**File:** `index.html`
Find: `Kenya<span>Tech</span>`
The word before `<span>` is white; the word inside `<span>` is gold.
Change both to your brand name. There are 3 occurrences (nav, mobile menu, footer).

---

### Change brand colours
**File:** `style.css` → Section 1 (CSS Variables)

| Variable       | Used for                          |
|----------------|-----------------------------------|
| `--gold`       | Primary colour: buttons, prices   |
| `--gold-light` | Hover state of gold buttons       |
| `--black`      | Page background                   |
| `--text`       | Body text colour                  |
| `--green`      | Delivery / success messages       |

Example — change gold to a teal accent:
```css
--gold:       #0D9488;
--gold-light: #14B8A6;
--gold-dim:   #0F766E;
```

---

### Add a new product
**File:** `script.js` → Section 1 (Product Data)

Copy this template and paste it inside the `products` array:
```js
{
  id: 21,                         // Unique number — always increment
  name: "Your Product Name",
  category: "accessories",        // "accessories" or "electronics" only
  emoji: "🎯",                    // Placeholder — replace with real image later
  price: 1500,                    // Price in KES (no commas)
  original: 2000,                 // Crossed-out original price — or null
  badge: "new",                   // "new", "hot", "sale", or null
  desc: "Short product description here.",
  rating: 4.7
},
```

---

### Remove a product
**File:** `script.js` → Section 1 (Product Data)
Delete the entire object from `{` to `},` for that product.

---

### Use real product photos
**File:** `script.js` → `renderProducts()` function

1. Create an `images/` folder next to your HTML file.
2. Name your images by product ID: `1.jpg`, `2.jpg`, etc.
3. Find this line in `renderProducts()`:
   ```js
   ${p.emoji}
   ```
4. Replace it with:
   ```js
   <img src="images/${p.id}.jpg" alt="${p.name}" style="width:65%; height:65%; object-fit:contain;">
   ```

---

### Change the hero headline
**File:** `index.html` → Hero Section
```html
<h1>
  Accessories<br>
  <em>Worth Having.</em>   ← This line is italic and gold
</h1>
```
Edit the text between the tags. The `<em>` tag makes text italic + gold.

---

### Change hero stats (numbers on the right)
**File:** `index.html` → Hero Section → `.hero-stats`
```html
<div class="stat-num">500+</div>   ← Change the number
<div class="stat-label">Products</div>  ← Change the label
```

---

### Change the trust bar messages
**File:** `index.html` → Trust Bar section
Edit the text inside each `<span class="trust-item">` tag.
**Important:** Each item appears **twice** (the list is duplicated for the
seamless loop). Update both occurrences of each message.

---

### Update category product counts
**File:** `index.html` → Categories Section
```html
<div class="cat-count">// 12 Products Available</div>
```
Change the number to match your actual product count.

---

### Change bestseller products
**File:** `script.js` → `renderBestsellers()` function

Edit the `top` array. Each item references a position in the `products`
array (0 = first product). Use `products.find(p => p.id === X)` to pick
by product ID instead:
```js
const top = [
  products.find(p => p.id === 2),  // Featured: Pro Wireless Earbuds
  products.find(p => p.id === 1),  // #2
  products.find(p => p.id === 9),  // #3
  products.find(p => p.id === 15), // #4
  products.find(p => p.id === 4),  // #5
];
```

---

### Change free shipping threshold
**File:** `script.js` → `renderCheckout()` function
```js
// Free shipping over KES 2,000 — change threshold here
const shipping = subtotal >= 2000 ? 0 : 300;
```
Change `2000` to your threshold. Change `300` to your flat shipping fee.

---

### Update contact details (footer)
**File:** `index.html` → Footer section
```html
<li><a href="tel:+254700000000">+254 700 000 000</a></li>
<li><a href="mailto:hello@kenyatech.co.ke">hello@kenyatech.co.ke</a></li>
<li><a href="#">Westlands, Nairobi</a></li>
```

---

### Connect to n8n (send orders to your backend)
**File:** `script.js` → `placeOrder()` function

Find the `// ── TODO: Send order to backend/n8n here ──` comment and
add your webhook call:
```js
fetch('https://your-n8n-instance.com/webhook/order', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    name,
    phone,
    location,
    cart,
    paymentMethod: selectedPayment,
    total: cart.reduce((s, c) => s + c.price * c.qty, 0)
  })
});
```

---

### Add Meta Pixel tracking
**File:** `index.html` → inside `<head>`

Paste your Meta Pixel base code here, then add events in `script.js`:
- `ViewContent` — add inside `openProduct()`
- `AddToCart` — add inside `addToCart()`
- `InitiateCheckout` — add inside `openCheckout()`
- `Purchase` — add inside `placeOrder()` after validation passes

---

## 🎨 Fonts Used

| Font                | Role                      | Where to change            |
|---------------------|---------------------------|----------------------------|
| Cormorant Garamond  | Headings, prices, logo    | `style.css` → Section 1    |
| DM Sans             | Body text, buttons        | `style.css` → Section 1    |
| Space Mono          | Labels, tags, badges      | `style.css` → Section 1    |

To change fonts: update the Google Fonts URL in `index.html` `<head>`,
then update the `font-family` declarations in `style.css`.

---

## 📱 Responsive Breakpoints

| Breakpoint  | Behaviour                                          |
|-------------|----------------------------------------------------|
| > 1024px    | Full desktop layout (4-column grid, side stats)    |
| ≤ 1024px    | Tablet: 2-column grids, stacked bestsellers        |
| ≤ 768px     | Mobile: hamburger menu, single/2-col grids         |
| ≤ 480px     | Small mobile: fully single-column, stacked CTAs    |

---

## 🗂️ CSS File Sections (style.css)

Each section is clearly marked with a comment header. Use Ctrl+F to
jump to any section:

```
1.  CSS Variables          ← Edit colours here
2.  Reset & Base
3.  Custom Cursor          ← Disable custom cursor here
4.  Navigation Bar
5.  Mobile Menu
6.  Hero Section
7.  Trust Bar (Marquee)
8.  Shared Section Utilities
9.  Categories Section
10. Products Section
11. Product Cards
12. Product Modal
13. Checkout Panel
14. Cart & Order Success
15. Forms & Payment Options
16. Best Sellers Section
17. Why Us / About Section
18. Footer
19. Toast Notification
20. Scroll Reveal Animations
21. Keyframe Animations
22. Responsive — Tablet
23. Responsive — Mobile
24. Responsive — Small Mobile
```

---

## 🗂️ JS File Sections (script.js)

```
1.  Product Data           ← Add/remove products here
2.  State Variables
3.  renderProducts()
4.  renderBestsellers()    ← Change featured bestsellers here
5.  filterProducts()
6.  openProduct()
7.  closeModal()
8.  addToCart()
9.  removeFromCart()
10. updateCartCount()
11. toggleWishlist()
12. openCheckout()
13. closeCheckout()
14. renderCheckout()       ← Change shipping fee/threshold here
15. selectPayment()
16. placeOrder()           ← Connect to n8n webhook here
17. showToast()
18. Custom Cursor
19. Scroll Effects
20. Mobile Menu
21. Overlay Click to Close
22. Initialisation
```
