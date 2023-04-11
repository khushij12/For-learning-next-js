# For-learning-next-js
Using next js, graphql

## In React, 
- has to be bundle with bundler like webpack and transformed using a compiler like Babel.
    - Babel: This is a JavaScript compiler that helps in transforming modern JavaScript code into a backwards compatible version that can be run in current and older browsers/environments.
    - Webpack: It helps in bundling the style, images, code and assets, and also has several plugins for optimizing the build. It is a static module bundler for JS.
- code splitting for production optimization to improve performance and can reduce the amount of data that needs to be transformed over network
    - Example:
      First, install the react-loadable library as a development dependency:
      ```css
      npm install --save-dev react-loadable
      ```
      Next, create a new file called AsyncComponent.js in your app's directory:

      ```js
      import React from 'react';
      import Loadable from 'react-loadable';

      const AsyncComponent = Loadable({
        loader: () => import('./MyComponent'),
        loading: () => <div>Loading...</div>,
      });

      export default AsyncComponent;
      ```
      In this example, MyComponent is the component that we want to code split. The AsyncComponent file is responsible for loading that component asynchronously.

      Finally, in your app's main file, you can use the AsyncComponent like this:

      ```js
      import React from 'react';
      import AsyncComponent from './AsyncComponent';

      function App() {
        return (
          <div>
            <h1>Welcome to my app!</h1>
            <AsyncComponent />
          </div>
        );
      }

      export default App;
      ```
- You might want to statically pre-render some pages for performance and SEO.
    - To statically pre-render some pages for performance and SEO in a React app, you can use a technique called Static Site Generation (SSG).

      SSG generates HTML pages during the build process of your app, and these pages are then served statically to the client. This means that the page content is pre-rendered and ready to display as soon as the user requests it, instead of having to wait for client-side JavaScript to load and render the page.

      Here are the steps to implement SSG in a React app:

      1. Choose a static site generator: There are several options available, including Gatsby, Next.js, and React Static. These generators provide built-in support for SSG.
      2. Configure your app for SSG: Depending on the static site generator you choose, you will need to configure your app accordingly. Typically, this involves setting up a configuration file, defining your app's routes, and specifying the data sources for each page.
      3. Build your app: Once your app is configured for SSG, you can build it to generate the pre-rendered pages. This can be done with a command like npm run build or yarn build.
      4. Deploy your app: After building your app, you can deploy it to a hosting service like Netlify or Vercel, which can serve the pre-rendered pages to the client.
    - Here is an example of how you can use SSG with Next.js to pre-render some pages:

    Create a Next.js app: Run the following command to create a new Next.js app:
    ```lua
    npx create-next-app my-app
    ```
    Create some pages: Create some React components in the pages directory of your app, for example:
    ```jsx
    // pages/index.js
    function HomePage() {
      return (
        <div>
          <h1>Welcome to my app!</h1>
          <p>This page is statically pre-rendered.</p>
        </div>
      );
    }

    export default HomePage;
    ```
    ```jsx
    // pages/about.js
    function AboutPage() {
      return (
        <div>
          <h1>About Us</h1>
          <p>This page is also statically pre-rendered.</p>
        </div>
      );
    }

    export default AboutPage;
    ```
    Configure SSG: In the next.config.js file, add the following code to enable SSG:
    ```js
    module.exports = {
      exportPathMap: async function () {
        return {
          '/': { page: '/' },
          '/about': { page: '/about' },
        };
      },
    };
    ```
    This code defines the routes for your app and tells Next.js to pre-render them statically.

    Build your app: Run the following command to build your app:
    ```arduino
    npm run build
    ```
    Deploy your app: You can now deploy your app to a hosting service like Vercel or Netlify, which can serve the pre-rendered pages to the client.
- You might have to write some server-side code to connect your React app to your data store.
    - Example:
    To connect a React app to a data store, you would typically use server-side code. Here's an example of how to do this using Node.js and MongoDB:

    Install the required dependencies:
    ```css
    npm install express mongoose
    ```
    Create a server.js file with the following code:
    ```js
    const express = require('express');
    const mongoose = require('mongoose');
    const app = express();

    // Connect to MongoDB
    mongoose.connect('mongodb://localhost/myapp', { useNewUrlParser: true, useUnifiedTopology: true });

    // Create a schema for your data
    const myDataSchema = new mongoose.Schema({
      name: String,
      age: Number,
      email: String
    });

    // Create a model for your data
    const MyData = mongoose.model('MyData', myDataSchema);

    // Create an endpoint to get all data
    app.get('/api/data', async (req, res) => {
      try {
        const data = await MyData.find();
        res.json(data);
      } catch (err) {
        console.error(err);
        res.status(500).send('Server error');
      }
    });

    // Start the server
    const PORT = process.env.PORT || 5000;
    app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
    ```
    In your React app, make a request to the server to get the data. Here's an example using the fetch API:
    ```js
    fetch('/api/data')
      .then(res => res.json())
      .then(data => console.log(data))
      .catch(err => console.error(err));
    ```
    Note that in a real-world app, you would probably want to handle errors and loading states, and you would also want to use a more robust HTTP library such as Axios.
    
## In Next.js,
- An intuitive page-based routing system (with support for dynamic routes)
Pre-rendering, both static generation (SSG) and server-side rendering (SSR) are supported on a per-page basis
Automatic code splitting for faster page loads
Client-side routing with optimized prefetching
Built-in CSS and Sass support, and support for any CSS-in-JS library
Development environment with Fast Refresh support
API routes to build API endpoints with Serverless Functions
Fully extendable

## Pages
- Each page is associated with a route based on its file name.
### Pages with Dynamic Routes
- Next.js supports pages with dynamic routes. For example, if you create a file called pages/posts/[id].js, then it will be accessible at posts/1, posts/2, etc.












































Now, when the AsyncComponent is loaded, it will only download the code for MyComponent if it hasn't already been downloaded. This can significantly improve the performance of your app, especially for larger codebases.
    
