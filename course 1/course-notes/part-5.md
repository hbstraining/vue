# Handling Events

At the end of last class, we left off with the following in our **index.html** file.  You should use this as your starting point.

```html
<body>
    <div id="shopping-list">
        <h1>{{ header.toLocaleUpperCase() }}</h1>
        <input v-model="newItem" type="text" placeholder="add an item">
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

In order to add the new item the user has typed to our `items` array, we'll start by adding a button to the page.

```html
<div id="shopping-list">
    <h1>{{ header.toLocaleUpperCase() }}</h1>
    <div class="item-add-form">
        <input v-model="newItem" type="text" placeholder="add an item">
        <button class="btn btn-primary">Save it</button>
    </div>
    <ul>
        <li v-for="item in items">{{ item }}</li>
    </ul>
</div>
```

The only thing left to do now is watch for a click event on the button, and push the text from the input box to the `items` array.  `v-on` is a directive we can use to listen for events and respond.

```html
<button class="btn btn-primary" v-on:click="items.push( newItem )">Save it</button>
```

To make the application more functional, let's allow the user to save the contents of the text box using the **enter** key.  Because we're listening for a key event, `v-on` is the correct directive to use.  Vue has several key modifiers to look for common key events, which allows us to write with a nice shorthand.

```html
<input v-model="newItem" type="text" placeholder="add an item" v-on:keyup.enter="items.push( newItem )">
```

Vue has the ability to respond to all events available in JavaScript, and we'll be touching on many more later.  In the meantime, we can clean up the code we wrote for our `<input>` and `<button>` tags in a few ways.  We can start by using the shorthand syntax for `v-on`, which is the `@` symbol, and in the next part, you'll see how to move the code that pushes `newItem` to the `items` array into a method.

```html
<input v-model="newItem" type="text" placeholder="add an item" @keyup.enter="items.push( newItem )">
<button class="btn btn-primary" @click="items.push( newItem )">Save it</button>
```