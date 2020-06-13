---
layout: post
title: "Configuring Tailwind CSS"
author: Pranay Aryal
tags: ["CSS"]
image: img/testimg1.jpg
date: "2020-06-06T23:46:37.121Z"
draft: false
---

👋 Hi, this is how you can add tailwind css to your create-react-app 

```bash
npm install --save tailwindcss postcss-cli autoprefixer concurrently
```

Then go to your `package.json` file and add this

```json
  "scripts": {
    "tailwind": "postcss src/tailwind.css -o public/App.css",
    "start": "concurrently \"npm run tailwind" \"react-scripts start""
  }

```

Then go to your `src/` directory and create a file called `tailwind.css` and add this

```css
@tailwind base;

@tailwind components;

@tailwind utilities;
```

This will automatically inject the baseline css into your App.css file

Then run 
```bash
npm run start
```

You should see the basic tailwind css classes and normalization of css in `App.css` file

You should be good to go.