# Stoicism Quotes API creation steps and deployment

In this repository we have all the files nedeed to deploy an API in heroku. The API is going to have a simple jso file with some stoics quotes just to use it in other projects.

Now we are going to see the steps to create the project with the prerequisite needed to be able of deploit in heroku.

## 1. json file

First of all we have to create our [quotes.json](./quotes.json) file where we are going to storage the data, the quotes in our case:

```ruby
{
    "quotes": [
    {
        "id":0,
        "author": "Marcus Aurelius",
        "quote": "Waste no more time arguing what a good man should be. Be One."
    },
    {
        "id":1,
        "author": "Marcus Aurelius",
        "quote": "You could leave life right now. Let that determine what you do and say and think."
    },
    {
        "id":2,
        "author": "Seneca",
        "quote": "He who fears death will never do anything worth of a man who is alive."
    },
    {
        "id":3,
        "author": "Seneca",
        "quote": "Life is very short and anxious for those who forget the past, neglect the present, and fear the future."
    },..

```

## 2. Creating out server script 

We have to create a file where we can set the actions to run our server using the json-server package that we will install in the next step. In this file is where we can set the port and the file to show in the server, as we can see below:

```ruby

const jsonServer = require('json-server');
const server = jsonServer.create();
const router = jsonServer.router('quotes.json');
const middlewares = jsonServer.defaults();
const port = process.env.PORT || 3000;

server.use(middlewares);
server.use(router);

server.listen(port);

```

## 3. Executing our local server

Now we have to create an environment where we can use our json as an API in our machine, this way we are going to make sure that we have all the dependencies needed to deploy the app in heroku, the commands that we are going to need are:

Creating the package.json file which is going to have the configuration of out API:

```sh
npm init

```

We are going to need the [package-lock.json](./package-lock.json), so we have to use:

```sh
npm i

```

Installing server, make sure that we can see the dependency in our [package.json](./package.json) file once is installed:

```sh
npm install json-server

```

We have to create a new script in the file to run the server file that we created before like so:

```ruby

  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js"
  }

```

Setting the file to use as endpoint, we can check it in the URL that this command should show us:

```sh
json-server --watch quotes.json

```

## 4. Heroku deployment

[Here](https://devcenter.heroku.com/articles/heroku-cli) we can find the way to use it properly in different environments.

If everything worked properly we have to be able of get something like so 
[running JSON server](https://stoic-quotes-app.herokuapp.com/).

We have to make sure that in the resources section we can see our json file as endpoint.
