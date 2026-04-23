# Adobe Commerce Developer Professional — Study Guide + Flashcards (AD0-E724)

## Exam facts (confirmed)

| Attribute | Value | Confidence |
|---|---|---|
| Exam code | **AD0-E724** | ✅ |
| Full title | Adobe Certified Professional — Adobe Commerce Developer | ✅ |
| Questions | **50** | ✅ Confirmed (certqueen, itfreedumps, certificationbox) |
| Duration | **100 minutes** | ✅ |
| Passing score | **39 / 50 (78%)** | ✅ |
| Retake wait (1st fail) | 24 hours | ✅ |
| Cost | $125 USD / $95 India (free Summit voucher) | ✅ |
| Prerequisites | **6-12 months hands-on Adobe Commerce 2.4.x development**, PHP + OOP, MySQL, Cloud basics | ✅ |

### Official domain weights (confirmed from multiple sources)

| # | Domain | Weight | Questions |
|---|---|---|---|
| 1 | **Architecture** | **52%** | ~26 |
| 2 | **Customizations** | **36%** | ~18 |
| 3 | **Cloud** | **12%** | ~6 |

**⚠️ 78% pass threshold is high.** You need 39/50 correct. Can only miss ~11 questions.

**Realistic fit check:** the confirmed prerequisite is "6-12 months hands-on Adobe Commerce 2.4.x." If your last Magento 2 backend code was more than a year ago, this exam is brutal. Go in aware.

---

# PART 1 — Full topic coverage

## Domain 1 — Architecture (52%) 🎯 MUST KNOW COLD

### Module File Structure

```
app/code/Vendor/Module/
├── registration.php                 # component registration
├── composer.json                    # (optional) dependencies
├── etc/
│   ├── module.xml                   # module metadata, sequence
│   ├── di.xml                       # DI (global) 
│   ├── frontend/di.xml              # area-specific DI
│   ├── adminhtml/di.xml
│   ├── webapi.xml                   # REST routes
│   ├── events.xml                   # event observers
│   ├── crontab.xml                  # cron jobs
│   ├── indexer.xml                  # indexers
│   ├── acl.xml                      # admin permissions
│   ├── schema.graphqls              # GraphQL schema
│   ├── frontend/routes.xml          # URL routes
│   ├── adminhtml/routes.xml
│   └── db_schema.xml                # declarative schema (2.3+)
├── Setup/Patch/Data/*.php           # data patches
├── Setup/Patch/Schema/*.php         # schema patches
├── Api/                             # service contracts (interfaces)
│   ├── Data/                        # DTO interfaces
│   └── *Interface.php
├── Model/                           # business logic
│   ├── ResourceModel/               # DB layer
│   └── Config/
├── Controller/                      # HTTP entry points
│   ├── Adminhtml/
│   └── ...
├── Block/                           # view-model classes
├── Observer/                        # event handlers
├── Plugin/                          # method wrappers
├── Cron/                            # scheduled tasks
├── Console/Command/                 # CLI commands
└── view/
    ├── frontend/
    ├── adminhtml/
    └── base/
```

### Dependency Injection — the single biggest topic

```xml
<!-- etc/di.xml -->
<config>
    <!-- Preference: replace a class (one winner) -->
    <preference for="Magento\Catalog\Api\ProductRepositoryInterface"
                type="Vendor\Module\Model\ProductRepository"/>

    <!-- Plugin: wrap method (multiple stackable, sortOrder matters) -->
    <type name="Magento\Catalog\Model\Product">
        <plugin name="vendor_product_plugin"
                type="Vendor\Module\Plugin\ProductPlugin"
                sortOrder="10"
                disabled="false"/>
    </type>

    <!-- Type arguments: constructor injection config -->
    <type name="Vendor\Module\Model\MyService">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="limit" xsi:type="number">100</argument>
            <argument name="config" xsi:type="array">
                <item name="key" xsi:type="string">value</item>
            </argument>
        </arguments>
    </type>

    <!-- Virtual type: same class, different config -->
    <virtualType name="VendorLogger" type="Monolog\Logger">
        <arguments>
            <argument name="name" xsi:type="string">vendor-channel</argument>
        </arguments>
    </virtualType>
</config>
```

### Plugin method signatures (MEMORIZE)

```php
// BEFORE plugin — modify args, return array of args (or null to not modify)
public function beforeSetName(Product $subject, string $name): ?array {
    return [strtoupper($name)];
}

// AFTER plugin — modify return value, return new value
public function afterGetPrice(Product $subject, $result): float {
    return $result * 1.1;
}

// AROUND plugin — wrap entire call (most powerful, most expensive)
public function aroundSave(ProductRepository $subject, callable $proceed, Product $product) {
    $this->logger->info('before save');
    $result = $proceed($product);  // call original
    $this->logger->info('after save');
    return $result;
}
```

**Plugin rules:**
- Works ONLY on **public non-final methods** of non-final classes
- Cannot plug static, final, or private methods
- Cannot plug constructors
- Multiple plugins can stack (sortOrder ascending)
- Performance: **after > before > around** (around wraps everything)

### Events & Observers

```xml
<!-- etc/events.xml -->
<config>
    <event name="catalog_product_save_after">
        <observer name="vendor_product_saved"
                  instance="Vendor\Module\Observer\ProductSaved"/>
    </event>
</config>
```

```php
class ProductSaved implements ObserverInterface {
    public function execute(Observer $observer): void {
        $product = $observer->getEvent()->getProduct();
        // or: $observer->getData('product');
    }
}
```

**Common events you should recognize:**
- `customer_register_success` — after customer registration
- `checkout_submit_all_after` — order placed
- `sales_order_save_after` — order record updated
- `catalog_product_save_after` — product saved
- `catalog_product_save_before` — before save
- `controller_action_predispatch_*` — pre-dispatch any controller
- `admin_user_authenticate_after` — admin login

### Plugin vs Observer (tested often)

| Plugin | Observer |
|---|---|
| Wraps a **method call** | Responds to an **event dispatch** |
| Can modify args or return value | Cannot modify the event result |
| Explicit target (class + method) | Loose coupling (event name only) |
| Synchronous | Synchronous (same thread) |
| Best for: extending method behavior | Best for: triggering side effects |

### Module Dependencies

```xml
<!-- etc/module.xml -->
<config>
    <module name="Vendor_Module">
        <sequence>
            <module name="Magento_Catalog"/>
            <module name="Magento_Sales"/>
        </sequence>
    </module>
</config>
```

### CLI Commands — must memorize

```bash
bin/magento setup:upgrade                 # run patches, enable new modules
bin/magento setup:di:compile              # compile DI for production
bin/magento setup:static-content:deploy   # compile CSS/JS for production
bin/magento cache:flush                   # clear ALL caches (stops services)
bin/magento cache:clean                   # clean caches (no service stop)
bin/magento cache:disable                 # disable specific cache type
bin/magento cache:enable
bin/magento cache:status
bin/magento indexer:reindex               # reindex all
bin/magento indexer:reset                 # mark all for reindex
bin/magento indexer:info                  # list indexers
bin/magento indexer:show-mode
bin/magento indexer:set-mode {realtime|schedule}
bin/magento cron:run                      # run cron manually
bin/magento cron:install
bin/magento cron:remove
bin/magento deploy:mode:set {default|developer|production}
bin/magento deploy:mode:show
bin/magento module:enable Vendor_Module
bin/magento module:disable Vendor_Module
bin/magento module:status
bin/magento maintenance:enable
bin/magento maintenance:disable
bin/magento app:config:import
bin/magento config:set path value
```

### Indexers

```xml
<!-- etc/indexer.xml -->
<config>
    <indexer id="vendor_item" view_id="vendor_item_view" class="Vendor\Module\Indexer\Item">
        <title>Vendor Item</title>
        <description>Index Vendor Items</description>
    </indexer>
</config>
```

**Indexer modes (admin-configurable):**
- **Update on Save** (realtime) — slow saves, instant reads
- **Update on Schedule** (cron) — fast saves, cron-delayed reads (recommended for prod)

**Indexer interfaces:**
- `IndexerActionInterface` — must implement `executeFull`, `executeRow`, `executeList`
- `MviewActionInterface` — for materialized view changes
- `executeByDimensions` — partitioned execution (multi-store scaling)

### Cron

```xml
<!-- etc/crontab.xml -->
<config>
    <group id="default">
        <job name="vendor_hourly_job" instance="Vendor\Module\Cron\Hourly" method="execute">
            <schedule>0 * * * *</schedule>
        </job>
    </group>
</config>
```

- Groups: `default`, `index`, `consumers`, custom
- Install cron: `bin/magento cron:install`
- Check scheduled vs running: `cron_schedule` table

### Caching

| Cache Type | Purpose |
|---|---|
| **FPC (Full Page Cache)** | Full HTML per page — Varnish/Redis/built-in |
| **Block HTML Cache** | Per-block HTML cache |
| **Config Cache** | Merged XML config |
| **Layout Cache** | Compiled layout XML |
| **Translation Cache** | i18n strings |
| **DDL Cache** | DB schema |
| **EAV Cache** | EAV attribute metadata |
| **Customer Notification** | Customer notifications |
| **Compiled Config** | DI graph (prod) |
| **Target Rule Index** | Related products rules |

**Cache tags:** `cache_tag` column on cached entry. Flushing by tag invalidates related entries.

### Store Hierarchy

```
Website (top-level scope — e.g., en-US, en-GB)
└── Store (Store Group — catalog + root category)
    └── Store View (frontend presentation — language)
```

- **Website** = highest scope (separate currency, customer accounts)
- **Store** = middle (shares website, has own root category tree)
- **Store View** = lowest (same catalog, different language/presentation)
- Configuration scopes follow: Default → Website → Store → Store View

### URL Rewrites

- `url_rewrite` table
- Types: product, category, cms page, custom
- Created automatically on save, or manually via Marketing → URL Rewrites
- Support redirects (301, 302)

### Localization / i18n

- Translation files: `i18n/en_US.csv` in module / theme
- PHP: `__('string', $args)`
- Phtml: `<?= __('string') ?>`
- JS: `$t('string')` (requires `'mage/translate'` dep)

### Admin Panel Architecture

- Admin controllers: `app/code/Vendor/Module/Controller/Adminhtml/*.php` extending `Magento\Backend\App\Action`
- Admin routes: `etc/adminhtml/routes.xml`
- ACL permissions: `etc/acl.xml` → Admin → Role → Resource permissions
- Admin menu: `etc/adminhtml/menu.xml`
- System config: `etc/adminhtml/system.xml` → Stores → Configuration → [your section]

### Attribute Sets + EAV

- Every EAV entity has an **attribute set** (e.g. "Default" for products, "Bag", "Shoes")
- **Attribute groups** within attribute sets (Product Details, Images, SEO)
- **Attribute scope:** Global, Website, Store View
- EAV tables: `eav_attribute`, `eav_entity_attribute`, per-entity value tables (`catalog_product_entity_varchar`, etc.)

### Declarative Schema (Magento 2.3+)

- `etc/db_schema.xml` — define tables declaratively
- `bin/magento setup:db-declaration:generate-whitelist` — whitelist new tables
- Replaces old imperative `InstallSchema`, `UpgradeSchema` scripts

### Setup Patches (Magento 2.3+)

```php
// Setup/Patch/Data/AddConfigValue.php
class AddConfigValue implements DataPatchInterface {
    public function __construct(private ModuleDataSetupInterface $moduleDataSetup) {}

    public static function getDependencies(): array {
        return [SomeOtherPatch::class];
    }

    public function getAliases(): array { return []; }

    public function apply(): void {
        // data modifications
    }
}
```

- Replaces legacy `InstallData` / `UpgradeData`
- Auto-run by `bin/magento setup:upgrade`
- Version-independent (unlike Schema `UpgradeSchema`)

---

## Domain 2 — Customizations (36%)

### Catalog Customizations

- **Product types:** Simple, Configurable, Grouped, Bundle, Virtual, Downloadable
- **Custom product type:** extend `Magento\Catalog\Model\Product\Type\AbstractType`
- **Attribute creation:** via Setup Patch (`eav_setup`) or Admin UI
- **Custom options:** per-product options (size, engraving)
- **Tier pricing** vs **Special price** vs **Catalog price rules** vs **Cart price rules**
- **Categories:** nested tree, root category per store

### Checkout Customizations

- Multi-step checkout built on Knockout + UI Components
- Customize via UI Component overrides + plugins on `Magento\Checkout\Model\*`
- Shipping methods: extend `Magento\Quote\Model\Quote\Address\RateCollectorInterface`
- Payment methods: extend `Magento\Payment\Model\MethodInterface`
- Quote (cart) to Order lifecycle

### Sales Customizations

- Order states vs statuses (state = system; status = admin label)
- Default states: New, Pending Payment, Processing, Complete, Closed, Cancelled, Holded, Payment Review
- Custom order statuses map to states
- Invoices, Shipments, Credit Memos created from orders
- Order grid sync — indexed for performance

### Custom Entities (EAV vs Flat)

- **EAV entities:** Product, Customer, Category (dynamic attributes via UI)
- **Flat entities:** Order, Quote, etc. (fixed schema)
- Create custom EAV entity: extend `Magento\Eav\Model\Entity\AbstractEntity`
- Flat table custom entity: declare in db_schema.xml + models

### Custom Admin Grids (UI Components)

UI Components in admin use XML-declarative structure:

```xml
<!-- view/adminhtml/ui_component/vendor_listing.xml -->
<listing>
    <dataSource name="vendor_listing_data_source">
        <argument name="dataProvider" xsi:type="configurableObject">
            <argument name="class" xsi:type="string">Vendor\Module\Model\ResourceModel\Item\Grid\Collection</argument>
            ...
        </argument>
    </dataSource>
    <columns name="vendor_listing_columns">
        <column name="id">...</column>
        <column name="name">...</column>
    </columns>
</listing>
```

### REST API (WebAPI)

```xml
<!-- etc/webapi.xml -->
<routes>
    <route url="/V1/vendor/items/:id" method="GET">
        <service class="Vendor\Module\Api\ItemRepositoryInterface" method="getById"/>
        <resources>
            <resource ref="Vendor_Module::view"/>
        </resources>
    </route>
    <route url="/V1/vendor/items" method="POST">
        <service class="Vendor\Module\Api\ItemRepositoryInterface" method="save"/>
        <resources>
            <resource ref="Vendor_Module::create"/>
        </resources>
    </route>
</routes>
```

- Service interface in `Api/`
- Data interface (DTO) in `Api/Data/`
- Interfaces annotated `@api` = public stable API
- REST, SOAP, or both

### GraphQL

```graphql
# etc/schema.graphqls
type Query {
    vendorItem(id: Int!): VendorItem
        @doc(description: "Get vendor item")
        @resolver(class: "Vendor\\Module\\Model\\Resolver\\GetItem")
}

type VendorItem @doc(description: "Vendor item") {
    id: Int
    name: String
    price: Float
}
```

Resolver class implements `ResolverInterface` with single `resolve()` method.

### Areas

| Area | Purpose | Config path |
|---|---|---|
| `frontend` | Customer-facing | `etc/frontend/` |
| `adminhtml` | Admin panel | `etc/adminhtml/` |
| `crontab` | Cron jobs | `etc/crontab/` |
| `webapi_rest` | REST API | `etc/webapi_rest/` |
| `webapi_soap` | SOAP API | `etc/webapi_soap/` |
| `graphql` | GraphQL endpoint | `etc/graphql/` |
| `base` | Defaults (all areas) | `etc/` |

### Adobe Commerce-specific features (beyond Magento OS)

- **B2B features:** Companies, Shared Catalogs, Quotes, Credit limits, Requisition lists
- **Staging & Preview:** Schedule content/product changes with preview
- **Content Staging:** timed product/category changes
- **Page Builder:** visual content editor
- **Advanced Reporting:** MBI (Magento Business Intelligence) integration
- **Customer Segments:** dynamic segmentation for promotions

### Adobe Commerce Cloud SaaS Data Services

- **Commerce Services:** Catalog Service, Live Search, Product Recommendations (SaaS-based)
- **Data Flow:** Commerce → Commerce Services mesh → Merchant frontend via GraphQL
- **Eventing:** Adobe I/O Events for integration

---

## Domain 3 — Cloud (12%)

### Adobe Commerce Cloud Architecture

- **Magento Cloud Docker** for local dev (mimics cloud environment)
- **Pro plan:** 3-tier (Integration / Staging / Production), auto-deployed
- **Starter plan:** simplified single-stack

### Environments

- **Integration** — feature branches auto-deploy
- **Staging** — pre-prod, closest to production
- **Production** — live, 3-node HA cluster (prod-only)

### Configuration Files

- `.magento.app.yaml` — application config (routes, relationships, workers, crons, build/deploy hooks, PHP version, extensions)
- `.magento/services.yaml` — services (MariaDB, Redis, ElasticSearch/OpenSearch, RabbitMQ)
- `.magento/routes.yaml` — domain routing, redirects, SSL
- `app/etc/config.php` — committed system config (pipeline-deployed config)
- `app/etc/env.php` — environment-specific secrets (not committed)
- `auth.json` — Composer auth keys (sensitive)

### Deployment Phases (the lifecycle)

1. **Build phase** — Composer install, Magento di:compile, static content deploy — runs in build container
2. **Deploy phase** — app/etc/env.php generated, DB migrations run
3. **Post-deploy phase** — cache warmup, container-ready, tests

### Cloud CLI Tool (`magento-cloud`)

```bash
magento-cloud login
magento-cloud project:list
magento-cloud environment:list
magento-cloud environment:ssh                # SSH into environment
magento-cloud db:sql                         # DB shell
magento-cloud db:dump                        # download DB dump
magento-cloud environment:activate
magento-cloud environment:deactivate
magento-cloud environment:redeploy
magento-cloud mount:list
magento-cloud variable:list
magento-cloud variable:set
```

### Cloud-Specific Config

- **Fastly** (CDN) config via modules in Admin
- **Blackfire** profiling in Staging/Prod
- **New Relic APM** out-of-box
- **File mounts** (`pub/media`, `var`, etc.) — persistent across deploys
- **Read-only filesystem** elsewhere — cannot write to `app/code/` in runtime

### SCD Strategies (Static Content Deploy)

- **SCD_ON_DEPLOY** (default) — runs during deploy phase (downtime window)
- **SCD_ON_BUILD** — runs during build (faster deploy, more build time)
- **SCD_ON_DEMAND** — runs per request (dev only, don't use prod)

---

# PART 2 — Rapid-Scan Flashcards

## ⚡ Top 15 most-tested distinctions

| A | B | Discriminator |
|---|---|---|
| **Preference** | **Plugin** | Preference = class replace (one winner); Plugin = AOP wrapper (stack multiple) |
| **before plugin** | **after plugin** | before = modify args; after = modify return value |
| **around plugin** | **before/after** | around wraps whole call (expensive); before/after are targeted |
| **Plugin** | **Observer** | Plugin wraps method call; Observer responds to event dispatch |
| **Virtual Type** | **Preference** | Virtual Type = reuse class w/ different args; Preference = swap class |
| **Setup Patch** | **UpgradeSchema/Data** | Patches (new 2.3+) with dependencies; legacy scripts deprecated |
| **Schema Patch** | **Data Patch** | Schema Patch modifies DB structure; Data Patch modifies data |
| **Declarative Schema** | **InstallSchema** | Declarative = db_schema.xml (desired state); Install = imperative (legacy) |
| **Update on Save** | **Update on Schedule** | Save = realtime reindex; Schedule = cron reindex (prod recommended) |
| **Website** | **Store** | Website = top scope (currency, customers); Store = catalog root category |
| **Store** | **Store View** | Store = catalog + root category; Store View = language/presentation |
| **EAV** | **Flat** | EAV = dynamic attributes; Flat = fixed schema |
| **Service Contract** | **Repository** | Contract = Api/ interface (stable); Repository = Model persistence impl |
| **cache:flush** | **cache:clean** | flush = stops services, nukes everything; clean = only invalidated entries |
| **SCD on Deploy** | **SCD on Build** | On Deploy = downtime during deploy; On Build = front-loaded to build (faster deploy) |

## ⚡ Plugin rules (cold memorize)

- Works on **public non-final methods of non-final classes** only
- ❌ Cannot plug: static, final, private, protected, constructors
- ✅ Multiple plugins stack (sortOrder ascending = runs first)
- Performance: **after > before > around**

## ⚡ Plugin signatures

```php
public function beforeMETHOD($subject, ...$args) {}       // return [args] or null
public function afterMETHOD($subject, $result, ...$args) {}  // return modified $result
public function aroundMETHOD($subject, callable $proceed, ...$args) {}  // wraps
```

## ⚡ Common events (recognize these names)

`customer_register_success` · `checkout_submit_all_after` · `sales_order_save_after` · `catalog_product_save_after` · `catalog_product_save_before` · `controller_action_predispatch_*` · `admin_user_authenticate_after`

## ⚡ Areas map

`frontend` · `adminhtml` · `crontab` · `webapi_rest` · `webapi_soap` · `graphql` · `base`

## ⚡ Product types (all 6)

Simple · Configurable · Grouped · Bundle · Virtual · Downloadable

## ⚡ Order states vs statuses

- State = system-enforced (New, Processing, Complete, Cancelled, Closed, Holded, Pending Payment, Payment Review)
- Status = admin label mapped to state

## ⚡ Caching essentials

FPC · Block · Config · Layout · Translation · DDL · EAV · Compiled Config · Target Rule Index

## ⚡ Cloud environments

Integration (feature branches) → Staging → Production (3-node HA on Pro plan)

## ⚡ Cloud config files

`.magento.app.yaml` · `.magento/services.yaml` · `.magento/routes.yaml` · `app/etc/config.php` (committed) · `app/etc/env.php` (not committed)

## ⚡ CLI top 15

```
setup:upgrade · setup:di:compile · setup:static-content:deploy · cache:flush · cache:clean · 
indexer:reindex · indexer:set-mode · cron:run · cron:install · 
deploy:mode:set {developer|production} · module:enable · module:disable · maintenance:enable · maintenance:disable · 
app:config:import
```

## ⚡ GraphQL / REST / SOAP API config

- REST: `etc/webapi.xml` with service interface reference
- GraphQL: `etc/schema.graphqls` + Resolver class
- Service Contracts: interfaces in `Api/` (mark `@api` for stable public)

## ⚡ di.xml instruction types

`preference` · `type` + `arguments` · `virtualType` · `plugin`

## ⚡ Exam strategy

- **Pass = 39/50 (78%)** — can only miss 11 questions. Not much room for guessing.
- **DI + plugin syntax is ~30% of questions.** Know plugin signatures cold.
- **Spot-the-bug code questions:** watch for public vs private, missing `$subject` param, wrong return types
- **Cloud is 12%** = ~6 questions. Don't over-study; focus on config file names + environments
- **If you don't recognize a specific class / method name**, pick the answer that matches Magento conventions (camelCase, DI-friendly, area-scoped)
- **78% pass bar is the toughest among your Summit exams** — go in with realistic expectations

---

## Sources used

- [Adobe AD0-E724 certification page (Adobe)](https://certification.adobe.com/courses/1186)
- [CertificationBox AD0-E724 guide (confirmed 50q / 100min / 39 pass / domain weights)](https://www.certificationbox.com/2025/05/01/cracking-the-adobe-commerce-developer-professional-exam/)
- [CertQueen AD0-E724 sub-topic summary](https://www.certqueen.com/AD0-E724.html)
- [ITFreeDumps AD0-E724 exam prep](https://www.itfreedumps.com/ad0-e724-adobe-commerce-developer-professional-exam-preparation-resources/)
- Magento 2 developer documentation (`devdocs.magento.com`, Adobe Experience League)
