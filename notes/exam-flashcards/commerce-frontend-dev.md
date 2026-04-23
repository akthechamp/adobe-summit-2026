# Adobe Commerce Front-end Developer Professional — Study Guide + Flashcards (AD0-E726)

## Exam facts

| Attribute | Value | Confidence |
|---|---|---|
| Exam code | **AD0-E726** | ✅ Confirmed (Adobe cert catalog) |
| Full title | Adobe Certified Professional — Adobe Commerce Front-end Developer | ✅ |
| Replaces | AD0-E721 (older version) | ✅ |
| Questions | ~50 (standard Commerce Professional format; matches AD0-E712 and AD0-E724) | ⚠️ Not publicly confirmed |
| Duration | ~100 min | ⚠️ Not publicly confirmed |
| Passing score | ~39/50 (78%) likely (matches AD0-E724) | ⚠️ Not publicly confirmed |
| Retake wait (1st fail) | 24 hours | ✅ |
| Cost | ~$125 USD (free Summit voucher) | ✅ |
| Prerequisites | 6-12 months Magento 2 theming + frontend work | ✅ (inferred from Dev Pro prerequisites) |

**Research limitation:** Adobe keeps the detailed exam guide behind login. Only the paid prep vendors (certswarrior, marks4sure) reference it and one source gave suspicious numbers (120q/120min/66% — likely incorrect). I've assumed it follows the same format as AD0-E724 (50q/100min/39 pass) since they're sibling Commerce Professional exams. **Verify question count on exam check-in.**

### Expected domain structure (reconstructed from Adobe's AD0-E721→AD0-E726 transition + standard Magento FE curriculum)

| Domain | Est. weight | What it covers |
|---|---|---|
| Themes & Layout | ~25-30% | Theme structure, layout XML, page types, handles |
| Templates & Blocks | ~20-25% | .phtml, blocks, containers, UI composition |
| JavaScript | ~15-20% | RequireJS, Knockout, UI Components JS, mixins, jQuery widgets |
| CSS & Styling | ~10-15% | LESS, variables, theme extending |
| Page Builder | ~10-15% | Content types, custom content type dev |
| Customer-facing features | ~5-10% | Checkout UI, minicart, customer account |
| (optional) PWA Studio | ~5% | If in scope — PWA/venia theme basics |

---

# PART 1 — Full topic coverage

## Domain 1 — Themes & Layout (~25-30%)

### Theme File Structure

```
app/design/frontend/Vendor/theme-name/
├── theme.xml                          # theme metadata + parent
├── registration.php                   # component registration
├── composer.json                      # (optional, for Composer distribution)
├── preview.jpg                        # theme preview thumbnail
├── etc/
│   └── view.xml                       # image dimensions, media gallery config
├── Magento_Theme/                     # override Magento_Theme module
│   ├── layout/
│   │   └── default.xml                # site-wide layout overrides
│   └── templates/
│       └── header.phtml               # override header template
├── Magento_Catalog/
│   ├── layout/
│   │   ├── catalog_product_view.xml
│   │   └── catalog_category_view.xml
│   └── templates/
├── Magento_Checkout/                  # override checkout
├── web/
│   ├── css/
│   │   └── source/
│   │       ├── _extend.less           # append to parent (additive)
│   │       ├── _theme.less            # override parent variables
│   │       └── _module.less           # module-specific LESS
│   ├── images/
│   ├── js/
│   └── template/                      # Knockout templates
└── requirejs-config.js                # JS map/paths/shim/mixins
```

### Theme Declaration

```xml
<!-- theme.xml -->
<theme xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="urn:magento:framework:Config/etc/theme.xsd">
    <title>Vendor Theme Name</title>
    <parent>Magento/blank</parent>  <!-- or Magento/luma -->
    <media>
        <preview_image>media/preview.jpg</preview_image>
    </media>
</theme>
```

### Theme Hierarchy (Inheritance / Fallback)

- Child theme overrides parent
- `Magento/blank` = minimal parent theme (most common parent)
- `Magento/luma` = full demo theme (extends blank)
- Fallback for files: child → parent → ancestor → module
- Files NOT found in child fall through to parent

### Page Types = Layout Handles

| Handle | Page |
|---|---|
| `default` | All pages (base layout) |
| `cms_index_index` | Home page (CMS) |
| `cms_page_view` | CMS pages |
| `catalog_product_view` | Product detail page |
| `catalog_category_view` | Category listing |
| `catalog_category_view_type_default` | Specific category type |
| `catalog_product_view_type_simple` | Simple product |
| `catalog_product_view_type_configurable` | Configurable product |
| `catalogsearch_result_index` | Search results |
| `checkout_cart_index` | Cart page |
| `checkout_index_index` | Checkout page |
| `checkout_onepage_success` | Order confirmation |
| `customer_account` | My account base |
| `customer_account_login` | Login page |
| `customer_account_create` | Register page |
| `sales_order_view` | Order view (account) |

### Layout XML — core instructions

```xml
<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      layout="1column"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    
    <!-- Update from another handle -->
    <update handle="catalog_category_default"/>
    
    <body>
        <!-- Reference existing block -->
        <referenceBlock name="product.info.price">
            <action method="setTemplate">
                <argument name="template" xsi:type="string">Vendor_Module::price.phtml</argument>
            </action>
        </referenceBlock>
        
        <!-- Reference existing container -->
        <referenceContainer name="content.top">
            <block class="Vendor\Module\Block\MyBlock" 
                   name="my.custom.block" 
                   template="Vendor_Module::custom.phtml"/>
        </referenceContainer>
        
        <!-- Move block -->
        <move element="product.info.price" 
              destination="product.info.main" 
              after="product.info.details"/>
        
        <!-- Remove block -->
        <referenceBlock name="product.info.upsell" remove="true"/>
    </body>
</page>
```

### Layout Instructions reference

| Instruction | Purpose |
|---|---|
| `<page>` | Root element, declares page layout (1column, 2columns-left, 2columns-right, 3columns) |
| `<update handle="..."/>` | Include another layout handle |
| `<block>` | Define new block |
| `<container>` | Define new container |
| `<referenceBlock name="...">` | Modify existing block |
| `<referenceContainer name="...">` | Modify existing container |
| `<move element="..." destination="..." before="-|..." after="-|..."/>` | Reposition |
| `<remove name="..."/>` OR `remove="true"` attribute | Delete from output |
| `<action method="..."/>` | Call a method on a block |
| `<arguments>...<argument>` | Pass data to block |

### Page Layouts (known 1-3 column)

- `1column` — single column (e.g. checkout, landing)
- `2columns-left` — sidebar left
- `2columns-right` — sidebar right
- `3columns` — sidebar left + right
- `empty` — for totally custom
- `admin-1column` / `admin-2columns-left` (adminhtml)

### Block vs Container

- **Block** = renders output (has a template)
- **Container** = groups blocks (no template, no output of its own — just structure)
- Both have `name` attribute (unique identifier)

---

## Domain 2 — Templates & Blocks (~20-25%)

### .phtml Template Basics

```php
<?php
/** @var \Vendor\Module\Block\MyBlock $block */
/** @var \Magento\Framework\Escaper $escaper */
?>
<div class="my-container" data-scope="<?= $escaper->escapeHtmlAttr($block->getScope()) ?>">
    <h2><?= $escaper->escapeHtml($block->getTitle()) ?></h2>
    <p><?= $escaper->escapeHtml($block->getDescription()) ?></p>
    <a href="<?= $escaper->escapeUrl($block->getUrl()) ?>">Link</a>
</div>
```

### Escaping (critical — tested)

- `$escaper->escapeHtml($value)` — for HTML text content
- `$escaper->escapeHtmlAttr($value)` — for HTML attribute values
- `$escaper->escapeUrl($url)` — for URL in href/src
- `$escaper->escapeJs($value)` — for JS strings
- `$escaper->escapeCss($value)` — for CSS values
- `$escaper->escapeQuote($value)` — for double-quote content
- **Never** `<?= $block->getX() ?>` raw user input — always escape

### Block Classes

```php
namespace Vendor\Module\Block;

use Magento\Framework\View\Element\Template;

class MyBlock extends Template {
    public function __construct(
        Template\Context $context,
        private SomeDataProvider $dataProvider,
        array $data = []
    ) {
        parent::__construct($context, $data);
    }
    
    public function getTitle(): string {
        return $this->dataProvider->getTitle();
    }
    
    // Cached data (block-level cache)
    public function getCacheKeyInfo() {
        return array_merge(parent::getCacheKeyInfo(), [$this->getParam('id')]);
    }
}
```

### Template Inheritance

- Override template: place override in theme at same path
- e.g. override `vendor/magento/module-catalog/view/frontend/templates/product/view/form.phtml` → put in `app/design/frontend/Vendor/Theme/Magento_Catalog/templates/product/view/form.phtml`
- Or change via layout: `<action method="setTemplate"><argument xsi:type="string">Vendor_Module::custom.phtml</argument></action>`

### Translation in .phtml

```php
<?= __('Welcome to the store') ?>
<?= __('Hello, %1', $block->getCustomerName()) ?>
```

---

## Domain 3 — JavaScript (~15-20%)

### RequireJS Config

```javascript
// requirejs-config.js (in theme or module)
var config = {
    map: {
        '*': {
            // Override a core module
            'Magento_Checkout/js/view/summary': 'Vendor_Theme/js/view/summary'
        }
    },
    paths: {
        // Alias to avoid long paths
        'vendor-lib': 'Vendor_Theme/js/vendor-lib'
    },
    shim: {
        // Non-AMD module dependencies
        'vendor-lib': {
            deps: ['jquery']
        }
    },
    config: {
        mixins: {
            // Inject mixin — runs alongside original
            'Magento_Checkout/js/view/summary': {
                'Vendor_Theme/js/mixin/summary-mixin': true
            }
        }
    }
};
```

### Mixins

- Non-destructive extension of JS components
- Wrap original with extra logic without modifying source

```javascript
// Vendor_Theme/js/mixin/summary-mixin.js
define(['jquery'], function($) {
    'use strict';
    return function(target) {
        return target.extend({
            defaults: {
                extraField: ''
            },
            initialize: function() {
                this._super();
                console.log('Mixin initialized');
                return this;
            }
        });
    };
});
```

### jQuery UI Widgets (Magento extends jQuery UI)

```javascript
// Vendor_Theme/js/my-widget.js
define(['jquery', 'jquery/ui'], function($) {
    $.widget('mage.myWidget', {
        options: {
            defaultOption: 'value'
        },
        _create: function() {
            // init logic
        },
        publicMethod: function() {
            // callable via $('.selector').myWidget('publicMethod')
        }
    });
    return $.mage.myWidget;
});
```

Attach in .phtml:
```html
<div class="my-widget" data-mage-init='{"Vendor_Theme/js/my-widget": {"option1": "value"}}'>
    content
</div>
```

### UI Components (Knockout-based)

4-file pattern for a UI Component:

```
1. Layout XML (declares):
   view/frontend/layout/example.xml
   <uiComponent name="my_component"/>

2. Component XML (structure):
   view/frontend/ui_component/my_component.xml

3. JS Component:
   view/frontend/web/js/view/my-component.js
   define(['uiComponent'], function(Component) {
       return Component.extend({
           defaults: {
               template: 'Vendor_Theme/my-component-template'
           }
       });
   });

4. HTML Template (Knockout):
   view/frontend/web/template/my-component-template.html
   <div data-bind="text: title"></div>
```

### Knockout Bindings (Magento's flavor)

```html
<div data-bind="scope: 'my-component'">
    <!-- Inline binding -->
    <h2 data-bind="text: getTitle()"></h2>
    <p data-bind="text: description"></p>
    
    <!-- Foreach loop -->
    <ul data-bind="foreach: items">
        <li data-bind="text: name"></li>
    </ul>
    
    <!-- Event binding -->
    <button data-bind="click: onSave, css: {disabled: isDisabled}">Save</button>
    
    <!-- Scope for Magento UI Components -->
    <each args="getRegion('extra-content')" render=""></each>
</div>
```

### i18n in JS

```javascript
define(['mage/translate'], function($t) {
    return {
        message: $t('Hello World')
    };
});
```

Or in .phtml data-bind:
```html
<span data-bind="i18n: 'Hello World'"></span>
```

### AJAX in Magento

```javascript
define(['jquery', 'mage/storage'], function($, storage) {
    storage.get('rest/V1/customer/me', false).done(function(response) {
        console.log(response);
    });
});
```

---

## Domain 4 — CSS & LESS Styling (~10-15%)

### LESS (not Sass) — Magento 2 Standard

- Variables: `@color-primary`, `@spacer__l` (BEM-double-underscore convention)
- Nesting OK but limit depth
- Mixins + functions
- `_extend.less` = additive (parent + child)
- `_theme.less` = override parent variables

```less
// web/css/source/_theme.less
@color-primary: #C15F3C;          // override variable
@font-family-base: 'Inter Tight', sans-serif;

// web/css/source/_extend.less
.custom-class {
    color: @color-primary;
    &:hover {
        color: darken(@color-primary, 10%);
    }
}
```

### CSS Architecture Conventions

- **BEM-like** — block__element--modifier
- **`_module.less` files** named per module they affect
- **CSS compiled server-side** or via Grunt (dev)

### Static Content Deploy

```bash
bin/magento setup:static-content:deploy en_US -f
bin/magento setup:static-content:deploy en_US -t Vendor/theme
```

- Runs LESS compilation
- Copies to `pub/static/frontend/Vendor/theme/en_US/`
- Production mode requires this before deploy

### Grunt (Dev Mode)

```bash
grunt exec:<theme>       # copy files to pub/static
grunt less:<theme>       # compile LESS
grunt watch              # auto-compile on change
```

### Responsive Design

- Magento uses mobile-first approach
- Breakpoints via LESS media queries: `@screen__s`, `@screen__m`, `@screen__l`, `@screen__xl`
- Flex-based grid in Luma

---

## Domain 5 — Page Builder (~10-15%)

### Overview

- Drag-drop content editor in Admin (for CMS pages, blocks, product descriptions, category descriptions)
- Out-of-box content types: Layout (row, column, tabs, accordion), Elements (heading, text, buttons, image, video, HTML code), Media (map, slider, banner), Add Content (block, dynamic block, products, schedule)

### Custom Content Types

```
view/adminhtml/pagebuilder/content_type/
├── my_content_type.xml                # content type config
├── preview.phtml                      # admin-side preview
└── ...

view/base/web/ (or view/frontend/web/)
├── template/content-type/my_content_type/
│   ├── default.html                   # Knockout admin template
│   └── ...
└── js/content-type/my_content_type/
    ├── preview.js                     # admin preview JS
    ├── widget.js                      # frontend widget
    └── ...
```

### Content Type XML

```xml
<type name="my_content_type" label="My Content Type" menu_section="elements" group="general" sort_order="10">
    <icon>path/to/icon.svg</icon>
    <appearances>
        <appearance name="default" preview_template="Vendor_Module/content-type/my_content_type/default/preview" master_template="Vendor_Module/content-type/my_content_type/default/master">
            <elements>
                <element name="main">
                    <style name="padding">
                        <source>padding</source>
                        <converter>...</converter>
                    </style>
                </element>
            </elements>
        </appearance>
    </appearances>
</type>
```

### Page Builder Inheritance

- Extend existing types (e.g. extend `heading` to add extra styles)
- Override via theme (place override in theme's Page Builder content_type folder)

---

## Domain 6 — Customer-facing Features (~5-10%)

### Checkout

- **Knockout-heavy** — customizations via UI Component mixins
- **Shipping step** and **Payment step** are UI Components
- Custom checkout field: add via `etc/frontend/di.xml` + Knockout UI Component
- **Quote vs Order** — Quote is pre-payment cart, Order is post-payment

### Minicart

- Also Knockout/UI Component
- `Magento_Checkout/js/view/minicart` — customizable via mixin
- Sidebar view, hoverable product list

### Customer Account

- Sections in `customer.account.navigation` container
- Add custom tab: extend `sales.order.history.info.buttons` container or add new link

### Product View Page

- `catalog_product_view.xml` handle
- Key blocks: `product.info.main`, `product.info.price`, `product.info.media`, `product.info.details`, `product.info.upsell`, `product.info.related`

---

## Domain 7 — PWA Studio (optional, ~5% if in scope)

### Overview

- Separate frontend in React
- Uses Apollo Client + GraphQL + service workers
- **Venia** = sample theme for PWA Studio
- Runs as standalone app, calls Adobe Commerce via GraphQL

### When it might appear on exam

- High-level architectural questions about PWA vs traditional theme
- GraphQL queries for products/categories
- Service Worker caching strategy

---

# PART 2 — Rapid-Scan Flashcards

## ⚡ Top 12 most-tested distinctions

| A | B | Discriminator |
|---|---|---|
| **Block** | **Container** | Block renders (has template); Container groups blocks (no output) |
| **referenceBlock** | **referenceContainer** | Modify existing block vs existing container |
| **`<move>`** | **`<remove>`** | Move repositions; Remove deletes |
| **Layout XML** | **Template** | Layout = XML structure; Template = .phtml HTML |
| **Luma** | **Blank** | Luma = full demo (extends Blank); Blank = minimal parent |
| **Widget (jQuery UI)** | **UI Component** | Widget = `$.widget('mage.x')`; UI Component = Knockout-based |
| **Mixin** | **Override (path fallback)** | Mixin wraps via requirejs-config; Override replaces via theme fallback |
| **`_extend.less`** | **`_theme.less`** | `_extend` appends styles; `_theme` overrides variables |
| **RequireJS `map`** | **RequireJS `paths`** | `map` remaps module references; `paths` aliases paths |
| **RequireJS `shim`** | **RequireJS `mixins`** | `shim` = deps for non-AMD; `mixins` = inject wrapper |
| **Page Builder content type** | **Page Builder appearance** | content_type = what it is; appearance = how it renders |
| **Quote** | **Order** | Quote = pre-payment cart state; Order = post-payment record |

## ⚡ Theme file structure essentials

- `theme.xml` → parent + title
- `Magento_Theme/layout/default.xml` → site-wide layout
- `Magento_Module/layout/*.xml` → module-scoped overrides
- `web/css/source/_extend.less` (additive)
- `web/css/source/_theme.less` (variable overrides)
- `requirejs-config.js` → JS config

## ⚡ Layout handles (top 10)

`default` · `cms_index_index` · `cms_page_view` · `catalog_product_view` · `catalog_category_view` · `catalogsearch_result_index` · `checkout_cart_index` · `checkout_index_index` · `checkout_onepage_success` · `customer_account`

## ⚡ Layout instructions

`<page>` · `<update handle="...">` · `<block>` · `<container>` · `<referenceBlock>` · `<referenceContainer>` · `<move>` · `<remove>` · `<action method="...">` · `<arguments>`

## ⚡ Page layouts

`1column` · `2columns-left` · `2columns-right` · `3columns` · `empty`

## ⚡ Escaping methods in .phtml

`escapeHtml` · `escapeHtmlAttr` · `escapeUrl` · `escapeJs` · `escapeCss` · `escapeQuote`

## ⚡ UI Component 4-file pattern

1. Layout XML (declares `<uiComponent name="..."/>`)
2. Component definition XML (structure + data)
3. JS component (`uiComponent` extension)
4. HTML template (Knockout `data-bind`)

## ⚡ Knockout bindings you'll see

`text` · `html` · `foreach` · `if` · `ifnot` · `visible` · `click` · `css` · `attr` · `value` · `scope` · `i18n` · `each` (Magento-specific)

## ⚡ RequireJS config keys

`map` (alias module references) · `paths` (alias paths) · `shim` (non-AMD deps) · `config.mixins` (wrap components)

## ⚡ LESS compilation

```bash
# Dev (instant compile via Grunt)
grunt less:<theme>

# Production (static content deploy)
bin/magento setup:static-content:deploy en_US -t Vendor/theme -f
```

## ⚡ Translation pattern

- PHP: `__('Text')`
- Phtml: `<?= __('Text') ?>`
- JS: `$t('Text')` with `'mage/translate'` dep
- CSV: `i18n/en_US.csv`

## ⚡ Product page key blocks

`product.info.main` · `product.info.price` · `product.info.media` · `product.info.details` · `product.info.upsell` · `product.info.related`

## ⚡ Checkout is Knockout-heavy

- Customize via **UI Component mixins**, not direct edits
- Core: `Magento_Checkout/js/view/*`
- Forms: KO with `data-bind="scope: 'checkoutProvider'"`

## ⚡ Exam strategy

- **Pass bar likely 78%** (matching AD0-E724) — 39+/50
- **Layout XML questions ~25-30%** of exam — if `referenceBlock` vs `referenceContainer` feels unfamiliar → high-fail risk
- **Spot-the-bug code questions** — check for: wrong element names (block vs container), wrong attribute names (name vs as), wrong escaping
- **RequireJS config with `map`/`mixins`** commonly tested — memorize pattern
- **If you haven't built a Magento theme in the last 12 months**, recognize the limitation and pace yourself for guesswork on code fragments
- **Escaping is the security quick-win** — when in doubt, pick the answer that escapes output

---

## Sources used

- [Adobe AD0-E726 certification page (Adobe, official)](https://certification.adobe.com/courses/1247)
- [Adobe Commerce Front-end Developer Professional Prep Guide (login-gated)](https://certification.adobe.com/courses/1188)
- [AD0-E721 (predecessor exam) sample questions EDUSUM](https://www.edusum.com/adobe/ad0-e721-adobe-commerce-front-end-developer-professional)
- Adobe Commerce developer documentation (Experience League)
- Magento 2.4.x DevDocs archived content

**Note:** AD0-E726 replaced AD0-E721 — most public content still references E721. Content coverage is the same; exam format may have minor differences.
