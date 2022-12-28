---
layout: post
title: "The Complete Guide to Full Stack MARN Web Apps Development: MongoDB, Apollo (GraphQL), React, and Node.js"
categories:
- programming
tags:
- MongoDB
- React
- Node.js
- Apollo Server
- GraphQL
- web apps
permalink: "/the-complete-guide-to-full-stack-marn-web-apps-development-mongodb-apollo-graphql-react-nodejs/"
---

<h2>What is the MARN stack?</h2>

**MARN** stands for **M**ongoDB, **A**pollo Server, **R**eact and **N**ode.js.

* [MongoDB](https://en.wikipedia.org/wiki/MongoDB) — document database
* [Apollo Server](https://www.apollographql.com/docs/apollo-server/) — [GraphQL](https://en.wikipedia.org/wiki/GraphQL) server
* [React](https://en.wikipedia.org/wiki/React_(JavaScript_library)) — a client-side JavaScript framework
* [Node.js](https://en.wikipedia.org/wiki/Node.js) — back-end JavaScript runtime environment

**MARN Stack** is the next generation of popular [MERN Stack](https://www.geeksforgeeks.org/mern-stack/) ([MongoDB](https://en.wikipedia.org/wiki/MongoDB), [Express.js](https://en.wikipedia.org/wiki/Express.js), [React](https://en.wikipedia.org/wiki/React_(JavaScript_library)), [Node.js](https://en.wikipedia.org/wiki/Node.js)). Using [Apollo Server](https://www.apollographql.com/docs/apollo-server/) instead of [Express.js](https://en.wikipedia.org/wiki/Express.js) makes it very easy to create [GraphQL](https://en.wikipedia.org/wiki/GraphQL) APIs.

Why Apollo Server instead of Express? Everything has its pros and cons. I like Apollo Server for its ease of setup, GraphiQL console (very useful during development), and support for many front-end frameworks. For more check out [Comparison of Apollo Server with `express-graphql`](https://github.com/apollographql/apollo-server/tree/cfb086227e623ba1531bb887c3919e224682ccbc#comparison-with-express-graphql).

There is a lot of documentation and tutorials for building GraphQL backend with Apollo Server. There is also a lot of documentation for consuming GraphQL API from React. Yet, there is nothing about building end-to-end web apps with React, Apollo Server backend, and MongoDB persistence layer.

In this article I will show you how to build end to end web app with [React](https://en.wikipedia.org/wiki/React_(JavaScript_library)) front-end, and [Node.js](https://en.wikipedia.org/wiki/Node.js) backend with [GraphQL](https://en.wikipedia.org/wiki/GraphQL) API (powered by [Apollo Server](https://www.apollographql.com/docs/apollo-server/)) and [MongoDB](https://en.wikipedia.org/wiki/MongoDB) persistance layer.

<!-- diagram -->

<h2>Getting Started</h2>

<h3>Installing dependencies</h3>

- Install node.js: I recommend installing node with [brew](https://brew.sh/) (I'm using node 16.14.2 and npm 8.5.0):
```
brew install node
```
- Install nodemon (I am using version 2.0.20):
```
npm install nodemon
```
- Install Mongo ([instructions for Mac](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/), [instructions for Windows](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/)). I'm using MongoDB Community Edition 6.0. I recommend installing with brew (on Mac):
```
xcode-select --install  # installing XCode tools
brew tap mongodb/brew`
brew update`
brew install mongodb-community@6.0
```

<h3>Setup Apollo Server (GraphQL API) with Node.js</h3>

Create new directory for your app:
```
mkdir marn-app
```

Create new directory for Apollo Server
```
mkdir apollo-server
cd apollo-server
```

Install dependencies:
```
npm install @apollo/client graphql @apollo/server
npm install @babel/core @babel/node @babel/preset-env --save-dev
```

Add script to run Apollo Server with nodemon to `package.json`:

{% highlight json %}
"scripts": {
    "start": "nodemon --exec babel-node --presets='@babel/preset-env' -- src/index.js"
},
{% endhighlight %}

Add `type=module` property to `package.json` to enable ES 6 modules:

{% highlight json %}
"type": "module"
{% endhighlight %}

Create `src/index.js` file with [GraphQL schema](https://www.apollographql.com/docs/apollo-server/schema/schema) and [resolvers](https://www.apollographql.com/docs/apollo-server/data/resolvers):

{% highlight javascript %}
import { ApolloServer } from '@apollo/server';
import { startStandaloneServer } from '@apollo/server/standalone';
import gql from 'graphql-tag';

// GraphQL Schema
const typeDefs = gql`
  type Query {
    hello: String
  }
`;

// GraphQL Resolvers
const resolvers = {
    Query: {
        hello: () => "Hello from Apollo Server"
    }
};

const server = new ApolloServer({typeDefs, resolvers});

const { url } = await startStandaloneServer(server, {
    listen: { port: 4000 },
});

console.log(`🚀 Server ready at ${url}`);
{% endhighlight %}

[GraphQL schema](https://www.apollographql.com/docs/apollo-server/schema/schema) describes the shape of your available data.

[GraphQL resolvers](https://www.apollographql.com/docs/apollo-server/data/resolvers) are responsible for pupulating data into fields in Schema.

The above code defines 1 field (`hello`) in GraphQL Schema, and the resolver function returns `"Hello from Apollo Server"` when querying that field.

Start Apollo Server with:
```
npm start
```

If you go to http://localhost:4000 you should see GraphQL Playground where you can execute queries:

<img src="{{ site.baseurl }}/assets/2022/apollo-graphql-playground.png" alt="Apollo GraphQL Playground" title="Apollo GraphQL Playground" />

<!-- References:
https://babeljs.io/setup#installation
https://www.apollographql.com/docs/apollo-server/migration -->

<h3>Create Web UI with React</h3>

Create react app from your project root directory:
```
npx create-react-app web-ui
cd web-ui
npm install @apollo/client graphql
npm start
```

<h2>Querying Apollo GraphQL API from React</h2>

To call Apollo Server with Apollo Client module, we need to do two things:

Initialize client:
{% highlight javascript %}
const client = new ApolloClient({
  uri: 'http://localhost:4000',
  cache: new InMemoryCache(),
});
{% endhighlight %}

Wrap React components with `ApolloProvider` component and pass `ApolloClient` instance to it:
{% highlight react %}
export default function App() {
  return (
    <ApolloProvider client={client}>
      ...
    </ApolloProvider>
  );
}
{% endhighlight %}

To query the Apollo GraphQL endpoint we can use `useQuery` React hook provided by `@apollo/client` module.

<h3>Call 'hello' query from React</h3>

Let's create `Hello` React component that will perform a call to GraphQL API and display the returned result. We need to define a GraphQL query and pass it to `useQuery`. The neat thing about the Apollo server is the ability to directly copy/paste queries from the playground.

{% highlight react %}
import { gql, useQuery } from '@apollo/client';

const HELLO_QUERY = gql`
query Query {
  hello
}
`;

export default function Hello() {
    const { data, loading, error } = useQuery(HELLO_QUERY);

    if (loading) return <p>Loading...</p>;
    if (error) {
        console.error('HELLO_QUERY error', error);
    }

    return <div>
        {loading && 'Loading...'}
        {error && 'Error (check console logs)'}
        {!loading && !error && data?.hello}
    </div>;
}
{% endhighlight %}

To make it work we need to update `App.js` with changes mentioned in previous section: initializing `ApolloCLient` and wrapping components with `ApolloProvider`:

{% highlight react %}
import { ApolloClient, InMemoryCache, ApolloProvider } from '@apollo/client';
import Hello from './components/Hello';

const client = new ApolloClient({
  uri: 'http://localhost:4000',
  cache: new InMemoryCache(),
});

export default function App() {
  return (
    <ApolloProvider client={client}>
      <Hello />
    </ApolloProvider>
  );
}
{% endhighlight %}

This should display `Hello from Apollo Server` in the browser coming from GraphQL API!

<img src="{{ site.baseurl }}/assets/2022/hello-from-apollo-server.png" alt="Hello from Apollo Server" title="Hello from Apollo Server" />

<h3>Add parameter to query</h3>

So far, the query is pretty simple. Let's make it more sophisticated by adding parameter `name`, and changing response to `Hello ${name}`.

To do that we need to modify GraphQL schema and resolvers in the backend:

{% highlight javascript %}
const typeDefs = gql`
    type Query {
        hello(name: String): String
    }
`;

const resolvers = {
    Query: {
        hello: (_, {name}) => `Hello ${name}`,
    }
};
{% endhighlight %}

Notice that we extract `name` param from the second argument of resolver function.

We can use GraphQL Playground to test it, and help us to generate the query with parameter:

<img src="{{ site.baseurl }}/assets/2022/apollo-graphql-playground-query-with-param.png" alt="Apollo GraphQL Playground: query with param" title="Apollo GraphQL Playground: query with param" />

<h3>Call GraphQL query with parameter from React</h3>

We need to update our `HELLO_QUERY`. You can copy/paste the query from GraphQL Playground:

{% highlight javascript %}
const HELLO_QUERY = gql`
    query Query($name: String) {
        hello(name: $name)
    }
`;
{% endhighlight %}

We also need to pass `name` variable to `useQuery`:

{% highlight javascript %}
const { data, loading, error } = useQuery(HELLO_QUERY, {
    variables: {name: "Jacob"},
});
{% endhighlight %}

This should result in displaying `Hello Jacob` in the browser:

<img src="{{ site.baseurl }}/assets/2022/hello-jacob.png" alt="Hello Jacob" title="Hello Jacob" />

<!-- https://www.apollographql.com/docs/react/get-started -->

<h3>Refactoring resolvers and schema to separate components</h3>

Before we move to the next section, let's clean up our backend code by extracting schema and resolvers to separate modules.

Create new file `src/models/typeDefs.js`:

{% highlight javascript %}
import gql from 'graphql-tag';

export const typeDefs = gql`
    type Query {
        hello(name: String): String
    }
`;
{% endhighlight %}

Create new file `src/resolvers.js`:

{% highlight javascript %}
export const resolvers = {
    Query: {
        hello: (_, {name}) => `Hello ${name}`,
    }
};
{% endhighlight %}

Remove equivalent pieces of code from `src/index.js` and import modules instead:

{% highlight javascript %}
import {resolvers} from './resolvers.js';
import {typeDefs} from './models/typeDefs.js';
{% endhighlight %}

This will set us up for the next section. You should always extract independent modules as much as possible to keep you code clean.

<h2>CRUD with MongoDB</h2>

CRUD stands for Create, Read, Update, Delete. It's a backbone on every web app. Except twitter. They didn't support Update for a while xD

In this section, I'll describe how to create simple CRUD for books. Every book will have title and year when it was published. Data will be stored in MongoDB. Web UI will have interface to display (Read), add (Create), edit (Update) and delete books through GraphQL API.

<h3>Working with MongoDB</h3>

To start mongo on Mac ([docs](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/)):
```
brew services start mongodb-community@6.0
```

I recommend to use [MongoDB Compass](https://www.mongodb.com/try/download/compass) for working with data in MongoDB. It's much easier than using [MongoDB Shell (mongosh)](https://www.mongodb.com/docs/mongodb-shell/). Of course, if you prefer using `mongosh`, go for it.

To get started with Books Library, let's create new database called `marn` and new collection called `books`. It can be done easily with Compass:

<img src="{{ site.baseurl }}/assets/2022/compass-createdb.png" alt="Create MongoDB with Compass" title="Create MongoDB with Compass" />

<h3>Connect to MongoDB from node.js</h3>

To connect to MongoDB from node.js we will use `mongoose`. 

It has to be installed from Apollo Server directory:

```
cd apollo-server
npm install mongoose
```

To connect to MongoDB we can establish connection in `src/index.js` by adding this code:

{% highlight javascript %}
import mongoose from 'mongoose';

mongoose.set('strictQuery', true);
const db = await mongoose.connect("mongodb://localhost:27017/marn", {
    useNewUrlParser: true,
});
console.info('📚 Connected to db', db?.connections[0]?._connectionString);
{% endhighlight %}

Make sure your MongoDB uses port 27017. If not, update the uri. You can find the uri in Compass UI:

<img src="{{ site.baseurl }}/assets/2022/compass-localhost.png" alt="MongoDB uri in Compass" title="MongoDB uri in Compass" />

<h3>Create Book model and query data from MongoDB</h3>

We can map MongoDB collections to JavaScript objects by creating models with `mongoose`. Create Book model in `src/models/Book.js` file:

{% highlight javascript %}
import mongoose from 'mongoose';

export const Book = mongoose.model('Book', { title: String, year: Number });
{% endhighlight %}

We can query all books by simply calling the `Book` model:

{% highlight javascript %}
Book.find({})
{% endhighlight %}

To make data accessible through GraphQL, we need to add `Book` type to GraphQL schema and `books` query that returns array of `Book` elements in `src/models/typeDefs.js`:

{% highlight javascript %}
import gql from 'graphql-tag';

export const typeDefs = gql`
    type Query {
        hello(name: String): String
        books: [Book]
    }
    type Book {
        id: ID,
        title: String,
        year: Int,
    }
`;
{% endhighlight %}

We also need to add resolver that is querying MongoDB with `mongoose` in `src/resolvers.js`:

{% highlight javascript %}
import {Book} from './models/Book.js';

export const resolvers = {
    Query: {
        hello: (_, {name}) => `Hello ${name}`,
        books: async () => await Book.find({}),
    }
};
{% endhighlight %}

Querying with Playground should return empty array:

<img src="{{ site.baseurl }}/assets/2022/apollo-query-books-empty.png" alt="Apollo books query (empty)" title="Apollo books query (empty)" />

Let's add a book to MongoDB with Compass by clicking `ADD DATA -> Insert document`:

<img src="{{ site.baseurl }}/assets/2022/insert-mongodb-document.png" alt="Insert document with Compass" title="Insert document with Compass" />

Once the book is added it should be returned in `books` query:
<img src="{{ site.baseurl }}/assets/2022/apollo-query-books-one-book.png" alt="Apollo books query (one book)" title="Apollo books query (one book)" />

<h3>Display books in React UI</h3>

To make styling easier, let's use [Twitter Bootstrap](https://getbootstrap.com).

Add bootstrap css to `web-ui/public/index.html` in `<head>` section:

{% highlight html %}
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.0.0/dist/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
{% endhighlight %}

To display books, we will create two components: 
1. `Books` - for querying GraphQL API and displyaing all books
2. `Book` - for displaying single book (data will be passed from `Books` component)

Let's start with `Book` component. Create new file `src/components/Book.js`:

{% highlight react %}
export default function Book({book}) {
    return (
        <tr>
            <td>{book.title}</td>
            <td>{book.year}</td>
        </tr>
    );
}
{% endhighlight %}

The `Books` component will use the `Book` component to display all books from MongoDB. It will also fetch data from GraphQL API. We need to define GraphQL query (which we can copy form Playground), and query Apollo Server with `useQuery`. Create new file `src\components\Books.js`:

{% highlight react %}
import { gql, useQuery } from '@apollo/client';
import Book from './Book';

const BOOKS_QUERY = gql`
    query Books {
        books {
            title
            year
            id
        }
    }
`;

export default function Books() {
    const {data, error, loading} = useQuery(BOOKS_QUERY);

    if (error) {
        console.error('BOOKS_QUERY error', error);
    }

    return <div>
        <table className='table'>
            <thead className='thead-dark'>
                <tr>
                    <th>Title</th>
                    <th>Year</th>
                </tr>
            </thead>
            <tbody>
                {loading && <tr><td>Loading...</td></tr>}
                {error && <tr><td>Check console for error logs</td></tr>}
                {!loading && !error && data?.books.map(book => <Book book={book} key={book.id} />)}
            </tbody>
        </table>
    </div>;
}
{% endhighlight %}

Import `Books` component in `App` component and display it on the main page:

{% highlight react %}
import { ApolloClient, InMemoryCache, ApolloProvider } from '@apollo/client';
import Hello from './components/Hello';
import Books from './components/Books';

const client = new ApolloClient({
  uri: 'http://localhost:4000',
  cache: new InMemoryCache(),
});

export default function App() {
  return (
    <ApolloProvider client={client}>
      <Hello />
      <Books />
    </ApolloProvider>
  );
}
{% endhighlight %}

When you go back to website you should see the book, which we added to database displayed in a table:

<img src="{{ site.baseurl }}/assets/2022/books-table-one-book.png" alt="Books table displayed with React" title="Books table displayed with React" />

<!-- https://getbootstrap.com/docs/4.0/getting-started/introduction/ 
https://getbootstrap.com/docs/4.0/content/tables/  -->

<h3>Add React Router</h3>

Before we start working on creating, deleting and updating books, let's add navigation to our UI with [React Router](https://reactrouter.com). This will allow us to separate different views instead of cluttering them on the same page.

First, we need to install `react-router-dom` in our React app:

```
cd web-ui
npm install react-router-dom
```

We need to wrap all components in `BrowserRouter`, map routes to components, and add links allowing to navigate between routes.

All changes that needs to be done take place in `src/App.js`:

{% highlight react %}
import { ApolloClient, InMemoryCache, ApolloProvider } from '@apollo/client';
import Hello from './components/Hello';
import Books from './components/Books';
import { Link, BrowserRouter, Route, Routes } from 'react-router-dom';

const client = new ApolloClient({
  uri: 'http://localhost:4000',
  cache: new InMemoryCache(),
});

export default function App() {
  return (
    <ApolloProvider client={client}>
      <BrowserRouter>
        <nav className="navbar navbar-dark bg-dark">
          <div className="navbar-nav mr-auto flex-row">
            <Link to="/" className="nav-link mr-2">Home</Link>
            <Link to="/books" className="nav-link mr-2">Books</Link>
          </div>
        </nav>
        <div className="container mt-5">
          <Routes>
            <Route path="/" element={<Hello />} />
            <Route path="/books" element={<Books />} />
          </Routes>
        </div>
      </BrowserRouter>      
    </ApolloProvider>
  );
}
{% endhighlight %}

After that you should see the main page with navigation and links to home that displays `Hello` component, and link to books that displays the list of books from MongoDB in a table:

<img src="{{ site.baseurl }}/assets/2022/react-router.gif" alt="React Router navigation" title="React Router navigation" />

<h3>Add create mutation</h3>

To insert a new book to MongoDB, we need to create a `Mutation`.

In GraphQL we can fetch data with `Query`, but to create or modify data, we need to create a `Mutation`. 

Let's start with updating schema. Mutations are in a separate block in the schema. We will add `create` mutation that takes `title` and `year` parameters, and returns `Book` object to `src/models/typeDefs.js` file:

{% highlight javascript %}
import gql from 'graphql-tag';

export const typeDefs = gql`
    type Query {
        hello(name: String): String
        books: [Book]
    }
    type Book {
        id: ID,
        title: String,
        year: Int,
    }
    type Mutation {
        create(title: String, year: Int): Book
    }
`;
{% endhighlight %}

Now, we need to implement resolver for `create` mutation. Similarly to schema, we need to add a new block `Mutation` to our resolvers, and `create` function. In the `create` function we need to add logic to create new book and save it to MongoDB. This is `src/resolvers.js` after updates:

{% highlight javascript %}
import {Book} from './models/Book.js';

export const resolvers = {
    Query: {
        hello: (_, {name}) => `Hello ${name}`,
        books: async () => await Book.find({}),
    },
    Mutation: {
        create: async (_, {title, year}) => {
            const newBook = new Book({
                title, year
            });
            await newBook.save();
            return newBook;
        }
    }
};
{% endhighlight %}

We can test creating books with GraphQL Playground:

<img src="{{ site.baseurl }}/assets/2022/apollo-graphql-playground-create-mutation.png" alt="Apollo GraphQL Playground - create mutation" title="Apollo GraphQL Playground - create mutation" />

If everything went well you should see new book in MongoDB. Notice `__v0` field in book inserted with Mongoose. This is versionKey property, which is set on each document when first created by Mongoose.

<img src="{{ site.baseurl }}/assets/2022/mongodb-insert-mongoose.png" alt="MongoDB - document created with mongoose" title="MongoDB - document created with mongoose" />

<h3>Add UI for creating new Book</h3>

Let's start with new `CreateBook` component. We need to create a new form to collect `title` and `year`, and call `create` mutation we created in previous section.

We will utilize `useState` hook to access `input` fields data (`title` and `year`).

To call mutation, we will use `useMutation` hook from `@apollo/client`.

We can get `CREATE_BOOK_MUTATION` from GraphQL playground.

Make sure to convert year from string to integer when passing it as variable to mutation. Otherwise it will return an error. You can simple add `+` before the variable to convert string to integer.

Add `src/components/CreateBook.js` file to `web-ui` folder:

{% highlight react %}
import { useState } from 'react';
import { gql, useMutation } from '@apollo/client';

const CREATE_BOOK_MUTATION = gql`
    mutation Mutation($title: String, $year: Int) {
        create(title: $title, year: $year) {
            id
            title
            year
        }
    }
`;

export default function CreateBook() {
    const [title, setTitle] = useState('');
    const [year, setYear] = useState('');
    const [createMutation] = useMutation(CREATE_BOOK_MUTATION);

    const handleSubmit = evt => {
        evt.preventDefault();
        console.info('Creating Book...', title, year);
        createMutation({
            variables: {
                title,
                year: +year,
            }
        });
        alert(`Book ${title} (${year}) created!`);
        setTitle('');
        setYear('');
    };

    return <form onSubmit={evt => handleSubmit(evt)}>
        <div className="form-group">
            <label htmlFor="title">Title:</label>
            <input 
                type="text" 
                name="title" 
                className="form-control"
                value={title}
                onChange={e => setTitle(e.target.value)}
                />
        </div>
        <div className="form-group">
            <label htmlFor="year">Year:</label>
            <input 
                type="text" 
                name="year" 
                className="form-control"
                value={year}
                onChange={e => setYear(e.target.value)}
                />
        </div>
        <input type="submit" value="Create" className="btn btn-primary" />
    </form>;
}
{% endhighlight %}

We will also create a separate route `/create` to to display `CreateBook` component, and a link to that route. Update `src/App.js`:

{% highlight react %}
import { ApolloClient, InMemoryCache, ApolloProvider } from '@apollo/client';
import Hello from './components/Hello';
import Books from './components/Books';
import CreateBook from './components/CreateBook';
import { Link, BrowserRouter, Route, Routes } from 'react-router-dom';

const client = new ApolloClient({
  uri: 'http://localhost:4000',
  cache: new InMemoryCache(),
});

export default function App() {
  return (
    <ApolloProvider client={client}>
      <BrowserRouter>
        <nav className="navbar navbar-dark bg-dark">
          <div className="navbar-nav mr-auto flex-row">
            <Link to="/" className="nav-link mr-2">Home</Link>
            <Link to="/books" className="nav-link mr-2">Books</Link>
            <Link to="/create" className="nav-link mr-2">Create Book</Link>
          </div>
        </nav>
        <div className="container mt-5">
          <Routes>
            <Route path="/" element={<Hello />} />
            <Route path="/books" element={<Books />} />
            <Route path="/create" element={<CreateBook />} />
          </Routes>
        </div>
      </BrowserRouter>      
    </ApolloProvider>
  );
}
{% endhighlight %}

<img src="{{ site.baseurl }}/assets/2022/react-create-book.gif" alt="Create book UI in React" title="Create book UI in React" />

You may notice that new book does not appear on the books list without refresh. There are two ways to fix it:
1. [Update local GraphQL cache](https://www.apollographql.com/docs/react/data/mutations/#updating-the-cache-directly) - use this approach when performance is priority over correctness
2. [Refetch query](https://www.apollographql.com/docs/react/data/mutations/#refetching-queries) - use this approach when correctness is more important than performance

We will use refetch query approach, which is usually the best default answer, unless you really care about high performance.

This requires to pass a list of queries to refetch to `useMutation` hook:

{% highlight react %}
const [createMutation] = useMutation(CREATE_BOOK_MUTATION, {
    refetchQueries: [
        {query: BOOKS_QUERY}
    ]
});
{% endhighlight %}

As you can see, we need `BOOKS_QUERY`, which we already defined in `Books` component. To do not copy/pasta, let's extract all GraphQL queries and mutations to `src/graphql.js` file:

{% highlight javascript %}
import { gql } from '@apollo/client';

export const CREATE_BOOK_MUTATION = gql`
    mutation Mutation($title: String, $year: Int) {
        create(title: $title, year: $year) {
            id
            title
            year
        }
    }
`;

export const BOOKS_QUERY = gql`
    query Books {
        books {
            title
            year
            id
        }
    }
`;
{% endhighlight %}

Now you can remove `BOOKS_QUERY` variable from `Books` component and just import it from `graphql.js`:

{% highlight javascript %}
import { BOOKS_QUERY } from '../graphql';
{% endhighlight %}

Similarly in, `CreateBook` component you can remove `CREATE_BOOK_MUTATION`, and import both `CREATE_BOOK_MUTATION` and `BOOKS_QUERY` from `graphql.js`:

{% highlight javascript %}
import { BOOKS_QUERY, CREATE_BOOK_MUTATION } from '../graphql';
{% endhighlight %}

<h3>Deleting books</h3>

Delete mutation will be very similar to `create` mutation from previous section. We just need a mutation that takes `id` of a book we want to delete.

Let's update schema in `src/models/typeDefs.js` by adding `delete` mutation that takes `id` parameter and returns the same id if books is successfully deleted:

{% highlight javascript %}
import gql from 'graphql-tag';

export const typeDefs = gql`
    type Query {
        hello(name: String): String
        books: [Book]
    }
    type Book {
        id: ID,
        title: String,
        year: Int,
    }
    type Mutation {
        create(title: String, year: Int): Book
        delete(id: ID): ID
    }
`;
{% endhighlight %}

And implement resolver function in `src/resolvers.js`:

{% highlight javascript %}
import {Book} from './models/Book.js';

export const resolvers = {
    Query: {
        hello: (_, {name}) => `Hello ${name}`,
        books: async () => await Book.find({}),
    },
    Mutation: {
        create: async (_, {title, year}) => {
            const newBook = new Book({
                title, year
            });
            await newBook.save();
            return newBook;
        },
        delete: async (_, {id}) => {
            const result = await Book.deleteOne({_id: id});
            if (result.acknowledged && result.deletedCount === 1) {
                return id;
            }
            return null;
        },
    }
};
{% endhighlight %}

We can test deleting book in GraphQL playground by grabbing an id from MongoDB Compass:

<img src="{{ site.baseurl }}/assets/2022/apollo-graphql-playground-delete.png" alt="Apollo GraphQL Playground - delete" title="Apollo GraphQL Playground - delete" />

If we try to delete book that doesn't exist we should get `null` in response:

{% highlight json %}
{
  "data": {
    "delete": null
  }
}
{% endhighlight %}

We have our backend working. Let's add delete functionality to UI. 

Add delete mutation to `graphql.js` (you can copy/paste from GraphQL Playground):

{% highlight javascript %}
export const DELETE_BOOK_MUTATION = gql`
    mutation Mutation($id: ID) {
        delete(id: $id)
    }
`;
{% endhighlight %}

We will add delete button to `Book` component, and call `delete` mutation from there:

{% highlight react %}
import { useMutation } from "@apollo/client";
import { DELETE_BOOK_MUTATION, BOOKS_QUERY } from "../graphql";

export default function Book({book}) {
    const [deleteBookMutation] = useMutation(DELETE_BOOK_MUTATION, {
        refetchQueries: [
            {query: BOOKS_QUERY},
        ],
    });
    const deleteBook = () => {
        deleteBookMutation({
            variables: {
                id: book.id,
            },
        });
    };
    return (
        <tr>
            <td>{book.title}</td>
            <td>{book.year}</td>
            <td>
                <button className="btn btn-danger" onClick={deleteBook}>
                    Delete
                </button>
            </td>
        </tr>
    );
}
{% endhighlight %}

We also need to add new column to table header in `Books` component:

{% highlight html %}
<thead className='thead-dark'>
    <tr>
        <th>Title</th>
        <th>Year</th>
        <th></th>
    </tr>
</thead>
{% endhighlight %}

Clicking delete button should delete book from MongoDB and from delete row from books list table:

<img src="{{ site.baseurl }}/assets/2022/react-delete-book.gif" alt="Delete book from React UI" title="Delete book from React UI" />

<h3>Editing books</h3>

Editing is almost like creating. You need to pass `id` of an existing book in addition to `title` and `year`.

Let's update schema by adding `edit` mutation:

{% highlight javascript %}
import gql from 'graphql-tag';

export const typeDefs = gql`
    type Query {
        hello(name: String): String
        books: [Book]
    }
    type Book {
        id: ID,
        title: String,
        year: Int,
    }
    type Mutation {
        create(title: String, year: Int): Book
        delete(id: ID): ID
        edit(id: ID, title: String, year: Int): Book
    }
`;
{% endhighlight %}

And resolvers, by implementing `edit` mutation:

{% highlight javascript %}
import {Book} from './models/Book.js';

export const resolvers = {
    Query: {
        hello: (_, {name}) => `Hello ${name}`,
        books: async () => await Book.find({}),
    },
    Mutation: {
        create: async (_, {title, year}) => {
            const newBook = new Book({
                title, year
            });
            await newBook.save();
            return newBook;
        },
        delete: async (_, {id}) => {
            const result = await Book.deleteOne({_id: id});
            if (result.acknowledged && result.deletedCount === 1) {
                return id;
            }
            return null;
        },
        edit: async (_, {id, title, year}) => {
            const result = await Book.updateOne(
                {
                    _id: id,
                },
                {
                    $set: {
                        title,
                        year
                    },
                });
            if (result.acknowledged && result.modifiedCount === 1) {
                return await Book.findOne({_id: id});
            }
            return null;
        }
    }
};
{% endhighlight %}

Test in GraphQL Playground:

<img src="{{ site.baseurl }}/assets/2022/apollo-graphql-playground-edit.png" alt="Apollo GraphQL Playground - edit" title="Apollo GraphQL Playground - edit" />

To enable editing from UI, we will add an edit button to `Book` component. It will change text to `input` fields when in editing mode, and display save and cancel buttons to commit or discard changes. 

Let's start with adding `EDIT_BOOK_MUTATION` to `src/graphql.js`:

{% highlight javascript %}
export const EDIT_BOOK_MUTATION = gql`
    mutation Mutation($id: ID, $title: String, $year: Int) {
        edit(id: $id, title: $title, year: $year) {
            id
            title
            year
        }
    }
`;
{% endhighlight %}

Update `src/components/Book.js` by adding editing state, buttons and call to update book:

{% highlight react %}
import { useMutation } from "@apollo/client";
import { DELETE_BOOK_MUTATION, BOOKS_QUERY, EDIT_BOOK_MUTATION } from "../graphql";
import { useState } from "react";

export default function Book({book}) {
    const [deleteBookMutation] = useMutation(DELETE_BOOK_MUTATION, {
        refetchQueries: [
            {query: BOOKS_QUERY},
        ],
    });
    const deleteBook = () => {
        deleteBookMutation({
            variables: {
                id: book.id,
            },
        });
    };

    const [isEditing, setIsEditing] = useState(false);
    const [title, setTitle] = useState(book.title);
    const [year, setYear] = useState(book.year);
    const [editBookMutation] = useMutation(EDIT_BOOK_MUTATION, {
        refetchQueries: [
            {query: BOOKS_QUERY},
        ],
    });

    const saveChanges = () => {
        editBookMutation({
            variables: {
                id: book.id,
                title: title,
                year: +year,
            },
        });
        setIsEditing(false);        
    };

    const discardChanges = () => {
        setIsEditing(false);
        setTitle(book.title);
        setYear(book.year);
    };

    return (
        <tr>
            <td>
                {isEditing 
                 ? <input type="text" 
                    value={title} 
                    onChange={(e) => setTitle(e.target.value)} 
                    className="form-control" />
                 : book.title}
            </td>
            <td>
                {isEditing 
                 ? <input type="text" 
                    value={year} 
                    onChange={(e) => setYear(e.target.value)}
                    className="form-control" />
                 : book.year}
            </td>
            <td>
                {isEditing 
                ? <>
                    <button className="btn btn-success mr-2" onClick={saveChanges}>
                        Save
                    </button>
                    <button className="btn btn-danger" onClick={discardChanges}>
                        Cancel
                    </button>
                </>
                : <>
                    <button className="btn btn-info mr-2" onClick={() => setIsEditing(true)}>
                        Edit
                    </button>
                    <button className="btn btn-danger" onClick={deleteBook}>
                        Delete
                    </button>
                </>
                }
                
            </td>
        </tr>
    );
}
{% endhighlight %}

Now, you should be able to edit books inline:

<img src="{{ site.baseurl }}/assets/2022/react-edit-book.gif" alt="Edit book from React UI" title="Edit book from React UI" />

To make sure that everything works as expected, you can double check if books are being properly created, deleted and updated in Mongo with MongoDB Compass.

<h2>Summary</h2>

<!-- At Meta, we built [Super Events](https://super.events) web app with Apollo Server, Mongo and [Vue.js](https://vuejs.org/). We also built iOS app, which used the same Apollo Server GraphQL APIs like web app.

While Vue vs React is a matter of preference, or requirements of your project, using Apollo Server over Express.js -->

Congratulations! Now, you know how to build web apps with MARN stack!

You can find entire code in this github repo: [https://github.com/jj09/marn](https://github.com/jj09/marn).

To learn more about Apollo Server, checkout [Apollo docs](https://www.apollographql.com/docs/). It's pretty good!

To dive into MongoDB check out [MongoDB CRUD Operations](https://www.mongodb.com/docs/manual/crud/) and [mongoose API](https://mongoosejs.com/docs/api.html). Once you learn how to write Mongo queries with [MongoDB Shell](https://www.mongodb.com/docs/mongodb-shell/), you don't really need to go over [mongoose API](https://mongoosejs.com/docs/api.html) as it's almost identical.

If you are new to React, I recommend [React Docs](https://beta.reactjs.org/) and [ReactJS Crash Course](https://www.youtube.com/watch?v=w7ejDZ8SWv8).

You can very easily swap different components for MARN stack. E.g., swap React with Vue.js like I did for [this demo project](https://github.com/jj09/vue-apollo).