# Methods

At the end of last class, we left off with the following in our **index.html** file.  You should use this as your starting point.

```html
<body>
    <div id="shopping-list">
        <h1>{{ header.toLocaleUpperCase() }}</h1>
        <div class="add-item-form">
            <input v-model="newItem" type="text" placeholder="add an item" @keyup.enter="saveItem">
<button class="btn btn-primary" @click="saveItem">Save it</button>
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
            },
            methods: {
                saveItem() {
                    this.items.push( this.newItem );
                    this.newItem = '';
                }
            }
        });
    </script>
</body>
```