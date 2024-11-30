# Exercise 2: Book Library - Your First RESTful Backbone.js App

In this chapter, we'll build a library application for managing digital books using Backbone.js. This differs from the previous Todo application by introducing more sophisticated relationships between models and how to handle them using a REST API.

## The Library Application

Our library will allow users to:
- Add new books with title, author, release date, and keywords
- Display the list of books
- Delete books
- Search through the library

### Setting Up

First, let's set up our HTML structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <title>Backbone.js Library</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <div id="books">
        <form id="addBook" action="#">
            <div>
                <label for="title">Title:</label>
                <input id="title" type="text">
            </div>
            <div>
                <label for="author">Author:</label>
                <input id="author" type="text">
            </div>
            <div>
                <label for="releaseDate">Release date:</label>
                <input id="releaseDate" type="text">
            </div>
            <div>
                <label for="keywords">Keywords:</label>
                <input id="keywords" type="text">
            </div>
            <div>
                <button id="add">Add</button>
            </div>
        </form>
    </div>

    <script id="bookTemplate" type="text/template">
        <img src="<%= coverImage %>"/>
        <ul>
            <li><%= title %></li>
            <li><%= author %></li>
            <li><%= releaseDate %></li>
            <li>
                <%- keywords.map(keyword => `<span class="keyword">${keyword}</span>`).join(' ') %>
            </li>
        </ul>

        <button class="delete">Delete</button>
    </script>

    <script src="js/lib/jquery.min.js"></script>
    <script src="js/lib/underscore.min.js"></script>
    <script src="js/lib/backbone.min.js"></script>
    <script src="js/models/book.js"></script>
    <script src="js/collections/library.js"></script>
    <script src="js/views/book.js"></script>
    <script src="js/views/library.js"></script>
    <script src="js/app.js"></script>
</body>
</html>
```

### The Book Model

Now let's define our Book model:

```javascript
// models/book.js
const Book = Backbone.Model.extend({
    defaults: {
        title: '',
        author: '',
        releaseDate: '',
        keywords: [],
        coverImage: 'img/placeholder.png'
    },

    parse(response) {
        // Handle MongoDB-style _id
        if (response._id) {
            response.id = response._id;
        }
        return response;
    }
});
```

### The Library Collection

Next, we'll create our Library collection:

```javascript
// collections/library.js
const Library = Backbone.Collection.extend({
    model: Book,
    url: '/api/books'
});
```

### The Book View

The Book view handles the display of individual books:

```javascript
// views/book.js
const BookView = Backbone.View.extend({
    tagName: 'div',
    className: 'bookContainer',
    template: _.template($('#bookTemplate').html()),

    events: {
        'click .delete': 'deleteBook'
    },

    render() {
        this.$el.html(this.template(this.model.toJSON()));
        return this;
    },

    deleteBook() {
        this.model.destroy({
            success: () => {
                this.remove();
            },
            error: (model, response) => {
                console.error('Error deleting book:', response);
            }
        });
    }
});
```

### The Library View

The Library view manages the collection of books:

```javascript
// views/library.js
const LibraryView = Backbone.View.extend({
    el: '#books',

    events: {
        'click #add': 'addBook'
    },

    initialize() {
        this.collection = new Library();
        this.listenTo(this.collection, 'add', this.renderBook);
        this.listenTo(this.collection, 'reset', this.render);

        this.collection.fetch({reset: true});
    },

    render() {
        this.collection.each(book => {
            this.renderBook(book);
        });
    },

    renderBook(book) {
        const bookView = new BookView({model: book});
        this.$el.append(bookView.render().el);
    },

    addBook(e) {
        e.preventDefault();

        const formData = {
            title: $('#title').val(),
            author: $('#author').val(),
            releaseDate: $('#releaseDate').val(),
            keywords: $('#keywords').val().split(',').map(k => k.trim())
        };

        this.collection.create(formData, {
            wait: true,
            success: () => {
                $('#addBook')[0].reset();
            },
            error: (model, response) => {
                console.error('Error adding book:', response);
            }
        });
    }
});
```

### Starting the Application

Finally, let's initialize our application:

```javascript
// app.js
$(() => {
    new LibraryView();
});
```

### Styling

Add some basic CSS to make it look decent:

```css
/* style.css */
.bookContainer {
    border: 1px solid #ccc;
    margin: 10px;
    padding: 15px;
    border-radius: 5px;
    display: inline-block;
}

.bookContainer img {
    max-width: 100px;
    margin-bottom: 10px;
}

.keyword {
    background: #eee;
    padding: 2px 5px;
    border-radius: 3px;
    margin-right: 5px;
    font-size: 0.9em;
}

#addBook {
    margin: 20px;
}

#addBook div {
    margin-bottom: 10px;
}

#addBook label {
    display: inline-block;
    width: 100px;
}
```

### Important Notes

1. Error Handling: Notice how we've added proper error handling for AJAX operations:
```javascript
this.collection.create(formData, {
    wait: true,
    success: () => {
        // Handle success
    },
    error: (model, response) => {
        console.error('Error:', response);
    }
});
```

2. MongoDB Integration: The `parse` method in the Book model handles MongoDB's `_id` field:
```javascript
parse(response) {
    if (response._id) {
        response.id = response._id;
    }
    return response;
}
```

3. Modern JavaScript: We're using ES6+ features like arrow functions and template literals:
```javascript
keywords.map(keyword => `<span class="keyword">${keyword}</span>`).join(' ')
```

4. Event Handling: Proper event cleanup is handled by Backbone's `listenTo`:
```javascript
this.listenTo(this.collection, 'add', this.renderBook);
```

### Testing the Application

To test the application:

1. Start your server (we'll cover server setup in the next section)
2. Open the application in your browser
3. Try adding a new book
4. Verify that the book appears in the list
5. Try deleting a book
6. Refresh the page to verify persistence

### Server-Side Implementation

For the server side, you'll need a REST API that supports:

- GET /api/books - List all books
- POST /api/books - Create a new book
- DELETE /api/books/:id - Delete a book

We'll cover server implementation in detail in the next chapter.
