---
title: "Layouts"
permalink: /docs/layouts/
excerpt: "Descriptions and samples of all layouts included with the theme and how to best use them."
single_layout_gallery:
  - image_path: /assets/images/mm-layout-single-header.png
    alt: "single layout with header example"
  - image_path: /assets/images/mm-layout-single-meta.png
    alt: "single layout with comments and related posts"
last_modified_at: 2017-11-28T08:42:54-05:00
toc: true
toc_label: "Included Layouts"
toc_icon: "columns"
---

The bread and butter of any theme. Below you'll find the layouts included with Minimal Mistakes, what they look like and the type of content they've been built for.

## Default Layout

The base layout all other layouts inherit from. There's not much to this layout apart from pulling in several `_includes`:

* `<head>` elements
* masthead navigation links
* {% raw %}`{{ content }}`{% endraw %}
* page footer
* scripts

**Note:** You won't ever assign this layout directly to a post or page. Instead all other layouts will build off of it by setting `layout: default` in their YAML Front Matter.
{: .notice--warning}

### Layout Based and User-Defined Classes

Class names corresponding to each layout are automatically added to the `<body>` element eg. `<body class="layout--single">`.

| layout           | class name                  |
| ---------------- | --------------------------- |
| archive          | `.layout--archive`          |
| archive-taxonomy | `.layout--archive-taxonomy` |
| search           | `.layout--search`           |
| single           | `.layout--single`           |
| splash           | `.layout--splash`           |
| home             | `.layout--home`             |

Using YAML Front Matter you can also assign custom classes to target with CSS or JavaScript. Perfect for "art directed" posts or adding custom styles to specific pages.

Example:

```yaml
---
layout: splash
classes:
  - landing
  - dark-theme
---
```

Outputs:

```html
<body class="layout--splash landing dark-theme">
```

## Compress Layout

A Jekyll layout that compresses HTML in pure Liquid. To enable add `layout: compress` to `_layouts/default.html`.

**Note:** Has been known to mangle markup and break JavaScript... especially if inline `// comments` are present. For this reason it has been disabled by default.
{: .notice--danger}

* [Documentation](http://jch.penibelst.de/)

## Single Layout

The layout you'll likely use the most --- sidebar and main content combo.

**Includes:**

* Optional header image with caption
* Optional header overlay (solid color/image) + text and optional "call to action" button
* Optional social sharing links module
* Optional comments module
* Optional related posts module

{% include gallery id="single_layout_gallery" caption="Image header and meta info examples for `single` layout" %}

Assign with `layout: single`, or better yet apply as a [Front Matter default]({{ "/docs/configuration/#front-matter-defaults" | absolute_url }}) in `_config.yml`.

### Table of Contents

Auto-generated table of contents list for your posts and pages can be enabled by adding `toc: true` to the YAML Front Matter.

![table of contents example]({{ "/assets/images/mm-toc-helper-example.jpg" | absolute_url }})

| Parameter   | Required | Description | Default |
| ---------   | -------- | ----------- | ------- |
| **toc**     | Optional | Show table of contents. (boolean) | `false` |
| **toc_label** | Optional | Table of contents title. (string) | `toc_label` in UI Text data file. |
| **toc_icon**  | Optional | Table of contents icon, displays before the title. (string) | [Font Awesome](https://fortawesome.github.io/Font-Awesome/icons/) <i class="fa fa-file-text"></i> **file-text** icon. Any other FA icon can be used instead. |

**TOC example with custom title and icon**

```yaml
---
toc: true
toc_label: "My Table of Contents"
toc_icon: "gear"
---
```

## Archive Layout

Essentially the same as `single` with markup adjustments and some modules removed.

**Includes:**

* Optional header image with caption
* Optional header overlay (solid color/image) + text and optional "call to action" button
* List and grid views

<figure>
  <img src="{{ '/assets/images/mm-layout-archive.png' | absolute_url }}" alt="archive layout example">
  <figcaption>List view example.</figcaption>
</figure>

Below are sample archive pages you can easily drop into your project, taking care to rename `permalink`, `title`, or the filename to fit your site. Each is 100% compatible with GitHub Pages.

* [All Posts Grouped by Category -- List View][posts-categories]
* [All Posts Grouped by Tag -- List View][posts-tags]
* [All Posts Grouped by Year -- List View][posts-year]
* [All Posts Grouped by Collection -- List View][posts-collection]
* [Portfolio Collection -- Grid View][portfolio-collection]

[posts-categories]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/category-archive.html
[posts-tags]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/tag-archive.html
[posts-year]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/year-archive.html
[posts-collection]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/collection-archive.html
[portfolio-collection]: https://github.com/{{ site.repository }}/blob/master/docs/_pages/portfolio-archive.html

Post and page excerpts are auto-generated by Jekyll which grabs the first paragraph of text. To override this text with something more specific use the following YAML Front Matter:

```yaml
excerpt: "A unique line of text to describe this post that will display in an archive listing and meta description with SEO benefits."
```

### Grid View

Adding `type=grid` to the `archive-single` helper will display archive posts in a 4 column grid. For example to create an archive displaying all documents in the portfolio collection:

**Step 1:** Create a portfolio archive page (eg. `_pages/portfolio-archive.html`) with the following YAML Front Matter:

```yaml
---
layout: archive
title: "Portfolio"
permalink: /portfolio/
author_profile: false
---
```

**Step 2:** Loop over all documents in the portfolio collection and output in a grid:

```html
{% raw %}<div class="grid__wrapper">
  {% for post in site.portfolio %}
    {% include archive-single.html type="grid" %}
  {% endfor %}{% endraw %}
</div>
```

To produce something like this:

<figure>
  <img src="{{ '/assets/images/mm-archive-grid-view-example.jpg' | absolute_url }}" alt="archive grid view example">
  <figcaption>Grid view example.</figcaption>
</figure>

Teaser images are assigned similar to header images using the following YAML Front Matter:

```yaml
header:
  teaser: path-to-teaser-image.jpg
```

**Note:** More information on using this `_include` can be found under [**Helpers**]({{ "/docs/helpers/" | absolute_url }}).
{: .notice--info}

### Taxonomy Archive

If you have the luxury of using Jekyll plugins, the creation of category and tag archives is greatly simplified. Simply enable support for the [`jekyll-archives`](https://github.com/jekyll/jekyll-archives) plugin with a few `_config.yml` settings as noted in the [**Configuration**]({{ "/docs/configuration/#archive-settings" | absolute_url }}) section and you're good to go.

![archive taxonomy layout example]({{ "/assets/images/mm-layout-archive-taxonomy.png" | absolute_url }})

If you're not using the `jekyll-archives` plugin then you need to create archive pages yourself. Sample taxonomy archives can be found by grabbing the HTML sources below and adding to your site.

| Name                 | HTML Source |
| -------------------- | --- |
| [Categories Archive](https://mmistakes.github.io/minimal-mistakes/categories/) | [category-archive.html](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/category-archive.html) |
| [Tags Archive](https://mmistakes.github.io/minimal-mistakes/tags/) | [tag-archive.html](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/tag-archive.html) |

The **Tags Archive** page that responds to urls such as `/tags/#tips` looks something like this:

```html
---
layout: archive
permalink: /tags/
title: "Posts by Tag"
author_profile: true
---

{% raw %}{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}{% endraw %}
```

## Home Page Layout

A derivative archive page layout to be used as a simple home page. It is built to show a paginated list of recent posts based off of the [pagination settings]({{ "/docs/configuration/#paginate" | absolute_url }}) in `_config.yml`.

<figure>
  <img src="{{ '/assets/images/mm-home-post-pagination-example.jpg' | absolute_url }}" alt="paginated home page example">
  <figcaption>Example of a paginated home page showing 5 recent posts.</figcaption>
</figure>

To use create `index.html` at the root of your project and add the following YAML Front Matter:

```yaml
---
layout: home
---
```

Then configure pagination in `_config.yml`.

```yaml
paginate: 5 # amount of posts to show
paginate_path: /page:num/
```

If you'd rather have a paginated page of posts reside in a subfolder instead of acting as your homepage make the following adjustments.

Create `index.html` in the location you'd like. For example if I wanted it to live at **/blog** I'd create `/blog/index.html` with `layout: home` in its YAML Front Matter.

Then adjust the `paginate_path` in **_config.yml** to match.

```yaml
paginate_path: /blog/page:num
``` 

**Note:** Jekyll can only paginate a single `index.html` file. If you'd like to paginate more pages (e.g. category indexes) you'll need the help of a custom plugin. For more pagination related settings check the [**Configuration**]({{ "/docs/configuration/#paginate" | absolute_url }}) section.
{: .notice--info}

## Splash Page Layout

For full-width landing pages that need a little something extra add `layout: splash` to the YAML Front Matter.

**Includes:**

* Optional header image with caption
* Optional header overlay (solid color/image) + text and optional "call to action" button
* Feature blocks (`left`, `center`, and `right` alignment options)

![splash page layout example]({{ "/assets/images/mm-layout-splash.png" | absolute_url }})

Feature blocks can be assigned and aligned to the `left`, `right`, or `center` with a sprinkling of YAML. For full details on how to use the `feature_row` helper check the [**Content**]({{ "/docs/helpers/" | absolute_url }}) section or review a [sample splash page](https://github.com/{{ site.repository }}/blob/master/docs/_pages/splash-page.md).

## Search Page Layout

A page with a search form. Add `layout: search` to the YAML Front Matter similar to [this example](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/search.md) on the demo site.

![search page layout example]({{ "/assets/images/search-layout-example.png" | absolute_url }})

### Exclusions

If you would like to exclude specific pages/posts from the search index set the search flag to `false` in the YAML Front Matter for the page/post.

```yaml
search: false
```

**ProTip:** Add a link to this page in the masthead navigation.
{: .notice--info}

---

## Headers

To add some visual punch to a post or page, a large full-width header image can be included.

Be sure to resize your header images. `~1280px` is a good width if you aren't [responsively serving up images](http://alistapart.com/article/responsive-images-in-practice). Through the magic of CSS they will scale up or down to fill the container. If you go with something too small it will look like garbage when upscaled, and something too large will hurt performance.

**Please Note:** Paths for image headers, overlays, teasers, [galleries]({{ "/docs/helpers/#gallery" | absolute_url }}), and [feature rows]({{ "/docs/helpers/#feature-row" | absolute_url }}) have changed and require a full path. Instead of just `image: filename.jpg` you'll need to use the full path eg: `image: /assets/images/filename.jpg`. The preferred location is now `/assets/images/`, but can be placed elsewhere or external hosted. This all applies for image references in `_config.yml` and `author.yml` as well.
{: .notice--danger}

![single layout header image example]({{ "/assets/images/mm-single-header-example.jpg" | absolute_url }})

Place your images in the `/assets/images/` folder and add the following YAML Front Matter:

```yaml
header:
  image: /assets/images/image-filename.jpg
```

For externally hosted images include the full image path instead of just the filename:

```yaml
header:
  image: http://some-site.com/assets/images/image.jpg
```

To provide a custom alt tag for screen readers:

```yaml
header:
  image: /assets/images/unsplash-image-1.jpg
  image_description: "A description of the image"
```

To include a caption or attribution for the image:

```yaml
header:
  image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
```

**ProTip:** Captions written in Markdown are supported, so feel free to add links, or style text. Just be sure to wrap it in quotes.
{: .notice--info}

### Header Overlay

To overlay text on top of a header image you have a few more options:

| Name               | Description | Default |
| ----               | ----------- | ------- |
| **overlay_image**  | Header image you'd like to overlay. Same rules as `header.image` from above. | |
| **overlay_filter** | Color/opacity to overlay on top of the header image eg: `0.5` or `rgba(255, 0, 0, 0.5)`. |
| **excerpt**        | Auto-generated page excerpt is added to the overlay text or can be overridden. | |
| **cta_label**      | Call to action button text label. | `more_label` in UI Text data file |
| **cta_url**        | Call to action button URL. | |

With this YAML Front Matter:

```yaml
excerpt: "This post should display a **header with an overlay image**, if the theme supports it."
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  cta_label: "More Info"
  cta_url: "https://unsplash.com"
```

You'd get a header image overlaid with text and a call to action button like this:

![single layout header overlay example]({{ "/assets/images/mm-single-header-overlay-example.jpg" | absolute_url }})

You also have the option of specifying a solid background-color to use instead of an image.

![single layout header overlay with background fill]({{ "/assets/images/mm-single-header-overlay-fill-example.jpg" | absolute_url }})

```yaml
excerpt: "This post should display a **header with a solid background color**, if the theme supports it."
header:
  overlay_color: "#333"
```

You can also specifying the opacity (between `0` and `1`) of a black overlay like so:

![transparent black overlay]({{ "/assets/images/mm-header-overlay-black-filter.jpg" | absolute_url }})

```yaml
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  cta_label: "More Info"
  cta_url: "https://unsplash.com"
```

Or if you want to do more fancy things, go full rgba:

![transparent red overlay]({{ "/assets/images/mm-header-overlay-red-filter.jpg" | absolute_url }})

```yaml
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: rgba(255, 0, 0, 0.5)
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  cta_label: "More Info"
  cta_url: "https://unsplash.com"
```

### OpenGraph & Twitter Card Images

By default the large page header or overlay images are used for sharing previews. If you'd like to set this image to something else use `page.header.og_image` like:

```yaml
header:
  image: /assets/images/your-page-image.jpg
  og_image: /assets/images/your-og-image.jpg
```

**ProTip:** `og_image` is useful for setting OpenGraph images on pages that don't have a header or overlay image.
{: .notice--info}

---

## Sidebars

The space to the left of a page's main content is blank by default, but has the ability to show an author profile (name, short biography, social media links), custom content, or both.

### Author Profile

Add `author_profile: true` to a post or page's YAML Front Matter.

![single layout example]({{ "/assets/images/mm-layout-single.png" | absolute_url }})

Better yet, enable it with Front Matter Defaults set in `_config.yml`.

```yaml
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      author_profile: true
```

**Note:** To disable the author sidebar profile for a specific post or page, add `author_profile: false` to the YAML Front Matter instead.
{: .notice--warning}

The theme comes pre-built with a selection of links for the most common social media networks. These are all optional and can be [assigned in `_config.yml`]({{ "/docs/configuration/" | absolute_url }}).

To add more links you'll need to crack open [`_includes/author-profile-custom-links.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/author-profile-custom-links.html) and add the appropriate `<li>` markup shown below. 

**Please note:** Links added here will appear after the ones in [`_includes/author-profile.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/author-profile.html). If you'd like to change the order of appearance you'll need to edit that file directly.
{: .notice--info}

#### Social network link example

```html
<li>
  <a href="https://whatever-social-network.com/username">
    <i class="fa fa-fw" aria-hidden="true"></i> Awesome Social Network
  </a>
</li>
```

To add a new link you'll need three things:

1. Destination URL
2. [Font Awesome icon](http://fontawesome.io/icons/) (`fa-` class)
3. Label for the link

It's up to you if you want to wrap it in a `{% raw %}{% if %} ... {% endif %}{% endraw %}`conditional and add a variable to `_config.yml`. If you don't plan to change it then hard-coding the string is perfectly acceptable.

Let's run through how you'd add a new link that points to a Reddit profile. Starting with the three things from above:

1. `https://www.reddit.com/user/username`
2. [`fa-reddit`](http://fontawesome.io/icon/reddit/)
3. `Reddit`

And plug them into the appropriate locations:

```html
<li>
  <a href="[1]">
    <i class="fa fa-fw [2]" aria-hidden="true"></i> [3]
  </a>
</li>
```

To end up with:

```html
<li>
  <a href="https://www.reddit.com/user/username">
    <i class="fa fa-fw fa-reddit" aria-hidden="true"></i> Reddit
  </a>
</li>
```

![Reddit link in author profile]({{ "/assets/images/mm-author-profile-reddit-gs.png" | absolute_url }})

To add a touch of color to the default black (`#000`) icon a few more steps are necessary.

Start by copying [`_utilities.scss`](https://github.com/mmistakes/minimal-mistakes/blob/master/_sass/minimal-mistakes/_utilities.scss) `<site root>/_sass`. Open it up to the icon section (it's near the bottom) and nest a new class beneath `.social-icons` that matches the one used to declare the Font Awesome icon. In our case `.fa-reddit`.

Simply add a `color` declaration and the corresponding hex code.

```scss
.social-icons {
  
  .fa-reddit {
    color: #ff4500;
  }
}
``` 

![Reddit link in author profile with color]({{ "/assets/images/mm-author-profile-reddit-color.png" | absolute_url }})

**ProTip:** For bonus points you can add it as a Sass `$variable` that you set in [`_variables.scss`](https://github.com/mmistakes/minimal-mistakes/blob/master/_sass/minimal-mistakes/_variables.scss) like the other ["brand" colors](http://brandcolors.net/). You'll need to add this file to `/_sass/` as well if you're using the Ruby Gem version of the theme.
{: .notice--info}

**Please please please** don't submit [pull requests]({{ "/docs/contributing/" | absolute_url }}) adding in support for "missing" social media links. I'm trying to keep things down to the minimum (hence the theme's name) and have no interest in merging such PRs :expressionless:.
{: .notice--warning}

### Custom Sidebar Content

Blocks of content can be added by using the following under `sidebar`:

| Name          | Description                                                |
| ----          | -----------                                                |
| **title**     | Title or heading.                                          |
| **image**     | Image path placed in `/images/` folder or an external URL. |
| **image_alt** | Alternate description for image.                           |
| **text**      | Text. Markdown is allowed.                                 |

Multiple blocks can also be added by following the example below:

```yaml
sidebar:
  - title: "Title"
    image: http://placehold.it/350x250
    image_alt: "image"
    text: "Some text here."
  - title: "Another Title"
    text: "More text here."
```

<figure>
  <img src="{{ '/assets/images/mm-custom-sidebar-example.jpg' | absolute_url }}" alt="custom sidebar content example">
  <figcaption>Example of custom sidebar content added as YAML Front Matter.</figcaption>
</figure>

**Note:** Custom sidebar content added to a post or page's YAML Front Matter will appear below the author profile if enabled with `author_profile: true`.
{: .notice--info}

### Custom Sidebar Navigation Menu

To create a sidebar menu[^sidebar-menu] similar to the one found in the theme's documentation pages you'll need to modify a `_data` file and some YAML Front Matter.

[^sidebar-menu]: Sidebar menu supports 1 level of nested links.

<figure>
  <img src="{{ '/assets/images/mm-custom-sidebar-nav.jpg' | absolute_url }}" alt="sidebar navigation example">
  <figcaption>Custom sidebar navigation menu example.</figcaption>
</figure>

To start, add a new key to `_data/navigation.yml`. This will be referenced later in via YAML Front Matter so keep it short and memorable. In the case of the theme's documentation menu I used `docs`.

**Sample sidebar menu links:**

```yaml 
docs:
  - title: Getting Started
    children:
      - title: "Quick-Start Guide"
        url: /docs/quick-start-guide/
      - title: "Structure"
        url: /docs/structure/
      - title: "Installation"
        url: /docs/installation/
      - title: "Upgrading"
        url: /docs/upgrading/

  - title: Customization
    children:
      - title: "Configuration"
        url: /docs/configuration/
      - title: "Navigation"
        url: /docs/navigation/
      - title: "UI Text"
        url: /docs/ui-text/
      - title: "Authors"
        url: /docs/authors/
      - title: "Layouts"
        url: /docs/layouts/

  - title: Content
    children:
      - title: "Working with Posts"
        url: /docs/posts/
      - title: "Working with Pages"
        url: /docs/pages/
      - title: "Working with Collections"
        url: /docs/collections/
      - title: "Helpers"
        url: /docs/helpers/
      - title: "Utility Classes"
        url: /docs/utility-classes/

  - title: Extras
    children:
      - title: "Stylesheets"
        url: /docs/stylesheets/
      - title: "JavaScript"
        url: /docs/javascript/
```

Now you can pull these links into any page by adding the following YAML Front Matter.

```yaml
sidebar:
  nav: "docs"
```

**Note:** `nav: "docs"` references the `docs` key in `_data/navigation.yml` so make sure they match.
{: .notice--info}

If you're adding a sidebar navigation menu to several pages the use of Front Matter Defaults is a better option. You can define them in `_config.yml` to avoid adding it to every page or post.

**Sample sidebar nav default:**

```yaml
defaults:
  # _docs
  - scope:
      path: ""
      type: docs
    values:
      sidebar:
        nav: "docs"
```

---

## Social Sharing Links

The `single` layout has an option to enable social links at the bottom of posts for sharing on Twitter, Facebook, Google+, and LinkedIn. Similar to the links found in the author sidebar, the theme ships with defaults for the most common social networks.

![default social share link buttons]({{ "/assets/images/mm-social-share-links-default.png" | absolute_url }})

To enable these links add `share: true` to a post or page's YAML Front Matter or use a [default](https://jekyllrb.com/docs/configuration/#front-matter-defaults) in your `_config.yml` to apply more globally.

If you'd like to add, remove, or change the order of these default links you can do so by editing [`_includes/social-share.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/social-share.html).

Let's say you wanted to replace the Google+ button with a Reddit one. Simply replace the HTML with the following:

```html
{% raw %}<a href="https://www.reddit.com/submit?url={{ page.url | absolute_url }}&title={{ page.title }}" class="btn" title="{{ site.data.ui-text[site.locale].share_on_label }} Reddit"><i class="fa fa-fw fa-reddit" aria-hidden="true"></i><span> Reddit</span></a>{% endraw %}
```

The important parts to change are:

1. Share point URL *eg. `https://www.reddit.com/submit?url=`
2. Link `title`
3. [Font Awesome icon](http://fontawesome.io/icons/) (`fa-` class)
4. Link label

![Reddit social share link button]({{ "/assets/images/mm-social-share-links-reddit-gs.png" | absolute_url }})

To change the color of the button use one of the built in [utility classes]({{ "/docs/utility-classes/#buttons" | absolute_url }}). Or you can create a new button class to match whatever color you want.

Under the `$social` color map in `assets/_scss/_buttons.scss` simply add a name (this will be appened to `btn--`) that matches the new button class. In our case `reddit` ~> `.btn--reddit`.

```scss
$social:
(facebook, $facebook-color),
(twitter, $twitter-color),
(google-plus, $google-plus-color),
(linkedin, $linkedin-color);
(reddit, #ff4500;)
```

**ProTip:** For bonus points you can add it as a Sass `$variable` that you set in `_variables.scss` like the other ["brand" colors](http://brandcolors.net/).
{: .notice--info}

Add the new `.btn--reddit` class to the `<a>` element from earlier, [compile `main.css`]({{ "/docs/stylesheets/" | absolute_url }}) and away you go.

```html
{% raw %}<a href="https://www.reddit.com/submit?url={{ page.url | absolute_url }}&title={{ page.title }}" class="btn btn--reddit" title="{{ site.data.ui-text[site.locale].share_on_label }} Reddit"><i class="fa fa-fw fa-reddit" aria-hidden="true"></i><span> Reddit</span></a>{% endraw %}
```

![Reddit social share link button]({{ "/assets/images/mm-social-share-links-reddit-color.png" | absolute_url }})
