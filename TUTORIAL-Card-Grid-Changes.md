# Step-by-Step Tutorial: Card Grid Layout Changes

This tutorial shows exactly what was changed to make the service cards display in a responsive grid.

---

## Overview of Changes

**Goal:** Make 4 service cards display as:
- **Mobile (phones):** 1 card per row (stacked)
- **Tablet/iPad Pro:** 2×2 grid (2 cards per row)
- **Desktop:** 1 row of 4 cards

**Files Modified:**
1. `index.html` - Fixed Bootstrap grid structure
2. `assets/css/styles.css` - Updated card styling

---

## Step 1: Fix HTML Structure (index.html)

### ❌ BEFORE (Incorrect Structure)

The cards had broken grid structure with misplaced divs and wrong Bootstrap classes:

```html
<div class="container">
    <div class="row-cols-sm-1 col d-flex row-cols-sm-2 row-cols-md-4 flex-lg-row-4 g-4 justify-content-center align-items-center">
        <div class="card">
            <img src="assets\images\horse-jumping-4372601.jpg" class="card-img-top img-fluid" alt="...">
            <div class="card-body">
                <h5 class="card-title">Lunge</h5>
                <p class="card-text">...</p>
            </div>
        </div>
    </div>
    <div class="col">
        <div class="card">
            <img src="assets\images\pexels-3842988-10889614.webp" class="card-img-top img-fluid" alt="...">
            <div class="card-body">
                <h5 class="card-title">Group Lessons</h5>
                <p class="card-text">...</p>
            </div>
        </div>
    </div>
    <!-- More cards with same broken structure... -->
</div>
```

**Problems:**
- ❌ First card wrapped in a `<div>` with mixed row/col classes
- ❌ Other cards each in separate `<div class="col">` without parent row
- ❌ Cards not siblings in the same row
- ❌ Classes like `flex-lg-row-4` don't exist in Bootstrap

---

### ✅ AFTER (Correct Structure)

All cards wrapped in a single row with proper column wrappers:

```html
<div class="container">
    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4 g-4">
        <div class="col">
            <div class="card h-100">
                <img src="assets\images\horse-jumping-4372601.jpg" class="card-img-top" alt="Lunge Training">
                <div class="card-body d-flex flex-column">
                    <h5 class="card-title">Lunge</h5>
                    <p class="card-text">...</p>
                </div>
            </div>
        </div>
        <div class="col">
            <div class="card h-100">
                <img src="assets\images\pexels-3842988-10889614.webp" class="card-img-top" alt="Group Lessons">
                <div class="card-body d-flex flex-column">
                    <h5 class="card-title">Group Lessons</h5>
                    <p class="card-text">...</p>
                </div>
            </div>
        </div>
        <div class="col">
            <div class="card h-100">
                <img src="assets\images\pexels-elisabeth-husebo-163886054-10865190.jpg" class="card-img-top" alt="Forest Hacks">
                <div class="card-body d-flex flex-column">
                    <h5 class="card-title">Forest Hacks</h5>
                    <p class="card-text">...</p>
                </div>
            </div>
        </div>
        <div class="col">
            <div class="card h-100">
                <img src="assets\images\pexels-alexander-dummer-37646-1364073.jpg" class="card-img-top" alt="Pony Rides">
                <div class="card-body d-flex flex-column">
                    <h5 class="card-title">Pony Rides</h5>
                    <p class="card-text">...</p>
                </div>
            </div>
        </div>
    </div>
</div>
```

**What Changed:**

| Element | Before | After | Why |
|---------|--------|-------|-----|
| **Parent Row** | Mixed classes on wrong element | `row row-cols-1 row-cols-md-2 row-cols-lg-4 g-4` | Bootstrap responsive grid classes |
| **Column Wrappers** | Inconsistent/missing | Each card in `<div class="col">` | Proper Bootstrap grid structure |
| **Card Element** | Just `class="card"` | `class="card h-100"` | `h-100` makes all cards equal height |
| **Card Body** | Just `class="card-body"` | `class="card-body d-flex flex-column"` | Flexbox stretches content evenly |
| **Images** | `class="card-img-top img-fluid"` | `class="card-img-top"` | Removed redundant `img-fluid` |
| **Alt Text** | Generic `"..."` | Descriptive text | Accessibility improvement |

---

## Step 2: Understanding Bootstrap Grid Classes

### `row row-cols-1 row-cols-md-2 row-cols-lg-4 g-4`

Let's break down each class:

| Class | Breakpoint | Effect |
|-------|------------|--------|
| `row` | Always | Creates a flexbox row container |
| `row-cols-1` | Default (mobile) | 1 column = 1 card per row |
| `row-cols-md-2` | ≥768px (tablets) | 2 columns = 2 cards per row (2×2 grid) |
| `row-cols-lg-4` | ≥992px (desktop) | 4 columns = 4 cards per row (1 row) |
| `g-4` | Always | Gap/gutter size 4 (1.5rem spacing) |

**Visual Representation:**

```
Mobile (<768px):
┌─────────────┐
│   Card 1    │
├─────────────┤
│   Card 2    │
├─────────────┤
│   Card 3    │
├─────────────┤
│   Card 4    │
└─────────────┘

Tablet (768-991px):
┌──────────┬──────────┐
│  Card 1  │  Card 2  │
├──────────┼──────────┤
│  Card 3  │  Card 4  │
└──────────┴──────────┘

Desktop (≥992px):
┌──────┬──────┬──────┬──────┐
│Card 1│Card 2│Card 3│Card 4│
└──────┴──────┴──────┴──────┘
```

---

## Step 3: Update CSS Styling (assets/css/styles.css)

### ❌ BEFORE (Old Card Styles)

```css
.card{
  width: 18rem;
  margin: 2rem auto;
  display: flex;
}
.card-img-top{
  height: 200px;
  object-fit: cover;
}
```

**Problems:**
- ❌ Fixed width `18rem` conflicts with Bootstrap grid
- ❌ `margin: 2rem auto` centers cards individually (not needed in grid)
- ❌ No styles for equal heights
- ❌ No hover effects
- ❌ Small image height

---

### ✅ AFTER (New Card Styles)

```css
/* Card styles for service cards */
.card{
  display: flex;
  flex-direction: column;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.2s;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}

.card-img-top{
  height: 250px;
  object-fit: cover;
  width: 100%;
}

.card-body {
  flex: 1;
}

/* Responsive card image heights */
@media (max-width: 768px) {
  .card-img-top {
    height: 200px;
  }
}
```

**What Each Property Does:**

| Property | Value | Purpose |
|----------|-------|---------|
| `display: flex` | - | Makes card a flex container |
| `flex-direction: column` | - | Stacks image/body vertically |
| `border-radius: 8px` | - | Rounded corners |
| `overflow: hidden` | - | Keeps image within rounded corners |
| `box-shadow` | `0 2px 8px rgba(0,0,0,0.1)` | Subtle shadow for depth |
| `transition` | `transform 0.2s` | Smooth hover animation |
| **On hover:** |
| `transform: translateY(-4px)` | - | Lifts card up 4px |
| `box-shadow` | `0 4px 12px rgba(0,0,0,0.15)` | Stronger shadow on hover |
| **Image:** |
| `height: 250px` | Desktop | Taller images on large screens |
| `height: 200px` | Mobile | Shorter images on small screens |
| `object-fit: cover` | - | Crops image to fill area |
| **Card Body:** |
| `flex: 1` | - | Stretches to fill remaining space |

---

## Step 4: How Equal Heights Work

### The Magic Combination

Three elements work together:

1. **HTML:** `<div class="card h-100">` 
   - `h-100` = Bootstrap class for `height: 100%`
   - Makes card fill its column's height

2. **CSS:** `.card { display: flex; flex-direction: column; }`
   - Card becomes a vertical flexbox
   - Image and body stack vertically

3. **CSS:** `.card-body { flex: 1; }`
   - Body stretches to fill remaining space
   - Pushes content evenly

**Visual Example:**

```
Without equal heights:
┌──────────┬──────────┐
│  Image   │  Image   │
├──────────┼──────────┤
│ Title    │ Title    │
│ Text     │ Text     │
│          │ Text     │
└──────────┤ Text     │
           │ Text     │
           └──────────┘  ← Uneven bottom edges

With equal heights:
┌──────────┬──────────┐
│  Image   │  Image   │
├──────────┼──────────┤
│ Title    │ Title    │
│ Text     │ Text     │
│          │ Text     │
│          │ Text     │
│          │ Text     │
└──────────┴──────────┘  ← Aligned bottom edges
```

---

## Step 5: Testing Your Changes

### Open in Browser

**PowerShell command:**
```powershell
Start-Process 'c:\Users\griff\Documents\vscode-projects\horse-riding-club\index.html'
```

### Test Responsiveness

1. **Desktop View (≥992px):**
   - Resize browser to full screen
   - ✅ Should see 4 cards in a single row
   - ✅ All cards same height
   - ✅ Hover effect lifts cards

2. **Tablet View (768-991px):**
   - Resize browser to ~800px width
   - ✅ Should see 2×2 grid (2 cards per row)
   - ✅ Cards in same row have equal height

3. **Mobile View (<768px):**
   - Resize browser to ~400px width
   - ✅ Should see 1 card per row (stacked)
   - ✅ Cards fill screen width

### Browser DevTools Method

1. Press `F12` to open DevTools
2. Click device icon (or press `Ctrl+Shift+M`)
3. Select different devices:
   - iPhone 12/13 (390px) → 1 column
   - iPad (768px) → 2 columns
   - Desktop (1920px) → 4 columns

---

## Summary of Changes

### ✅ What Works Now

- ✅ Proper Bootstrap 5 grid structure
- ✅ Responsive layout (1/2/4 columns)
- ✅ Equal-height cards in each row
- ✅ Hover effects for interactivity
- ✅ Consistent spacing with `g-4` gutters
- ✅ Proper image sizing (responsive heights)
- ✅ Accessible alt text on images

### 🎯 Key Takeaways

1. **Bootstrap Grid Structure:**
   ```html
   <div class="container">
     <div class="row row-cols-{breakpoint}-{columns}">
       <div class="col">
         <div class="card">...</div>
       </div>
     </div>
   </div>
   ```

2. **Equal Heights:** Use `h-100` on cards + `flex: 1` on card-body

3. **Responsive Breakpoints:**
   - No prefix = mobile (all sizes)
   - `-md-` = ≥768px (tablet)
   - `-lg-` = ≥992px (desktop)

---

## Need More Help?

- **Bootstrap 5 Grid Docs:** https://getbootstrap.com/docs/5.3/layout/grid/
- **Bootstrap 5 Cards:** https://getbootstrap.com/docs/5.3/components/card/
- **Flexbox Guide:** https://css-tricks.com/snippets/css/a-guide-to-flexbox/

---

*Tutorial created: December 7, 2025*
