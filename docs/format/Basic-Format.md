---
layout: default
title: Basic format
nav_exclude: false
has_children: false
parent: format
# grand_parent:
# has_toc: false
search_exclude: false # ALWAYS SET TO FALSE!!!
last_modified_date: 2024-12-10
---
# Main title
{: .no_toc }

{% include toc.md %}

## Secondary title
Information goes here. All stuff are written in code md files.

## Adding images
Ensure that the images are added in the "/assets/img/" folder for images, and create a subfolder for each specific topic for easier management.

All Markdown images render centered in the main content area by default, so standard image syntax is enough for most pages.

Use descriptive alt text inside the image syntax for accessibility:
```
![Description of the image](../../../assets/img/<PATH-TO-IMAGE>)
```

If you want visible text under the image, use a caption with HTML:
```
<figure>
	<img src="../../../assets/img/<PATH-TO-IMAGE>" alt="Description of the image">
	<figcaption>Caption text goes here</figcaption>
</figure>
```

A full example would look like this:
```
<figure>
	<img src="../../../assets/img/Blog/Homelab/nec-versa-e6500-series-laptop.jpg" alt="NEC Versa E6500 laptop">
	<figcaption>My first laptop back in 2007.</figcaption>
</figure>
```

When adding images, always ensure to add `../../../` before images as I have not yet CNAMED my wiki yet. An example image format will therefore be:
```
![Description of the image](../../../assets/img/<PATH-TO-IMAGE>)
```

## Callouts
There are numerous callouts and functions that are present. Use the following:

### Info blocks:
```
{: .info }
> This is an info block.
```

{: .info }
> This is an info block.

### Note blocks:
```
{: .note }
> Note block is note block.
```

{: .note }
> Note block is note block.

### Important blocks:
```
{: .important }
> *Important blocks are always italicized* as necessary.
```

{: .important }
> *Important blocks are always italicized* as necessary.

### Quote blocks:
```
{: .quote }
>  "Quote blocks are always in quote blocks."
```

{: .quote }
>  "Quote blocks are always in quote blocks."

### Warning blocks:
```
{: .warning }
> *Warning blocks are always italicized*
```

{: .warning }
> *Warning blocks are always italicized*
