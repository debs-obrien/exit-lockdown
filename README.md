# exit-plan

> My get out of lockdown exit plan

This is a very simple example of how to use Hasura in your project to fetch data. Feel free to clone the project and change the `GRAPHCMS_API` which is located in the apollo/client-config folder for your own hasura endpoint. Then add your own data and modify the query if you change the table name or columns.

## If you are new to Hasura it is really easy to get started.

- Here are the docs to [get started deploying with Heroku](https://hasura.io/docs/1.0/graphql/manual/getting-started/heroku-simple.html#deploy-to-heroku)
- Then you just need to [create a table and add some data](https://hasura.io/docs/1.0/graphql/manual/getting-started/first-graphql-query.html#create-a-table)

## For this example I have created a table called food with the following schema

Columns

- id - uuid, primary key, unique, default: gen_random_uuid()
- name - text
- where - text
- img - text
- status - text, default: 'pending'::text
- priority - integer

## To add to an existing project

- Install `@nuxtjs/apollo`
- Add it to your build modules in the nuxt.config.js
- Give apollo module options in the nuxt.config.js
  
```javascript
apollo: {
// optional
errorHandler: '~/plugins/apollo-error-handler.js',
// required
clientConfigs: {
default: '~/apollo/client-configs/default.js'
}
},
```

- Add a config file for apollo
  
```bash
mkdir apollo mkdir apollo/client-configs
touch apollo/client-configs/default.js
```

- Add the following code inside remembering to replace the endpoint with the endpoint you get from Hasura

```javascript
import { HttpLink } from 'apollo-link-http'
import { InMemoryCache } from 'apollo-cache-inmemory'

// Replace this with your project's endpoint
const GRAPHCMS_API = 'https://exit-lockdown.herokuapp.com/v1/graphql'

export default () => ({
  link: new HttpLink({ uri: GRAPHCMS_API }),
  cache: new InMemoryCache(),
  defaultHttpLink: false
})
```

- Optional: In the plugins folder add an `apollo-error-hander.js` file

```bash
touch plugins/apollo-error-handler.js
```

```javascript
/* eslint-disable no-console */
export default (error, nuxtContext) => {
  console.log('Global error handler')
  console.error(error)
}
```

- In your component add your query in within the script tags

```javascript
import gql from 'graphql-tag'
export const food = gql`
  query {
    food {
      id
      img
      name
      priority
      status
      where
    }
  }
`
```

- And add this below it

```javascript
export default {
  data() {
    return {
      tableHeadings: ['What I miss', 'Place', 'Status', 'Priority'],
      food: []
    }
  },
  apollo: {
    $loadingKey: 'loading',
    food: {
      query: food
    }
  }
}
```

That's all you need. You should now have your Hasura endpoint and your application making a query to view the data. Have fun

## Build Setup

```bash
# install dependencies
$ yarn

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).
