# webcomp-starter-kit
A dev-ready bundler and packager to create Web-Components with:
- ESNext transpiled by Babel
- HTML templates loaded from *.html file into your JS
- Sass styles loaded to your JS
- The spec v1 of ShadowDom and CustomElement

## Disclaimer
As [HTML Import](https://developer.mozilla.org/en-US/docs/Web/Web_Components/HTML_Imports) is still not well implemented in browsers ([and will perhaps never be...](https://hacks.mozilla.org/2015/06/the-state-of-web-components)), this starter kit doesn't use this API. Instead, it's the JavaScript bundle that has to be loaded in the page to manage the WebComp.
For the sack of separation of concern, at dev step, we still have the html and the CSS (SCSS) files, but they are loaded in the JS by Webpack.

## Polyfill
To be supported crossbrowser, you'll need some polyfills that are commented out by default in the index.html file.
Just remove the comments to use the polyfill in dev mode.
If you need the polyfill for your application, you'll have to insert it manually with your other scripts.

- [ShadyDOM](https://github.com/webcomponents/shadydom) : ShadowDOM V1 shim
- [document-register-element](https://github.com/WebReflection/document-register-element) : A stand-alone working lightweight version of the W3C Custom Elements specification
- [custom-elements](https://github.com/webcomponents/custom-elements) : is still a work in progress but will be the official custom-element polyfill

Specify the extended tagname in the definition of the custom element like

```customElements.define('my-component', MyComponent, {extends: 'input'});```

## Development

### Steps to create your own WebComponent
1. Clone this repository
1. Change the git origin repo to your own
1. Adapt ```package.json``` according to your WebComponent
1. Rename the class in the ```scripts/component.js```
1. Adapt the ```CustomElements.define``` in the ```scripts/component.js```
1. Write the unit tests in the test folder
1. Happy coding

### Extending HTMLElement VS extending specific Elements
The default code is oriented for a HTMLElement extension. This the case when you don't need to extend a specific existing component, but just want to create your custom one.
In the case you want to extend a specific HTMLElement like HTMLButtonElement, HTMLInputElement,... you'll need to modify the ```scripts/component.js``` with the following changes :

**Select the element to extend**

Change the inherited member to your own like

```export class MyComponent extends HTMLInputElement {```

**Define the extended tagname**

Specify the extended tagname in the definition of the custom element like

```customElements.define('my-component', MyComponent, {extends: 'input'});```



### Using third party CSS
If you want to add a third party style library like let's say [Twitter Bootstrap](https://getbootstrap.com/), you can do so by using webpack imports.

```@import "~bootstrap/dist/css/bootstrap";```

See this [Webpack documentation](https://github.com/webpack-contrib/sass-loader#imports)

### Running tests
The test use the [web-component-tester](https://github.com/Polymer/tools/tree/master/packages/web-component-tester) created by the Polymer team.
It needs to have a html file in the ```test``` folder where the component is created with all the scripts needed.

Once you're done, run  ```npm test``` which will launch the wct runner. The ```hook configure``` step will probably take a while but then you should get a result in the console.

For more info about the UT, refer to :
https://bendyworks.com/blog/native-web-components
https://github.com/pearlbea/mini-form/tree/step-1
https://github.com/Polymer/tools/tree/master/packages/web-component-tester