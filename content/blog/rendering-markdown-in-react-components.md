+++
date = 2020-08-21T23:00:00Z
description = "How to render markdown inside of a React component"
image = ""
title = "Rendering Markdown in React Components"

+++
For this guide we are going to be using Remark to render markdown.

Start by installing `remark` and `remark-html` using

```
npm install remark remark-html --save
```

The function `remark` is async so can't simply be called to edit the text. To solve this issue, we will create a state `defin` with

```js
const [defin, setDefin] = useState("Definition");
```

The resulting HTML from the Markdown is generated with

```js
remark()
	.use(html)
	.process(props.children, function(err,file){
  		setDefin(file);
});
```

Note here that the text to transform is `props.children`, change it to whatever is suitable for your usecase.

This might look like enough, just pass `defin` to your return and you're done. Sadly when you change a state, the component is rerendered. In that rerendering, the state is set again and you end up in an infinite loop. 

To solve this, wrap the above function in an if statement that checks if defin has been changed, simply:

```js
if(defin==="Definition"){
 // Code here
}
```

Finally, to render the resulting HTML, use `dangerouslySetInnerHTML` like:

```js
<div dangerouslySetInnerHTML={{ __html: defin }} />
```

