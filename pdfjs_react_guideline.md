# Guideline of integrating pdf.js into React.js

1. install pdfjs dependency

```shell
yarn add pdfjs-dist
```

2. declare pdfjsLib from node_modules

```js
import pdfjsLib from 'pdfjs-dist/webpack';
```

3. load pdf in componentDidMount 

```js
componentDidMount() {
	let loadingTask = pdfjsLib.getDocument(this.props.url);
	loadingTask.promise.then((doc) => {
	  console.log(`Document ${this.props.url} loaded ${doc.numPages} page(s)`);
	  this.viewer.setState({
	    doc,
	  });
	}, (reason) => {
	  console.error(`Error during ${this.props.url} loading: ${reason}`);
	});
}
```

4. set loaded documents as state of component 
```js
let loadingTask = pdfjsLib.getDocument(this.props.url);
	loadingTask.promise.then((doc) => {
		console.log(`Document ${this.props.url} loaded ${doc.numPages} page(s)`);
	this.viewer.setState({
		doc,
	});
}, (reason) => {
	console.error(`Error during ${this.props.url} loading: ${reason}`);
});

```

# Components

- Viewer.js: display PDF
- Toolbar.js: Zoom-in and Zoom-out

# Reference 

https://github.com/yurydelendik/pdfjs-react

