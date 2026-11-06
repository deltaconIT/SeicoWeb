# Seico website — English version (editable front-end copy)

This is the English translation of the Seico website. All page text, page titles, image descriptions, search results, menus and code comments are in English, and the page and folder names were translated too (`gioi-thieu.html` → `about/about.html`, `du-an/` → `projects/`, and so on). `docs/renamed-files.csv` lists every old file name and where that page is now.

## Open the website

Extract the ZIP, then open **index.html** in your browser. The package contains ordinary HTML, CSS, JavaScript, fonts and images. You do not need Node.js, npm, a database, a build step or a backend to edit these files.

For the most consistent local browsing, run `python -m http.server 8000` in this folder, then open `http://localhost:8000`. This is an optional local file preview, not a business backend.

## Where things are

```
index.html                HOME PAGE - stays in this top folder

Pages, grouped by the navbar. Each folder holds its main page and its subpages:
about/                    about.html - one page with every About topic (see "About page" below)
products-services/        products-services.html (main page), light-buildings.html
  pre-engineered-steel-building/   main article (pre-engineered-steel-building.html),
                            description, applications, frames, secondary structure
  steel-structure/          description, applications, steel structure design to
                            American standards, steel-structure.html (placeholder)
  accessory-products/       cladding profile for roof and walls (roof-and-wall-panels.html),
                            SP Deck, paint, deck floors
  services/                 design, fabrication (Manufacturing), installation
projects/                 projects.html (main page), industrial-projects.html
  details/                  one page per project (45 pages), named after the project.
                            42 have placeholder images and details to fill in; each page
                            has a note on adding photos
careers/                  careers.html (main page)
  jobs/                     job postings (marketing-manager.html is also the job template)
contact/                  contact.html
shared/                   not in the navbar: privacy policy, and the document placeholder
                            that the brochure/catalogue buttons open
archive/                  pages taken off the site but kept (see "Archived pages" below)
  seico-people.html         the SEICO People listing
  seico-people/             its 7 stories

assets/css/main.css       ALL SITE-WRITTEN PAGE STYLES - header, menus, footer, floating
                          contact buttons, contact modal, shared helper classes and
                          page-specific styles. Pages have no <style> tags.
assets/css/seico-*.css    the original Seico stylesheets (pages, common,
                          products, home slider)
assets/js/main.js         SHARED SITE SCRIPT
                            Part 1: site data - the page list used by the search
                                    box, and the office/factory map locations
                            Part 2: site code - menus, search, sliders, map, forms
assets/js/projects-data.js  THE PROJECT LIST - edit this to add or change projects
assets/js/projects-page.js  Projects page filters, search and page numbers
assets/images/            ALL SITE IMAGES - photos, logos, banners, icons, certificates
vendor/                   third-party libraries only - don't edit
  css/, js/                 Bootstrap 3, jQuery, Owl Carousel, FlexSlider, Swiper,
                            Fancybox, Font Awesome...
  assets/                   the fonts and small images those libraries load
docs/                     reference lists, not used by the pages:
  page-map.json             every page with its file name and title
  renamed-files.csv         original seico.vn file names and where each page is now
  ASSET-NOTES.json          source files that could not be downloaded
news-publications/        ALL News & Publications pages (hidden for now - see below)
  news-publications.html    section landing page
  news.html, publications.html, news/   listing and category pages
  articles/                 the 18 news articles
```

Each page loads its stylesheets in this order, and the order matters because later files override earlier ones:

1. library and original Seico stylesheets (`vendor/css/…`, `assets/css/seico-*.css`)
2. `assets/css/main.css`

To style just one page, add your rule to the **PAGE-SPECIFIC STYLES** part of `main.css`. Pages with their own styles have a class on `<body>` (such as `page-home` or `page-careers`). If a rule could also match on other pages, limit it with `:where(.page-careers) .your-selector`, which adds no specificity. To give a new page its own styles, add a new class to its `<body>`.

Classes starting with `u-` and `tpl-` in `main.css` replaced `style="..."` attributes that were repeated across the site, so changing one updates every page that uses it.

At the bottom of each page, the libraries in `vendor/js/` load first, then `assets/js/main.js`.

## Edit the content

Open `index.html` in a text/code editor to change the homepage. The other `.html` files are the inner pages, in the folders listed above. Links and images use relative paths, so moving or renaming a page means updating every link to it and every path inside it. A new page in the same folder as an existing one can copy that page's paths unchanged.

The original layout, navigation, banners and visual sections are preserved where available. Text inside images (banners, diagrams, certificates) is part of the picture and is still in Vietnamese; replace those images if you need them in English. Pages marked **Your content goes here** are intentional editable templates for your own product details, projects, articles and job descriptions. Replace their text and media placeholders with your content.

The header and footer **HTML** is still repeated in each page, so each page works by itself without a server-side include or a frontend framework. Their **styles**, however, are now in `assets/css/main.css`. After changing branding or shared navigation text, make the same update across the HTML pages. A code editor's multi-file find/replace is useful here.

To add a page to the site search, add a line to the `pages` list at the top of `assets/js/main.js`.

Site images are in `assets/images/`. Change an image by replacing its file (keep the same name), or by adding a new file there and editing the relevant `src` or CSS `background-image` value. From a page, the path starts with `../` once per folder level, for example `../../assets/images/name.jpg` from `products-services/services/design.html`.

## News & Publications is hidden for now

The section still exists and its pages link to each other, but no other page shows a link to it. Nothing was deleted: the links are commented out, so they can be restored. Their addresses already point to the new `news-publications/` locations.

To show the section again, remove the comment markers from these places:

- **Every page:** the two nav entries (mobile and desktop) and the footer link. Search for `news-publications.html` to find them.
- **`index.html`:** the Featured news section, just above `<!-- End home-news -->`.
- **`archive/seico-people.html`** (archived, see below): the News sidebar and the "Radiant SEICO" card.
- **`products-services/pre-engineered-steel-building/pre-engineered-steel-building.html`:** the breadcrumb, News sidebar, "Read more related articles" line, Related news carousel and 10 links inside the article text. For those 10 links, only the `<a>` tags are commented out.
- **`assets/js/main.js`:** the 24 lines starting `// {"path": "/news-publications/` in the search page list.

Two larger hidden blocks (the Featured news section and the Related news carousel) had HTML comments inside them, and comments cannot be nested. Those inner comments are written as `<!~~ ~~>`. Change them back to `<!-- -->` when you un-hide a block.

## Archived pages

SEICO People (the listing and its 7 stories) was taken off the site but not deleted. The pages are in `archive/`, and their links to the rest of the site were updated so they still open correctly. No other page links to them, and they are not in the site search.

To bring SEICO People back:

1. Move `archive/seico-people.html` back to `careers/`, and `archive/seico-people/` back to `careers/seico-people/`. In those files, change `../careers/careers.html` back to `careers.html` (listing) and `../../careers/careers.html` back to `../careers.html` (stories).
2. On every page, give **Careers** its submenu again, in both menus. Desktop: `<a href="…/careers.html" rel="nofollow">Careers<i aria-hidden="true" class="fa fa-angle-down"></i></a><ul class="sub-menu"><li><a href="…/seico-people.html" rel="nofollow">SEICO PEOPLE </a></li></ul>`. Mobile: `<div class="mobile-link-header"><a href="…/careers.html" rel="nofollow">Careers</a><i aria-hidden="true" class="fa fa-plus mobile-nav__toggle-open"></i></div><ul class="sub-menu"><li><a href="…/seico-people.html" rel="nofollow">SEICO PEOPLE </a></li></ul>`.
3. In `careers/careers.html` and the job pages, add the sidebar menu back above OUR OFFICES: `<p class="upper">Careers</p><ul class="menu-page"><li><a href="seico-people.html"><i class="fa fa-angle-double-right"></i> SEICO PEOPLE </a></li></ul>` (from a job page, the link is `../seico-people.html`).
4. Add the pages back to the search list at the top of `assets/js/main.js`.

The story pages still have placeholder text ("Your content goes here").

## Front-end templates, not backend functionality

All forms are templates. They can validate fields and display a template notice, but they do not send email, save inquiries or submit anything to Seico's server. Connect your own backend or form/email service when you are ready.

The footer **Download our profile** button opens a popup form built by `setupProfilePopup` in `assets/js/main.js`. To connect it, add `data-native-form` and your address to its `<form>`, for example `action="/your-endpoint"`, and put the file to offer in the `link_document` field. It then submits by POST with these fields: `firstname`, `lastname`, `email`, `phone_number`, `id_document`, `link_document` and `send_infor_document`.

Links to SEICO's project search on seico.vn first open a popup asking for a full name and email. These are the Vietnam, Thailand and Indonesia menu items and the non-Philippine country flags on the Projects page. The popup is built by `setupInternationalProjectsPopup` in `assets/js/main.js`, and any link whose address starts with `https://seico.vn/en/projects.htm` gets it automatically. Nothing is sent yet: after the fields are checked, the visitor continues to seico.vn. To connect a backend, put your address in that form's `action` (for example `action="/api/project-leads"`). The form is then sent by POST as form data with these fields: `fullname`, `email`, `country` and `destination`. The visitor continues to seico.vn when your server replies, or after 5 seconds, even if the request fails. The popup appears on every click. To ask each browser only once instead, set `ASK_ONCE` to `true` in that function: after the form is filled in, that browser then goes straight to seico.vn.

The Projects page filters, name search, dropdowns and page numbers work without a backend. To add or change a project, edit the list in `assets/js/projects-data.js`; `assets/js/projects-page.js` builds the results from it. Other listing pages (such as News) still use static layouts, and their pagination links don't change the content. Local page search works without a backend. Profile and catalogue download controls lead to an editable document placeholder; original large reference PDFs are deliberately omitted.

On the home page, clicking a **Customers & Partners** logo shows it enlarged in a popup. A logo whose `<a class="partner-logo">` has a `data-project="projects/details/....html"` attribute also gets a **View our project** button that opens that page. To give another logo a button, add the attribute; to remove one, delete it. The company name shown in the popup is the logo's `alt` text.

**Site-wide look.** The inner pages share the About page's style: white cards with soft shadows, blue headings with a short accent bar, and a highlighted side menu. The styles are in `assets/css/main.css` under "SITE-WIDE REFRESH". Each page's `<body>` class tells those styles which layout it uses: `layout-sidebar` (pages with the left menu: products, services, careers, job, SEICO People), `layout-template` (pages built from the content template, including the placeholders), `layout-project` (project detail pages) and `page-contact`. A new page copied from one of these keeps the look automatically. The header, footer and home page keep their original design. For a long article on a template page, wrap the content in `<div class="tpl-content std-page">`, as on `products-services/steel-structure/steel-structure-design-to-american-standards.html` (Steel structure design to American standards). That gives it the larger text, photo captions (`std-figure`), the standards table (`std-table`, which becomes stacked cards on phones; each cell needs a `data-label`) and the notes style. The site script builds the table of contents from the headings automatically.

**About page.** `about/about.html` holds every About topic in one page, following seico.vn/en/about.htm: overview, organization chart, vision and mission, core values, development timeline, QHSE (quality, health, safety, environment), certificates and awards, why choose SEICO, the branch and factory map, and a contact form. The old separate pages (Seico overview, Vision, QHSE and its four subpages, and the two Certificates pages) were copies of the same content and have been removed. Each topic has an address of its own, for example `about/about.html#qhse-safety`. The section ids are `overview`, `organization-chart`, `vision-mission`, `core-values`, `development-timeline`, `qhse`, `qhse-quality`, `qhse-health`, `qhse-safety`, `qhse-environment`, `certificates`, `why-seico`, `network` and `about-contact`. The menu on the left and the last breadcrumb follow the section on screen (`setupAboutPage` in `assets/js/main.js`). Each section's `data-crumb` attribute sets its breadcrumb text. On phones and tablets the menu becomes a row of buttons that stays at the top. The text is seico.vn's English wording, with small spelling fixes. Styles are in `assets/css/main.css` under "About page".

`products-services/products-services.html` is the Products & Services overview page. It has an introduction, the six product cards, the three services (Design, Manufacturing, Installation), the company counters, a "Built by SEICO" section with six featured projects, and a contact call to action. It is ordinary HTML; its styles are in `assets/css/main.css` under "Products & Services overview" and apply only to pages with `<body class="page-ps-hub">`. The **Products & Services** label in the top menu opens this page. On desktop, hovering the label still shows the dropdown. On phones, the + still opens the submenu. The footer link and the breadcrumbs on the product and service pages also lead here.

The company office/factory map and galleries are client-side interface elements. Embedded YouTube videos, external social links and any unavailable source media still require internet access. `docs/ASSET-NOTES.json` lists resources that could not be downloaded; replace those references if you want a fully offline site.

## Before publishing your version

Replace the original logo, business name, phone numbers, email addresses, office addresses, social links, article dates, and any media or documents you do not have permission to reuse. The original contact links remain as reference content, so do not publish this copy as your own business without tailoring them.

Pages include `noindex,nofollow` while this is a reference copy. Remove that meta tag only after you have finished adapting your website. Upload the folder contents to any static web host; keep `index.html` at the site root.

No backend code, database credentials, trackers, original form endpoints or API keys are included.

## What changed in this version

- Translated from Vietnamese to English: page text, `<title>`s, image alt text, buttons, form labels and placeholders, the search page list, the office/factory map, and comments in the HTML and CSS.
- Page and folder names are in English. Every link was updated; `docs/renamed-files.csv` maps the old names to the new ones.
- The page `lang` attribute is now `en`, and the site always shows the English office and factory map data.
- Names of people, companies and projects are kept, written without Vietnamese accents (for example Hai Phong, Le Hoang Anh).
- Share buttons still point to the original Vietnamese pages on seico.vn, because those are addresses on Seico's live site.
