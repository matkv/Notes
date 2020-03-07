# Styling in Gatsby

## Global styles

The most common global styling option is using a global `.css` stylesheet.

We can create a `global.css` file, in `src/styles`:

```css
html {
  background-color: lavenderblush;
}
```

We then include the css file in a file called `gatsby-browser.js`. This is a file that Gatsby uses to build the site if it exists.

The `gatsby-browser.js` file needs to be in the root directory of your gatsby page.

```
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
├── gatsby-browser.js
```

We include the css in the gatsby-browser file:

```js
import "./src/styles/global.css";
```

And now the background of the site should have the new color.

There are other ways to style the Gatsby site, such as **modularizing CSS**.

## CSS Modules

A CSS module is a css file in which all class names and animation names are scoped locally by default.

This allows us to write css normally but with a lot more safety, because the tool automatically generates unique class names so we don't have to worry about name collisons.

### Creating a css module

We create a new folder `src/components` called `container.js`.

```js
import React from "react";
import containerStyles from "./container.module.css";
export default ({ children }) => (
  <div className={containerStyles.container}>{children}</div>
);
```

In the same directory, we create a `container.module.css` file:

```css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

The file ends with `module.css`. This tells Gatsby that this file should be processed as a CSS module rather than plain CSS.

Now let's use this module in a page. We create a new page component called `about-css-modules.js`.

```js
import React from "react";
import Container from "../components/container";
export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
);
```

Let's say we have a css file with multiple classes:

```css
.user {
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
}
.user:last-child {
  margin-bottom: 0;
}
.avatar {
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
}

.description {
  flex: 1;
  margin-left: 18px;
  padding: 12px;
}

.username {
  margin: 0 0 12px 0;
  padding: 0;
}

.excerpt {
  margin: 0;
}
```

Using this file as a module will guarantee that Gatsby will create unique class names for each of the classes in the file - they are guaranteed to be unique across the site.

Here's an example of using multiple classes inside a `<User />` component. In this example, the component is created inline, directly in this file.

```javascript
import React from "react"
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

const User = props => (
    <div className={styles.user}>
      <img src={props.avatar} className={styles.avatar} alt="" />
      <div className={styles.description}>
        <h2 className={styles.username}>{props.username}</h2>
        <p className={styles.excerpt}>{props.excerpt}</p>
      </div>
    </div>
  )

export default () => (

<Container>
  <h1>About CSS Modules</h1>
  <p>CSS Modules are cool</p>
  <User
    username="Jane Doe"
    avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
    excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
  />
  <User
    username="Bob Smith"
    avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
    excerpt="I'm Bob Smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
  />
</Container>

)
```

Stopped at [Part Three](https://www.gatsbyjs.org/tutorial/part-three/).
