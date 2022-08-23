---
description: Generate a Sitemap XML file for your website.
---

# Sitemap

The **Sitemap** class can generate a XML Sitemap for your website. This can be passed to Google or other search engines to improve your website indexing and boost your SEO.

The sitemap is actually composed of multiple files, an **index** file that references other XML files where the URLs are listed.

Example:

```xml
// Index XML
<?xml version="1.0" encoding="UTF-8"?>
<sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <sitemap>
        <loc>https://mywebsite.com/sitemap/sitemap_pages.xml</loc>
        <lastmod>(now)</lastmod>
    </sitemap>
    <sitemap>
        <loc>https://mywebsite.com/sitemap/sitemap_posts.xml</loc>
        <lastmod>(now)</lastmod>
    </sitemap>
    ...
</sitemapindex>
```

The generated XML sitemap will be stored in the path /**sitemap**. Use this method to generate it:

```php
Sitemap::generate([
    'pages' => [
        'https://...',
        'https://...',
        ...
    ],
    'posts' => [
        'https://...',
        'https://...',
        ...
    ]
]);
```

This will generate a XML file for each category (pages, posts, etc). Then, the URL to your sitemap will be: **https://mysite.com/sitemap/sitemap\_index.xml**. There, there will be a file for each category (sitemap\_pages.xml, etc).
