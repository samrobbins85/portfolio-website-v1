+++
categories = []
coders = []
date = 2020-07-10T23:00:00Z
description = "How to integrate MDX into a Next.js site"
github = []
image = ""
tech = []
title = "Expanding the Next.js blog example to use MDX"
type = ""

+++
I've recently been learning Next.js, and in this process I followed the excellent introduction tutorial you can find [here](https://nextjs.org/learn/basics/create-nextjs-app). This guides you through the creation of a Next.js site and how to parse markdown using Remark. Remark is a fantastic tool for parsing markdown, but for my project I want to use the superset of markdown, [MDX](https://mdxjs.com/). This makes it easier to add custom components as you can write JSX in your markdown.

Next.js does have a plugin for MDX that transforms every MDX page, so that when you visit it, you will see it rendered as HTML. However, I couldn't get this working for the use case here where you use `fs` to read in the file, as I believe that `fs` runs before the MDX conversion, but I'm not sure.

I then turned to the MDX documentation and found exactly what I was looking for in the "Getting started" page [here](https://mdxjs.com/getting-started#do-it-yourself), a function that takes in MDX and gives out markdown:

```js
const babel = require('@babel/core')
const React = require('react')
const {renderToStaticMarkup} = require('react-dom/server')
const mdx = require('@mdx-js/mdx')
const {MDXProvider, mdx: createElement} = require('@mdx-js/react')
const transform = code =>
  babel.transform(code, {
    plugins: [
      '@babel/plugin-transform-react-jsx',
      '@babel/plugin-proposal-object-rest-spread'
    ]
  }).code
const renderWithReact = async mdxCode => {
  const jsx = await mdx(mdxCode, {skipExport: true})
  const code = transform(jsx)
  const scope = {mdx: createElement}
  const fn = new Function(
    'React',
    ...Object.keys(scope),
    `${code}; return React.createElement(MDXContent)`
  )
  const element = fn(React, ...Object.values(scope))
  const components = {
    h1: ({children}) =>
      React.createElement('h1', {style: {color: 'tomato'}}, children)
  }
  const elementWithProvider = React.createElement(
    MDXProvider,
    {components},
    element
  )
  return renderToStaticMarkup(elementWithProvider)
}
```

You can just copy this code straight into the `posts.js` file created during the tutorial, replace the following lines in the `getPostData` function

```js
const processedContent = await remark()
    .use(html)
    .process(matterResult.content)
  const contentHtml = processedContent.toString()
```

with

```js
const contentHtml = await renderWithReact(matterResult.content);
```

and everything should "just work".

### Plugins

One of the nice features of MDX is that underneath is uses Remark to transform the markdown. This means that you can use the large ecosystem of Remark plugins. The example I will use is the remark-emoji plugin, which converts shortcodes for emoji like :wave: to the actual emoji 👋.

First install the `remark-emoji` plugin from npm with
```sh
npm install --save remark-emoji
```

Then import this into your project by adding

```js
import emoji from "remark-emoji";
```

at the top of your file, then in the line in the function used earlier that defines `jsx` that looks like:

```js
const jsx = await mdx(mdxCode, {skipExport: true})
```

replace it with

```js
const jsx = await mdx(mdxCode, { skipExport: true, remarkPlugins: [emoji] });
```

and the plugin will work when you refresh the page.