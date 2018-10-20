# Template Syntax and Expressions

At the end of last class, we left off with the following in our **index.html** file.  You should use this as your starting point.

```html
<body>
    <div id="shopping-list">
        <h1>{{ header }}</h1>
        <input type="text" v-model="header">
    </div>

    <script src="https://unpkg.com/vue"></script>

    <script>
        const shoppingList = new Vue({
            el: '#shopping-list',
            data: {
                header: 'vue shopping list content'
            }
        })
    </script>
</body>
```

We've already used Vue's templating syntax to bind data to the DOM, but it turns out we can use any JavaScript expression inside the double-mustache.  So for instance, if you want to convert the header to uppercase, you can just do the following:

```html
<h1>{{ header.toLocaleUpperCase() }}</h1>
```

There are a few limitations when executing JavaScript in this way.  None of the following will work.

```html
<!-- only one expression can be evaluated -->
<h1>{{ header; header.toLocaleUpperCase(); }}</h1>
```

```html
<!-- variables can't be declared -->
<h1>{{ var header = 'new header' }}</h1>
```

```html
<!-- long-hand if statements can't be used -->
<h1>{{ if (header) { return 'header found' } }}</h1>
```

Short hand if statements, also known as ternary statements can be used if needed.

```html
<!-- this ternary if statement will work -->
<h1>{{ header ? header : 'other header' }}</h1>
```

To see the above example in action, set the `header` attribute to `null` in the Vue config object.

```js
new Vue({
    el: '#shopping-list',
    data: {
        header: null
    }
})
```

In preparation for the next lesson, revert the changes above and reset your **index.html** file to the following.

```html
<body>
    <div id="shopping-list">
        <h1>{{ header }}</h1>
        <input type="text" v-model="header">
    </div>

    <script src="https://unpkg.com/vue"></script>

    <script>
        const shoppingList = new Vue({
            el: '#shopping-list',
            data: {
                header: 'shopping list app'
            }
        })
    </script>
</body>
```