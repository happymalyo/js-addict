## 📂 Dynamic Import in JavaScript

[State of JS 2023 Survey](https://survey.devographics.com/en-US/survey/state-of-js/2023/) - Features > Syntax Features > Dynamic Import.

#### What is Dynamic Import?

Dynamic import is a way to load JavaScript modules only when they are needed, instead of loading everything at once. This can make web application faster :rocket: and more efficient.

```js
import("./path-to-my-module.js");
```

Note that it looks like a function but it’s not inherit from <code>Function.prototype.</code>
Dynamic import returns a Promise so you need to handle it like you do for any Promise in your code.

#### When to Use Dynamic Import? ⏰

- When you have a large application and want to split the code into manageable chunks.
- When certain features or modules are used infrequently.
- When loading resources conditionally, such as based on user actions and so on...

#### Conditional imports

Let's create a new JavaScript file, user-module.js, with a basic user functions.

```js
// user-module.js
const USERNAME_ID_KEY = "_idcdl029fff";
export const MODULE_NAME = "user";
export const DEFAULT_USERNAME = "Jensen";
export const USER_ROLE = "admin";
export const getUserId = (user) => user.id;
export default USERNAME_ID_KEY;
```

Now, let's create a new JavaScript file, index.js, and import the user-module.js file.
In static import, we can't conditionally import a module.

```js
// index.js
if (condition) {
    import ...; // SyntaxError: Unexpected token '{'
}
```

But how can we import a module dynamically, on-demand?

```js
// index.js
const currentUser = {
  role: "admin",
};
if (currentUser.role === "admin") {
  import("./user-module.js")
    .then((userModule) => {
      console.log(userModule.DEFAULT_USERNAME); // Jensen
      console.log(userModule.default); // _idcdl029fff
      console.log(userModule.getUserId({ id: 32 })); // 32
    })
    .catch((err) => {
      console.error(err);
    });
}
```

#### Computed import path

You can also use computed import path to import a module based on a variable. That approach is not allowed in a static import.

```js
import { DEFAULT_USERNAME } from `./${user}-module.js`; // Unexpected template string
```

Use instead,

```js
const USER =  {
  DEVELOPER : 'developer',
  DESIGNER : 'designer',
};
const customPath = `./${USER.DEVELOPER}-module.js`;
import(customPath)
    .then(module => {
        ... // your code
    })
    .catch(err => {
        console.error(err)
    })
```

🎉 That's it! You've learned how to use dynamic imports in JavaScript. Happy coding! 😄
