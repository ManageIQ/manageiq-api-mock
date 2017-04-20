# ManageIQ Mock API

[![Build Status](https://travis-ci.org/ManageIQ/manageiq-api-mock.svg?branch=master)](https://travis-ci.org/ManageIQ/manageiq-api-mock)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg?style=plastic)](https://github.com/semantic-release/semantic-release)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
## Installation

If you don't plan on doing doing development for Mock API and would just like to use what has been developed, please run 
``` npm install -g  @manageiq/manageiq-api-mock```  
or ``` yarn global add  @manageiq/manageiq-api-mock```

## Development Installation
Download this git repository and run 
``` npm install ```  
or ``` yarn install```
### Mock API Usage
If you installed this NPM package globally then you can run it anywhere on the command line by running ``` mockapi ```  

(By default it runs on port 3004).  If you want to change ports or view available CLI options , run ```mockapi -h```   

If you want to include this node module in your project install it as you would any other dependency like 
```yarn add @manageiq/manageiq-api-mock	```  

If you want to start Mock API from your package.json "scripts" section.  Here is a snippet that makes that possible

``` 
"scripts": {
     "start:mock-api": "cd node_modules/manageiq-api-mock/ && node index.js"
     }
```
Then when in your projects directory you can then start mock api by running ```yarn start:mock-api``` or ```npm start:mock-api```

#### Configuration
If you would like to get this to run on a different port , please set the following environmental variable
```export MOCK_API_HOST=localhost:3005``` or whatever port you would like.  

If you would like to debug incoming http requests please set the following environmental variable
```export LOG_LEVEL=debug```

#### How to add data and RESTful endpoint data

If you look at the root of the project you will see a folder named **data** that contains subfolders that have .json files.  
If you want to add a new restful endpoint or edit an existing endpoint create a file with the following naming convention```unique_filename.json```  

* Please note that the folders under **data** are just to help organize files and do not have to match the endpoint the files underneath are for.  
 
Below you will see a sample of what one of the files looks like

```
{
    "url":"blueprints",
    "get":{"test":"test"},
    "put":{},
    "post":{},
    "delete":{}
}
```  
Key Elements in configuration    

- **url** - At the high level of the json object an endpoint is the restful endpoint you are defining.  So in this example "blueprints" would actually be for the url http://localhost:3000/api/blueprints.  
- **get** - This is a object with the data you would like the server to respond with 
- **put** - This is a object with the data you would like the server to respond with 
- **post** - This is a object with the data you would like the server to respond with 
- **delete** - This is a object with the data you would like the server to respond with 

#### Handling querystrings and subpaths

Sometimes you will have urls with querystrings you need to handle
like *http://localhost:3000/api/blueprints?test=123*
  
You also might end up with urls with subpaths like *http://localhost:3000/api/blueprints/test/path/*

The Mock API handles defining both of these scenarios the same way.  
For example querystrings  

```
{  
	"url":"blueprints?test=123",
	"get":{"test":"test"}
}
```
or subpaths

```
{
	"url":"blueprints/test/path/",
	"get":{"test":"test"}
}

```
#### Overriding stock endpoints with local changes
If you would like to override any of the endpoints in the repo please drop the overriden files into the **/local** directory structure.  This will pick up and override files that match from stock data.  

### Contributing
Please see [CONTRIBUTING.md](CONTRIBUTING.md) for more details on how to contribute to this repo. 