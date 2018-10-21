# User Input & Vue Devtools

At the end of last class, we left off with the following in our **index.html** file.  You should use this as your starting point.

```html
<body>
    <div id="shopping-list">
        <h1>{{ header.toLocaleUpperCase() }}</h1>
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

In the part-1, we used `v-model` when we tried out Vue's reactivity system.  Now we'll use it again to allow us to add new items to our shopping list.  Start by adding a `newItem` property to our `data`.

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
    }
});
```

Next, add an input element to the template, using `v-model` to bind it to the `newItem` data attribute.

```html
<div id="shopping-list">
    <h1>{{ header.toLocaleUpperCase() }}</h1>
    <input v-model="newItem" type="text" placeholder="add an item">
    <ul>
        <li v-for="item in items">{{ item }}</li>
    </ul>
</div>
```

This will keep the `newItem` property in sync with what the user types in the input box.  At this point, I'd like to introduce a useful tool for seeing what's going on in a Vue application.  Follow [this link](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd) and install the Vue Devtools browser extension in Chrome.  Vue Devtools in an integral part of a Vue developers workflow.

Once you've finished the installation, you'll notice a Vue icon next to the URL bar which appears grey.  Clicking on the icon will display the message **Vue.js not detected**.  The reason it's not detecting that we have Vue installed in our application is that we're serving it directly from the file system instead of using a web server.  To get this to work, you'll need to modify your Chrome Devtools settings.  Click on the three vertical dots to the right of the Vue Devtools icon, Select **More Tools**, then **Extensions**.  Scroll down to Vue Devtools and click on the **Details** button, then scroll down and turn on **Allow access to file URLs**.

At this point, reloading the page will show that Vue is recognized on the page by the fact that the Vue Devtools icon is green.  To vue details of the application, navigate to the **Vue** tab in Chrome Devtools.  Clicking on the `<Root>` element will give you access to view, add, delete, and update the data in our application.

As a test, with Vue Devtools open, start to type in the input box and watch the `newItem` property update in real time.