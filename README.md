# Riceline — Online Menu & Order Page

**How the site works:** customers land on the **text menu** (`index.html`). Every dish name and **Order →** link opens that dish on the ordering page (`order.html`), ready for "Add to bag". The **Order online** buttons (top bar, under the title, and the floating button on phones) open the ordering page. On the ordering page, **Full menu ↗** goes back.

This folder is a static website for GitHub Pages. It needs no server, database or build step.
Everything runs in the visitor's browser.

## 1. Put it on GitHub Pages (about 5 minutes)

1. Go to github.com and click **New repository**. A name such as `riceline` works. Set it to **Public** and click **Create**.
2. On the new repo page, click **uploading an existing file**.
3. Drag **everything inside this folder** (not the folder itself) into the upload box. That includes the hidden `.nojekyll` file.
4. Click **Commit changes**.
5. Go to **Settings → Pages**. Under *Build and deployment*, choose **Deploy from a branch**, then **main** and **/ (root)**, and click **Save**.
6. After 1–2 minutes the site is live at `https://<your-username>.github.io/riceline/`. The text menu is the homepage, and ordering is at `/riceline/order.html`.

To use your own domain (for example riceline.com), go to Settings → Pages → *Custom domain* and follow GitHub's steps.

## 2. Things you MUST change before going live

All of these are in **`config.js`**. Open it on GitHub, click the pencil (Edit), change the values, then click Commit.

| Setting | Now | What to do |
|---|---|---|
| `address`, `mapsQuery` | "Huntington Ave, Boston 02115" (placeholder) | Your real street address |
| `phone` | (617) 555-0142 (**fictional** 555 number) | Your real phone |
| `email` | orders@example.com | Your real email |
| `hours` | Mon–Fri 10:30–21:00, Sat 11–21, Sun 11–20 | Your real hours (24-hour format) |
| `orderMode` | `"demo"` (orders are **not** sent anywhere) | See below |

### How orders get to you (`orderMode`)
- **`"demo"`**: the customer sees a confirmation screen, but nothing is sent. Use this only for testing.
- **`"link"`**: copies the order text and opens your online-ordering page. Put your Toast, Square or Clover link in `orderLink`. *Recommended. It takes real payment.*
- **`"sms"`**: opens the customer's text app with the order addressed to `smsNumber`.
- **`"email"`**: opens the customer's email app with the order addressed to `email`.

## 3. Change prices, names, descriptions

Open **`data/menu.js`** and search for the item name. Change `"price": 11.5` to the new price. For build-your-own, the price set by each protein is `"bowlPrice"`. Keep the quotes and commas as they are.

Things that were proposed (not from your menu photo) and should be checked:
- Add-ons: avocado $2.00, egg $1.50, extra rice $1.50, sauce cup $0.75, consommé $1.50, double chicken $3.50, double beef $5.95, **double tofu $2.50 (new)**
- Drinks: iced tea $2.75, can soda $2.50, water $1.75, Vietnamese iced coffee $4.95
- **Sesame Garlic Tofu Bowl $9.00**: a new plant-based bowl. It is built from the tofu that is already in the Google Sheet. It is not in the 10 signature rows there yet.

## 4. Two looks: photos or illustrations

- **`order.html`**: ordering page with photos (Unsplash photos). The "Order online" buttons point here.
- **`order-illustrated.html`**: the same ordering page, but with flat illustrations of each bowl drawn for Riceline (in `assets/illus/`, SVG). Each bowl drawing is built from that bowl's real recipe: base, protein, veggie, toppings, sauce and finish.

To use the illustrated ordering page instead, rename `order.html` to `order-photos.html`, then rename `order-illustrated.html` to `order.html`.
Or, in `config.js`, add the line `imageStyle: "illustration",` to switch the photo version to illustrations as well.

**`index.html`** (the homepage) is the text menu: everything on one page with prices, calories and allergens, the hours and address, and a Print button. Its prices are written into the page. If you change a price in `data/menu.js`, also change it in `index.html`, or ask Claude to rebuild it.

## 5. Replace the photos with your own

The photos are free Unsplash photos that **illustrate similar dishes**. They are not your food. Credits are in `credits.html`.
Once you have real photos, replace them in `assets/img/` and **keep the same file names**:
- `<name>-560.webp`: 560×420 px (menu cards)
- `<name>-1000.webp`: 1000×750 px (item detail)
- `hero-900.webp` / `hero-1600.webp`: top banner

Any converter that outputs WebP works, for example squoosh.app. Once all photos are yours, you can delete `credits.html` and the "Photo credits" link in `index.html`.

## 6. Calories & allergens

- Calories, protein, carbs and fat are **calculated estimates**. They come from the recipes in the "Bowl Line Playbook" Google Sheet multiplied by USDA reference values, with cooking yields that are still estimates. Re-check them after your yield tests.
- Allergens come from each recipe's ingredients. **Check the actual labels you buy**, especially the tikka masala sauce (may contain tree nuts) and the jerk seasoning.
- The Massachusetts allergen notice and the federal calorie statement are in the footer and at checkout.

## 7. Testing tips

- Add `?now=2026-10-13T12:00` to the address to pretend it's Tuesday noon, or `?now=2026-10-13T23:30` to see the "closed" flow.
- Deep links: `order.html#item=bulgogi-bowl` opens a dish directly (good for Instagram), `#byo` opens Build Your Own, `#bag` opens the bag.
- The bag is saved in the visitor's browser, so it survives a refresh.

## Files

```
index.html            HOMEPAGE: text menu (read / print), links into ordering
order.html            ordering page (photos)
order-illustrated.html ordering page (illustrations)
assets/illus/         Riceline illustrations (SVG)
config.js             store settings (address, hours, phone, ordering)
data/menu.js          all menu items, prices, nutrition, allergens
assets/css/styles.css look & feel (colors at the top)
assets/js/core.js     price / calorie / allergen math, store hours
assets/js/ui.js       menu, filters, item sheet, bag, checkout
assets/img/           photos (WebP) + og-image.jpg for link previews
assets/icons/         logo / app icons
credits.html          photo credits (Unsplash)
404.html, robots.txt, manifest.webmanifest, .nojekyll
```
