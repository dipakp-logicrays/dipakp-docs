# SEO Meta Tags Configuration

This documentation project includes dynamic SEO meta tags that automatically adapt to each page's content.

## What's Included

### 1. Standard SEO Meta Tags
- **Description**: Automatically uses page-specific or default description
- **Keywords**: Page-specific or default keywords
- **Author**: Page author (defaults to "Dipak Prajapati")

### 2. Open Graph (Facebook/LinkedIn) Meta Tags
- `og:type`: website
- `og:site_name`: Site title
- `og:title`: Dynamic page title
- `og:description`: Dynamic description
- `og:url`: Page URL
- `og:image`: Site logo

### 3. Twitter Card Meta Tags
- `twitter:card`: summary_large_image
- `twitter:title`: Dynamic page title
- `twitter:description`: Dynamic description
- `twitter:image`: Site logo

## How It Works

### Default Meta Tags
The following defaults are configured in `docs/conf.py`:

```python
html_context = {
    'meta_description': 'Comprehensive documentation for web development including Magento 2, PHP, Docker, Linux...',
    'meta_keywords': 'Magento 2, PHP, Docker, Linux, Web Development, Dipak Prajapati...',
}
```

### Dynamic Content
- **Title**: Automatically extracted from each page's H1 heading
- **Description**: Uses page-specific meta or falls back to default
- **URL**: Automatically generated based on page location
- **Keywords**: Page-specific or default keywords

## Adding Custom Meta Tags to Individual Pages

To add custom SEO meta tags to a specific page, add a `:meta:` field at the top of your RST file:

### Example 1: Custom Description

```rst
:meta description: Complete guide to Magento 2 installation on Ubuntu. Step-by-step tutorial for setting up Magento 2 with Nginx, PHP, and MySQL.
:meta keywords: Magento 2 Installation, Ubuntu, Nginx, PHP, MySQL, Magento Setup

Magento 2 Installation Guide
=============================

Your content here...
```

### Example 2: Multiple Meta Fields

```rst
:meta description: Learn Git branching strategies and best practices for collaborative development
:meta keywords: Git, Git Branches, Version Control, Git Workflow, Branch Management
:meta author: Dipak Prajapati

Git Branch Management
=====================

Your content here...
```

### Example 3: Long Description

```rst
:meta description: Comprehensive Docker guide covering container creation, image management, Docker Compose, networking, and production deployment strategies for web applications.
:meta keywords: Docker, Containers, Docker Compose, Microservices, DevOps, Container Orchestration

Docker Complete Guide
======================

Your content here...
```

## Meta Tag Priority

The system uses this priority order:

1. **Page-specific meta** (from `:meta:` field in RST file)
2. **Default meta** (from `conf.py`)
3. **Fallback values** (hardcoded in template)

## Testing Your Meta Tags

### 1. Build Locally
```bash
cd docs
sphinx-build -b html . _build/html
```

### 2. Check Generated HTML
```bash
# View meta tags for a specific page
cat _build/html/your-page/index.html | grep '<meta'
```

### 3. Test with Online Tools
- **Facebook Debugger**: https://developers.facebook.com/tools/debug/
- **Twitter Card Validator**: https://cards-dev.twitter.com/validator
- **LinkedIn Post Inspector**: https://www.linkedin.com/post-inspector/

## Best Practices

### Description Meta Tag
- **Length**: 150-160 characters optimal
- **Content**: Clear, concise summary of the page
- **Keywords**: Naturally include 1-2 main keywords
- **Unique**: Each page should have a unique description

### Keywords Meta Tag
- **Count**: 5-10 relevant keywords
- **Relevance**: Only include keywords actually discussed on the page
- **Format**: Comma-separated list
- **Specificity**: Mix of broad and specific terms

### Example Good vs Bad

#### Good Description
```rst
:meta description: Learn how to configure PHP 7.4 and PHP 8.1 on Ubuntu 22.04. Switch between multiple PHP versions using update-alternatives command.
```

#### Bad Description
```rst
:meta description: PHP tutorial
```

#### Good Keywords
```rst
:meta keywords: PHP 7.4, PHP 8.1, Ubuntu 22.04, Multiple PHP Versions, PHP Configuration, Switch PHP Versions
```

#### Bad Keywords
```rst
:meta keywords: php, tutorial, guide, how to, step by step, easy, simple
```

## Files Modified

1. **`docs/_templates/layout.html`**: Contains the meta tag template logic
2. **`docs/conf.py`**: Defines default meta values in `html_context`

## Verification

After deployment, verify your meta tags appear correctly:

```bash
curl -s https://dipakp-docs.readthedocs.io/ | grep '<meta'
```

Or view source in your browser and check the `<head>` section.
