# Gatsby.js

Creating a new site:

```bash
gatsby new site-name
```

Then switch into the new created folder and run ```gatsby develop``` to start a live server that shows changes to the site in real time.

By using a syntax extension of JavaScript for React called **JSX**, we can use HTML code directly in a JavaScript function:

```javascript
import React from "react"
export default () => <div>Hello world!</div>
```

## Components

A component is a building block for the site, a self contained piece of code that describes a section of UI.

```
<PrimaryButton>Click me</PrimaryButton>
```

### Page components

Any component that is defined in ```src/pages/*.js``` will automatically become a page.

For example, an "about" page in ```src/pages/about.js```:

```js
import React from "react"
export default () => (
  <div style={{ color: `teal` }}>
    <h1>About Gatsby</h1>
    <p>This is the about page.</p>
  </div>
)
```

The page is now accessible at ```/about```.

### Sub components

We can break the UI into reusable pieces by using sub-components, for example creating a header component and using it in multiple files.

The header file in ```src/components/header.js```:

```js
import React from "react"
export default () => <h1>This is a header.</h1>
```

Now we can use this component in other files, for example our about.js :

```js
import React from "react"
import Header from "../components/header"
export default () => (
  <div style={{ color: `teal` }}>
    <Header />
    <p>This is the about page.</p>
  </div>
)
```

However we don't want the header to say the same words on every page. We can make it possible to modify it specifically for each page by using a property.

```js
import React from "react"
export default props => <h1>{props.headerText}</h1>
```

No we can set a custom text directly:

```js
import React from "react"
import Header from "../components/header"
export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="About Gatsby" />
    <p>Such wow. Very React.</p>
  </div>
)
```

```props``` are properties supplied to React components. We can use them to make our components dynamic by supplying them with different data.

### Layout components

Layout components are used for sections of a site that should be shared across multiple pages, for example a shared header and footer, a sidebar or a navigation menu.

## Linking between pages

We use the ```<Link />``` component to link to different pages.

```js
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"
export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Contact</Link>
    <Header headerText="Hello Gatsby!" />
    <p>What a world.</p>
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

This would link to a ```src/pages/contact.js``` page.

## Building & publishing the site

By using the command ```gatsby build``` command, Gatsby will generate ready to use files in the ```public``` directory. These files can now be used on any static site host.