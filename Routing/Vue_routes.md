Let's simplify the explanation of Vue Router:
What is Vue Router?

Vue Router is a tool used with Vue.js to help you create web pages that can change content without reloading. It's like turning your web application into a TV, where you can switch channels (pages) without turning the TV off and on again.

## Why Use Vue Router?

Single Page Applications (SPA): Vue Router lets you build a SPA, where users can navigate through different parts of your application smoothly, without the usual page reloads. It feels faster and more fluid.

## Bookmarkable URLs: Even though the page doesn't reload, users can still bookmark URLs or share them. Each "view" or "component" in your application can have its own URL.

## Basic Concepts

## Routes: Think of routes as paths or addresses. Each route tells Vue Router which page (component) to show when the user visits a specific URL.

## Components: These are the different pages or views of your application. You create a component for each part of your application (like Home, About, Contact).

`<router-link>`: This is a special link used in your templates. When you click it, Vue Router will show the component associated with its to attribute without reloading the page.

 `<router-view>`: This is a placeholder component where Vue Router displays the current route's component.

### How Does It Work? - A Simple Example

Imagine you have a website with two pages: Home and About.

Install Vue Router: First, you add Vue Router to your project.

Define Your Routes: You tell Vue Router that when someone goes to /, they should see the Home page, and when they go to /about, they should see the About page.

What is Vue Router?
Vue Router is a tool used with Vue.js to help you create web pages that can change content without reloading. It's like turning your web application into a TV, where you can switch channels (pages) without turning the TV off and on again.

Why Use Vue Router?
**Single Page Applications (SPA)**: Vue Router lets you build a SPA, where users can navigate through different parts of your application smoothly, without the usual page reloads. It feels faster and more fluid.


1. Define Your Routes: You tell Vue Router that when someone goes to `/`, they should see the `Home` page, and when they go to `/about`, they should see the `About` page.

```javascript
const routes = [
  { path: '/', component: HomePage },
  { path: '/about', component: AboutPage }
];
```
2. Create Vue Router Instance: You create a Vue Router instance and tell it about your routes.
```javascript
const router = VueRouter.createRouter({
  history: VueRouter.createWebHistory(),
  routes: routes
});
```

4. Use the router
```javascript
const app = Vue.createApp({});
app.use(router);
```

5. Add `<router-link>` and `<router-view>` to your template
 
```javascript
<router-link to="/">Home</router-link>
<router-link to="/about">About</router-link>
```

  - Besides, We can also use the `{{ name }}` syntax to bind the value of the to attribute to a data property.
  
  - The `to` attribute of `<router-link>` is the path that the link should navigate to when clicked.
  
  - The content of the `<router-link>` tag is the text that will be displayed as the link.
  
  - When you click a `<router-link>`, Vue Router will show the component associated with the `to` attribute without reloading the page.
  
  - `<router-link>` also accepts parameters and query strings. For example, `<router-link :to`=`"{ name: 'user',` `params: { id: 123 }}">User</router-link>` will navigate to the `user` route with the parameter `id` set to `123`.

6. `<router-view>` is where the current route's component will be displayed
```javascript
<router-view></router-view>
```

7. **Route Parameters**: You can also pass parameters in the URL, like `/user/123`. Vue Router can extract these parameters and pass them to your components.

```javascript
const routes = [
    path: '/user/:id',
    name: 'user', // optional , it is used to identify the route by name
    component: UserPage
//set props=true if you want to pass the route params as props to the component
    props: true

];
```
Here `:id` is a parameter that can be accessed in the `UserPage` component.

8. `$route`: This is an object that represents the **current route**. You can access the route's parameters, query, and other information through this object.
    -`$route.params`: This is an object containing the route parameters. For example, if the URL is `/user/123`, `$route.params.id` will be `123`.

9. **Redirects**: You can redirect users to a different route using the `redirect` property in the route configuration.
```javascript
const routes = [   
    path: '/home',//old path
    redirect: '/' //new path, to be redirected here


```

**catchAll** property is used to redirect all the routes that are not defined in the routes array.
```javascript
const routes = [
   path: '/:catchAll(.*)', //catch all routes that are not defined
    redirect: '/not-found' //redirect to not-found page
```
10. **Navigation**: You can navigate programmatically using the `$router` object.
    - `$router.push({ name: 'user', params: { id: 123 } })`: This will navigate to the `user` route with the parameter `id` set to `123`.
    - `$router.push('/about')`: This will navigate to the `/about` route.
    - `$router.go(-1)`: This will go back to the previous page in the history.
    - `$router.go(1)`: This will go back to the forward page in the history.
    - `$router.replace('/about')`: This will replace the current page in the history with the `/about` route.
```javascript
//navigate to the user route with id 123
$router.push({ name: 'user', params}}: { id: 123 } });
//$router.go(-1) //go back to the previous page
//$router.go(1) //go forward to the next page
//$router.replace('/about') //replace the current page with the about page
```    


11. **Custom Regex in Params**: You can use custom regex patterns in route parameters.
```javascript
const routes = [
  // matches /o/3549
  { path: '/o/:orderId' },
  // matches /p/books
  { path: '/p/:productName' },
]
```

12. **Repeatable Params**: You can have repeatable parameters in the URL.
```javascript
const routes = [
  // /:chapters -> matches /one, /one/two, /one/two/three, etc
  { path: '/:chapters+' },
  // /:chapters -> matches /, /one, /one/two, /one/two/three, etc
  { path: '/:chapters*' },
]
```

13. **Sensitive and Strict Route Options**:
  
By default, all routes are `case-insensitive` and `match routes with or without a trailing slash`. e.g. a `route /users matches /users, /users/, and even /Users/`. This behavior can be configured with the strict and sensitive options, they can be set both at a router and route level:

`sensitive`: When set to true, the route will be case-sensitive. (default: false)
`strict`: When set to true, the route will be strict. (default: false),i.e., it will not match the route if there is a trailing slash.

```javascript
const router = createRouter({
  history: createWebHistory(),
  routes: [
    // will match /users/posva but not:
    // - /users/posva/ because of strict: true
    // - /Users/posva because of sensitive: true
    { path: '/users/:id', sensitive: true },
    // will match /users, /Users, and /users/42 but not /users/ or /users/42/
    { path: '/users/:id?' },
  ],
  strict: true, // applies to all routes
}) //if we try to access /Users/posva, it will not match the route and the output will be 404
```

14. **Optional Parameters**: You can have optional parameters in the URL.
```javascript
const routes = [
  // matches /user, /user/123, /user/123/edit
  path: '/user/:id/edit?',
  component: UserEditPage
]
```

15. **Nested Routes**: You can have nested routes in Vue Router.
```javascript
const routes = [
  {
    name: 'user/:id',
    component: User,
    children: [
      {
        name: 'profile',
        path: 'profile',
        component: UserProfile
      },
      {
        name: 'posts',
        path: 'posts',
        component: UserPosts    
      }
    ]
  }
]
```
The above configuration will match the following URLs:
- `/user` -> User component
- `/user/profile` -> UserProfile component
- `/user/posts` -> UserPosts component
- `/user/profile/posts` -> User component with UserProfile and UserPosts components nested inside it.
- `/user/posts/profile` -> User component with UserPosts and UserProfile components nested inside it.


16. **Named Routes**: You can name your routes for easier navigation.
```javascript
const routes = [
  {
    name: 'user',
    route: '/user/:id',
    component: User
  }
]
```

17. **Named Views**: You can have multiple views in a single route.
```javascript
const routes = createRouter({
  history: createWebHashHistory(),
  routes: [
    {
      path: '/',
      components: {
        default: Home,
        // short for LeftSidebar: LeftSidebar
        LeftSidebar,
        // they match the `name` attribute on `<router-view>`
        RightSidebar,
      },
    },
  ],
})
```
18. **Nested Named Views**: You can have nested named views in Vue Router.
```javascript
const routes = createRouter({
  history: createWebHashHistory(),
  routes: [
    {
      path: '/',
      components: {
        default: Home,
        LeftSidebar,
        RightSidebar,
      },
      children: [
      {
        path: 'child',
        components: {
          default: ChildComponent,
          LeftSidebar: ChildLeftSidebar,
          RightSidebar: ChildRightSidebar,
        },
      },
    ],
  },
];
```
19. **Redirect and Alias**: You can use the redirect and alias properties in Vue Router.

`Alias`: to allow multiple paths to render the same component.

```javascript
const routes = [
  {
path: '/',
    component: Home,
  },
  {
    path: '/about',
    component: About,
  },
  {
    path: '/home',
    redirect: '/', // Redirect /home to /
  },
  {
    path: '/user/:id',
    component: User,
    alias: '/profile/:id', // Alias /profile/:id to /user/:id
  },
];
```

20. **Passing Props to Route Components**: You can pass props to route components in Vue Router.
```javascript
const routes = [
  {
  path: '/user/:id',
  component: User,
  props: true
}
]
```
21. **Active Links**:
    
```html
<template>
  <div>
    <router-link to="/" active-class="active-link">Home</router-link>
    <router-link to="/about" active-class="active-link">About</router-link>
  </div>
</template>

<style>
.active-link {
  font-weight: bold;
  color: red;
}
</style>
```

A RouterLink is considered to be `active` if:

1. It **matches the same route record (i.e. configured route) as the current location.**
2. It **has the same values for the params as the current location.**

If you're using `nested routes`, `any links to ancestor routes will also be considered active if the relevant params match`.