# Methods

At the end of last class, we left off with the following in our **index.html** file.  You should use this as your starting point.

```html
<body>
    <div id="shopping-list">
        <h1>{{ header.toLocaleUpperCase() }}</h1>
        <div class="add-item-form">
            <input v-model="newItem" type="text" placeholder="add an item" @keyup.enter="items.push( newItem )">
            <button class="btn btn-primary" @click="items.push( newItem )">Save it</button>
        </div>
        <ul>
            <li v-for="item in items">{{ item }}</li>
        </ul>
    </div>

    <script src="https://unpkg.com/vue"></script>

    <script>
        const shoppingList = new Vue({
            el: '#shopping-list',
            data: {
                header: 'shopping list app',
                newItem: '',
                items: [
                    '3 strip steaks',
                    '2 bell peppers',
                    'head of garlic',
                    'olive oil'
                ]
            }
        });
    </script>
</body>
```

It's an important practice when coding to keep your code DRY (don't repeat yourself).  When there is identical code running in a few different places, it's best to move the implementation to a shared function.  In the case of a Vue app, this involves creating a **method**.  To do this, we start by adding a **methods** attribute to the init object.

```js
const shoppingList = new Vue({
    el: '#shopping-list',
    data: {
        header: 'shopping list app',
        newItem: '',
        items: [
            '3 strip steaks',
            '2 bell peppers',
            'head of garlic',
            'olive oil'
        ]
    },
    methods: {}
});
```

Next we can create a function called `saveItem` with the same functionality we put in the `<input>` and `<button>` tags.

```js
methods: {
    saveItem() {
        // this won't work yet
        items.push( newItem );
    }
}
```

The reason the above code won't work is that methods don't have automatic access to the Vue instance data, so it can't resolve `items` or `newItem`.  To reference the Vue instance, use the `this` keyword.

```js
methods: {
    saveItem() {
        // this will work now that we're using 'this'
        this.items.push( this.newItem );
    }
}
```

The final step is to replace the logic in the `v-on`s with a call to the method.

```js
<input v-model="newItem" type="text" placeholder="add an item" @keyup.enter="saveItem">
<button class="btn btn-primary" @click="saveItem">Save it</button>
```

You may be wondering why we don't reference the `saveItem` method in the code above with parens like `saveItem()`, and the reason is that Vue is smart enough to understand when the name references a variable or a method based on what exists in the Vue instance.

One way to improve the application would be to clear out the user's input once the item has been added to the array.  To do this regardless of how the item is added, simple add a line to the `saveItem` method.

```js
saveItem() {
    this.items.push( this.newItem );
    this.newItem = '';
}
```