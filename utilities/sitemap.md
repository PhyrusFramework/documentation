---
description: Generate a Sitemap XML file for your website.
---

# Sitemap

The **Sitemap** class can generate a XML Sitemap for your website.

Specifically, the sitemap is composed of an **index** file that references other XML files where the URLs are listed.

Example:

```
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

The sitemap will be generated in the path /**sitemap**. Use this method to generate it:

```
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

Then, the URL to your sitemap will be: **https://mysite.com/sitemap/sitemap\_index.xml**.
