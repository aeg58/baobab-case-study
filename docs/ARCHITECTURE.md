# BAOBAB Architecture

## Component View

```mermaid
flowchart TB
    subgraph Public["Public experience"]
        Routes["Locale routes: /tr and /en"]
        Catalog["Books and authors"]
        Editorial["Articles, events and workshops"]
        Discovery["Search, newsletter and sales points"]
    end

    subgraph Admin["Authenticated administration"]
        Content["Editorial CRUD workflows"]
        Media["Central media library"]
        Settings["Homepage and site settings"]
        Account["Admin account"]
    end

    subgraph Server["Next.js server layer"]
        Components["Server Components"]
        Actions["Server Actions"]
        Security["Auth.js, Zod and HTML sanitization"]
        Images["Sharp image processing"]
    end

    subgraph Data
        ORM["Prisma ORM"]
        DevDB[("SQLite development / test")]
        ProdDB[("PostgreSQL planned production")]
    end

    Routes --> Components
    Catalog --> Components
    Editorial --> Components
    Discovery --> Components
    Content --> Actions
    Media --> Actions
    Settings --> Actions
    Account --> Security
    Components --> ORM
    Actions --> Security
    Security --> ORM
    Actions --> Images
    ORM --> DevDB
    ORM -. production migration .-> ProdDB
```

## Main Content Relationships

```mermaid
erDiagram
    BOOK }o--o{ AUTHOR : written_by
    BOOK }o--|| BOOK_CATEGORY : categorized_as
    BOOK ||--o{ BOOK_PREVIEW : contains
    BOOK }o--o{ SALES_POINT : available_at
    MEDIA ||--o{ BOOK : illustrates
    MEDIA ||--o{ AUTHOR : portrays
    MEDIA ||--o{ POST : illustrates
    MEDIA ||--o{ EVENT : illustrates
```

The production schema contains additional models for homepage composition,
newsletter subscribers, site settings, hero slides, and administrator access.

## Internationalization Strategy

- Turkish is the default locale.
- Public content is routed under explicit `/tr` and `/en` paths.
- Editorial models contain separate Turkish and English content fields.
- Editors manage both language versions in one administration workflow.
- SEO metadata and structured data are generated for locale-aware pages.

## Editorial Safety

- Rich-text content is validated and sanitized on the server.
- Administrative access uses authenticated sessions and password hashing.
- Media is processed centrally rather than being handled independently by each page.
- Public source, unpublished content, and production credentials are excluded from this case study.

## Deployment Boundary

The application has a Linux/Nginx/PM2 staging path. Production release is kept
separate from application completion because it depends on external analytics,
domain, infrastructure, database, and legal-content approvals.
