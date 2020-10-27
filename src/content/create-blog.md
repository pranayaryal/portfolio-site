---
layout: post
title: How to Create a Blog Like This
image: img/computer.jpg
author: Pranay Aryal
date: 2019-08-09T10:00:00.000Z
tags:
  - Blogging
---

This blog was created using <a href="https://www.gatsbyjs.org/" target="_blank">Gatsby</a>. Gatsby is a static-site generator.


First make sure you have gatsby installed.
```shell
npm install -g gatsby-cli
```

Then, head over <a href="https://www.gatsbyjs.org/docs/recipes/" target="_blank">here</a>

From the left panel, choose "Using a Starter" and click that and then click 'Starter Library' which will take you 
<a href="https://www.gatsbyjs.org/starters/?v=2" target="_blank">here</a>

For this particular blog style scroll down till you see 'gatsby-casper'.

You can click on it and see the demo.

To download into your machine. Type:
```shell
gatsby new {your-project-name} {link-to-starter}
```

'your-project-nake' could be any name you choose.

The 'link-to-starter' for this blog is <a href="https://github.com/scttcper/gatsby-casper" target="_blank">here</a>

Once it is downloaded, open it in a text editor.

Head over to `website-config.ts` file and scroll down

```ts
const config: WebsiteConfig = {
  title: "",
  description: 'Blog Posts',
  coverImage: 'img/blog-cover.jpg',
  // logo: 'img/ghost-logo.png',
  logo: 'img/self.jpg',
  lang: 'en',
  siteUrl: 'https://pranaysite.netlify.com',
  facebook: '',
  twitter: 'https://twitter.com/pranayaryal',
  showSubscribe: false,
  mailchimpAction: 'https://twitter.us19.list-manage.com/subscribe/post?u=a89b6987ac248c81b0b7f3a0f&amp;id=7d777b7d75',
  mailchimpName: 'b_a89b6987ac248c81b0b7f3a0f_7d777b7d75',
  mailchimpEmailFieldName: 'MERGE0',
  googleSiteVerification: 'GoogleCode',
  footer: '',
};
```

Change the above for your own website.

Go to `author.yaml` file and add yourself.

It should look like this
```yml
- id: Pranay Aryal
  avatar: avatars/self-resized.jpg
  bio: Software Developer
  twitter: pranayaryal
  facebook:
  website: https://pranaysite.netlify.com
  location: In a plane
```
Add your avatar image in the `/content/avatars/` folder.

Make sure the image is 400 x 400 pixels. You can resize your image <a href="https://resizeimage.net/" target="_blank">here</a>

Add another .md file in the `contents/` folder and format it with markdown. The route will be automatically added.

Use your new author id to create posts

You should be good to go.

You can change the number of posts in each page by gong to `gatsby-node.js`

Change this
```js
  // Create paginated index
  const postsPerPage = 8;
  const numPages = Math.ceil(posts.length / postsPerPage);
```

Edit the `postsPerPage` variable

If you want to change which is your favorite tag to link, head to `SiteNav.tsx`

Within the `<SiteNavLeft>` tag you will find this

```html
<li role="menuitem">
  <Link to="/tags/python/">Python</Link>
</li>
```

Change what follows after /tags and also within that <Link>

You might want to host this on <a href='https://netlify.com' target='_blank'>Netlify</a> but that is going to be a separate blog by itself 😄

I can be found in <a href="https://twitter.com/pranayaryal" target="__blank">twitter</a>