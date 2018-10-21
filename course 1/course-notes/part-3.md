# Loops

At the end of last class, we left off with the following in our **index.html** file.  You should use this as your starting point.

```html
<body>
    <div id="shopping-list">
        <h1>{{ header.toLocaleUpperCase() }}</h1>
        <input type="text" v-model="header">
    </div>

    <script src="https://unpkg.com/vue"></script>

    <script>
        const shoppingList = new Vue({
            el: '#shopping-list',
            data: {
                header: 'shopping list app'
            }
        });
    </script>
</body>
```

To start our shopping list, let's add some data for the list.  An array is the best way to represent a list of items, so we'll use that.

```js
const shoppingList = new Vue({
    el: '#shopping-list',
    data: {
        header: 'shopping list app',
        items: [
            '3 strip steaks',
            '2 bell peppers',
            'head of garlic',
            'olive oil'
        ]
    }
});
```

Next we need to loop over our list of items using a directive called `v-for`.  We'll apply the `v-for` to the element we want to be created multiple times, which in this case will be `<li>` elements inside a `<ul>`, which represents list items inside an unordered list.

```html
<div id="shopping-list">
    <h1>{{ header.toLocaleUpperCase() }}</h1>
    <ul>
        <li v-for="item in items">{{ item }}</li>
    </ul>
</div>
```

While this may look new and weird, if you break it down, it actually reads like a sentence:

*we'd like an an `<li>` for each item in our items array*

`v-for` is reactive as well, so in Chrome Devtools, in the **console** tab, you can run the following to see a new item appear on the page.

```js
shoppinglist.$data.items.push( '1/2 pound green beans' );
```
