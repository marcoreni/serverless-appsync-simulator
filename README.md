This serverless plugin is a wrapper for [amplify-appsync-simulator](amplify-appsync-simulator) made for testing AppSync APIs built with [serverless-appsync-plugin](https://github.com/sid88in/serverless-appsync-plugin).


# Requires
- [serverless framework](https://github.com/serverless/serverless)
- [serverless-appsync-plugin](https://github.com/sid88in/serverless-appsync-plugin)
- [serverless-offline](https://github.com/dherault/serverless-offline)
- [serverless-dynamodb-local](https://github.com/99xt/serverless-dynamodb-local) (when using dynamodb resolvers only)

# Install

````bash
npm install serverless-appsync-simulator
# or
yarn add serverless-appsync-simulator
````

# Usage

This plugin relies on your serverless yml file and on the `serverless-offline` plugin.

````yml
plugins:
  - serverless-dynamodb-local # only if you need dynamodb resolvers
  - serverless-appsync-simulator
  - serverless-offline
````

**Note:** Order is important `serverless-appsync-simulator` must go **before** `serverless-offline`

To start the simulator, run the followin command:
````bash
sls offline start
````

You should see in the logs something like:

````bash
...
Serverless: AppSync endpoint: http://localhost:20002/graphql
Serverless: GraphiQl: http://localhost:20002
...
````

# Configuration

Put options under `custom.appsync-simulator` in your `serverless.yml` file

| option | default | description |
|--------|---------|-------------|
| apiKey   | `0123456789`   | When using `API_KEY` as authentication type, the key to authenticate to the endpoint. |
| port   | 20002   | AppSync operations port |
| wsPort | 20003   | AppSync subscriptions port |
| location | . (base directory)   | Location of the lambda functions handlers. |

Example:

````yml
custom:
  appsync-simulator:
    location: '.webpack/service' # use webpack build directory
````

# Caveats

This plugin currently only supports resolvers implemented by `amplify-appsync-simulator`.
At the time of writing, this is:

- NONE
- AWS_LAMBDA (*)
- AMAZON_DYNAMODB

(*) Note: This plugin also supports `AWS_LAMBDA`'s `BatchInvoke` (which Amplify Simulator doesn't)
