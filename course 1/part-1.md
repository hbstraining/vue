# Getting Started

To start, we'll need to add Vue to our page.  The easiest way to do this is to simply include it in **index.html** at the bottom of your `<body>` tag.

```html
<body>
    <script src="https://unpkg.com/vue"></script>
</body>
```

Next, create the `<div>` which will contain our Vue app will live.

```html
<body>
    <div id="shopping-list">
        <h1>shopping list content</h1>
    </div>

    <script src="https://unpkg.com/vue"></script>
</body>
```

Vue isn't currently doing anything on the page, even though we've loaded it in with the `<script>` tag.  Let's update our code to make use of Vue.  For this simple application, we'll do everything in `<script>` tags within our **index.html** file, although in the future we'll be making use of Vue modules to separate our code more cleanly.  To get vue on the page, we'll need to create a Vue instance, and pass it a config object.

```html
<body>
    <div id="shopping-list">
        <h1>shopping list content</h1>
    </div>

    <script src="https://unpkg.com/vue"></script>

    <script>
        var shoppingList = new Vue({})
    </script>
</body>
```

Vue doesn't know what part of the HTML to bind to, unless we specify using the `el` attribute in the passed in config object. `el` is short for 'element', and is the standard name for most front-end frameworks.

```js
new Vue({
    el: '#shopping-list'
})
```

That's all we need to do to instantiate Vue.  Next, let's add some data to the Vue instance, which is done using the `data` attribute in the passed in config object.  `data` is where we can store any data we want our Vue instance to use.

```js
new Vue({
    el: '#shopping-list',
    data: {
        header: 'vue shopping list content'
    }
})
```

Next, we'll use Vue's templating syntax (double-mustache syntax) to dynaically bind the header data from the Vue instance to the HTML.

```html
<div id="shopping-list">
    <h1>{{ header }}</h1>
</div>
```

This is a one way binding from our Vue instance to the HTML.  Changes to the Vue data will change the HTML, however, Vue's reactivity allows us to create two-way bindings between an `<input>` element and the Vue instance.  To do this, we'll use a few things, the first is a new `<input>` field, and the second is our first directive `v-model`.

```html
<div id="shopping-list">
    <h1>{{ header }}</h1>
    <input type="text" v-model="header">
</div>
```

Now, when you change the value in the input, it changes the value displayed in the `<h1>`.

To see that binding doesn't just flow from the template to the Vue instance, but the other way as well, let's make a small modification to the code.  Instead of declaring `new Vue`, let's assign our Vue instance to a variable called `shoppingList`

```js
const shoppingList = new Vue({
    el: '#shopping-list',
    data: {
        header: 'vue shopping list content'
    }
});
```

Now you can open up Chrome Dev tools and change the data in the Vue instance directly to see the changes affect the HTML.

```js
shoppinglist.$data.header = 'console shopping list';
```
