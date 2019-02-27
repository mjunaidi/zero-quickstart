### Getting Started

#### Installation

You can install `zero` globally by:

    npm install -g zero


#### Hello World

Let's start by making a website that tells us server time.

First we need to create an API endpoint in Node.js to tell us time in JSON.

Create a new folder and add a new file `time.js` in that folder. In this file, export a function that accepts `Request` and `Response` objects ([like Express](https://expressjs.com/en/4x/api.html#res)):

    // time.js
    const moment = require("moment")

    module.exports = (req, res) => {
      var time = moment().format('LT');   // 11:51 AM
      res.send({time: time })
    }


Once saved, you can `cd` into that folder and start the server like this:

    zero


Running this command will automatically install any dependencies (like _momentjs_ here) and start the web server.

Open this URL in the browser: [`http://localhost:3000/time`](http://localhost:3000/time)

You just created an API endpoint 🎉:

![Time API](https://zeroserver.io/assets/images/timeapi.png "Time API")

Keep the server running. Now let's consume our API from a React page, create a new file `index.jsx` and add the following code:

    // index.jsx
    import React from 'react'

    export default class extends React.Component {
      static async getInitialProps(){
        var json = await fetch("/time").then((resp) => resp.json())
        return {time: json.time}
      }

      render() {
        return <p>Current time is: {this.props.time}</p>
      }
    }


This is a standard React component. With one additional hook for initial data population:

`getInitialProps` is an `async` static method which is called by `zero` when the page loads. This method can return a plain object which populates `props`.

Now go to this URL: `http://localhost:3000/` and you should see the current server time rendered by React while `fetch`\-ing an API endpoint you created earlier:

![Time In React](https://zeroserver.io/assets/images/timejsx.png "Time In React")

`zero` automatically bundles your code and supports server-side rendering. You don't need to fiddle with webpack anymore.

That's it! You just created a web application.
