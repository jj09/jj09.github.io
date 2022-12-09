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
* [Apollo Server](https://www.apollographql.com/docs/apollo-server/) — [GraphQL](https://en.wikipedia.org/wiki/GraphQL) server that's compatible with any GraphQL client
* [React](https://en.wikipedia.org/wiki/React_(JavaScript_library)) — a client-side JavaScript framework
* [Node.js](https://en.wikipedia.org/wiki/Node.js) — back-end JavaScript runtime environment

**MARN Stack** is the next generation of popular [MERN Stack](https://www.geeksforgeeks.org/mern-stack/) ([MongoDB](https://en.wikipedia.org/wiki/MongoDB), [Express.js](https://en.wikipedia.org/wiki/Express.js), [React](https://en.wikipedia.org/wiki/React_(JavaScript_library)), [Node.js](https://en.wikipedia.org/wiki/Node.js)). Using [Apollo Server](https://www.apollographql.com/docs/apollo-server/) instead of [Express.js](https://en.wikipedia.org/wiki/Express.js) makes it very easy to create [GraphQL](https://en.wikipedia.org/wiki/GraphQL) APIs.

There is a lot of documentation and youtube videos for building GraphQL backend with Apollo Server. There is also a lot of documentation for consuming GraphQL API from React. However, there is nothing about building end-to-end web apps with React, Apollo Server backend and MongoDB persistance layer.

<h2>Getting Started</h2>

<h3>Installing dependencies</h3>

- Install node.js: I recommend installing node with [brew](https://brew.sh/) (I'm using node 9.2.0 and npm 8.1.2):
```
brew install node
```
- Install nodemon (I am using version 2.0.20):
```
npm install nodemon
```
- Install Mongo ([instructions for Mac](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/), [instructions for Windows](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/)). I'm using MongoDB Community Edition 6.0. To install it on Mac with brew:
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

Create .babelrc file in `apollo-server` directory:

{% highlight json %}
{
    "presets": ["@babel/preset-env"]
}
{% endhighlight %}

Add script to run Apollo Server with nodemon to `package.json`:

{% highlight json %}
"scripts": {
    "start": "nodemon --exec babel-node -- src/index.js"
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

Above code defines 1 field (`hello`) in GraphQL Schema, and resolver function returns `"Hello from Apollo Server"` when querying that field.

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

To query Apollo GraphQL endpoint we can use `useQuery` React hook provided by `@apollo/client` module.

<h3>Call 'hello' query from React</h3>

Let's create `Hello` React component that will perform a call to GraphQL API and display the returned result. We need to define a GraphQL query and pass it to `useQuery`. Neat thing about Apollo server is the ability to directly copy/paste query from the playground.

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

In order to do that we need to modify GraphQL schema and resolvers in the backend:

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

Before we move to the next section, let's cleanup our backend code by extracting schema and resolvers to separate modules.

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

We can add a Book to Mongo with Compass by clicking `ADD DATA -> Insert document`:

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
                <th>Title</th>
                <th>Year</th>
            </thead>
            <tbody>
                {loading && <p>Loading...</p>}
                {error && <p>Check console for error logs</p>}
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
Update schema
Update resolver
Show with Compass

<h3>Add UI for creating new Book</h3>

<!-- Update local cache/refetch
https://www.apollographql.com/docs/react/data/mutations/#refetching-queries  -->

<h3>Deleting books</h3>
Backend
UI

<h3>Editing books</h3>
Backend
UI

<h2>Summary</h2>

At Meta, we built [Super Events](https://super.events) web app with Apollo Server, Mongo and [Vue.js](https://vuejs.org/). We also built iOS app, which used the same Apollo Server GraphQL APIs like web app.

While Vue vs React is a matter of preference, or requirements of your project, using Apollo Server over Express.js

Is Apollo Server better than Express? It depends. Everything has its pros and cons. I like Apollo Server for easy of setup, free Graphical UI (very useful during development) and support for many front-end frameworks.
https://github.com/apollographql/apollo-server/tree/cfb086227e623ba1531bb887c3919e224682ccbc#comparison-with-express-graphql