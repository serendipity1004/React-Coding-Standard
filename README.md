# React Coding Standard

## Table of Contents

1. [Declarations](#basics-variables)
2. [Exports](#basics-exports)
3. [Imports](#basics-imports)

## Variables

Variable declaration is always done with `let`. `var` jeopardizes the restricted scope provided by `let` so it will never be used unless it is absolutely necessary.

```jsx
import React from 'react';

class ExampleClass extends React.Component(){
    constructor(props){
        super(props);
    }
    
    componentDidMount(){
        //Use let only
        let exampleVar = 'Chorong';
        
        //DO NOT use var
        var donotUse = 'Seulki';
    }
    
    render(){
        return(
            <div>I am a class</div>
        )
    }
}
```

## Functions

Use ES6 arrow functions unless `this` needs to be scoped.

```jsx
let members =
    [
        {
            name: 'seulki',
            group:'Red Velvet'
        },
        {
            name: 'chorong',
            group:'A Pink'
        }
    ];

let findSeulki = (members) => {
    for(let i = 0; i < members.length; i++) {
        if(members[i].name === 'seulki') {
            return members[i];
        }
    }
};

findSeulki(members);
```

## Object

```jsx
let seulki = 
    {
        name:'seulki',
        group:'Red Velvet'
    }
    
//DO NOT DO ANY OF THE FOLLOWING

let seulki = {name:'seulki', group:'Red Velvet'};

let seulki = {
        name:'seulki',
        group:'Red Velvet'
    }
```

## Array

- ***`Default`***

```jsx
let redVelvet = ['seulki', 'irene', 'yaeri', 'joy', 'wendy'];

//OR

let redVelvet = 
    [
        'seulki',
        'irene',
        'yaeri',
        'joy',
        'wendy'
    ]
    
//DO NOT

let redVelvet = [
        'seulki',
        'irene',
        'yaeri',
        'joy',
        'wendy'
    ]
```

- ***`Array of Objects`***

```jsx
//DECLARE LIKE THIS

let redVelvet = 
    [
        {
            name:'seulki',
            group:'Red Velvet'
        },
        {
            name:'irene',
            group: 'Red Velvet'
        },
        ...
    ]
    
//DO NOT DECLARE LIKE FOLLOWING

let redVelvet = [
        {
            name:'seulki',
            group:'Red Velvet'
        },
        {
            name:'irene',
            group: 'Red Velvet'
        },
        ...
    ]
    
let redVelvet = [{
            name:'seulki',
            group:'Red Velvet'
        }, {
            name:'irene',
            group: 'Red Velvet'
        },
        ...
    ]
```

## Spread ES7 syntax


- ***`Objects`***

```jsx
let seulki =
    {
        name:'seulki',
        group:'Red Velvet'
    };
    
let seulkiUpdated = 
    {
        ...seulki,
        age:25
    };
```

- ***`Arrays`***

```jsx
let redVelvet = (seulki, irene, joy, yaeri, wendy) => {
    return [seulki, irene, joy, yaeri, wendy];
};

let members =
    [
        {
            name: 'seulki',
            group: 'Red Velvet'
        },
        {
            name: 'irene',
            group: 'Red Velvet'
        },
        {
            name: 'joy',
            group: 'Red Velvet'
        },
        {
            name: 'yaeri',
            group: 'Red Velvet'
        },
        {
            name: 'wendy',
            group: 'Red Velvet'
        },
    ];

redVelvet(...members);
```

## Exports <a id="basics-exports"></a>

- ***`Default Components`***


```jsx
import React from 'react';

export default class ExampleComponent extends React.Component{
    render(){
        return(
            <div>Red Velvet</div>
        )
    }
}
```

- ***`Material UI Components`***

```jsx
import React from 'react';
import {withStyles} from 'material-ui/styles';

const styles = theme => ({
    root: {}
});

class MaterialUiClass extends React.Component{
    render(){
    
        let {classes} = this.props;
    
        return(
            <div className={classes.root}>Red Velvet Seulki</div>
        )
    }
}

export default withStyles(styles)(MaterialUiClass);
```

- ***`React Redux Components`***

```jsx

import React from 'react';
import {connect} from 'react-redux'
import {yourAction} from './path/to/action';

class MaterialUiClass extends React.Component {
    render() {
        return (
            <div>Red Velvet Seulki</div>
        )
    }
}

function mapStateToProps(state) {
    return {
        redVelvet: state.sm.redVelvet
    }
}

export default connect(mapStateToProps, {yourAction})(MaterialUiClass);
```

- ***`React Redux with Material UI Components`***

```jsx
import React from 'react';
import {connect} from 'react-redux'
import {withStyles} from 'material-ui/styles';
import {yourAction} from './path/to/action';

const styles = theme => ({
    root: {}
});

class MaterialUiClass extends React.Component {
    render() {
        return (
            <div>Red Velvet Seulki</div>
        )
    }
}

function mapStateToProps(state) {
    return {
        redVelvet: state.sm.redVelvet
    }
}

export default withStyles(styles)(connect(mapStateToProps, {yourAction})(MaterialUiClass))
```

## Imports <a id="basics-imports"></a>

- ***`Default`***

```jsx
import React from 'react';
import module from './path/to/module';

//Do not use require. For example.
const React = require('react');
```

- ***`ES6 Imports`***

```jsx
import {connect} from 'react-redux';

//Do not use require. For example
const connect = require('react').connect;
```

- ***`Material UI Component Imports`***

Import the components of the same class using `ES6 syntax`

```jsx
import Avatar from 'material-ui/Avatar';
import List, { ListItem, ListItemAvatar, ListItemText } from 'material-ui/List';
```

## Asynchronous Requests

Use the `axios` library as the standard HTTP(S) communication with the server. Only use `async/await` for asynchronous requests. Try to minimize the indentation as much as possible.

-***`Default`***
```jsx
import React from 'react';
import axios from 'axios';

class AsyncRequest extends React.Component {

	//Use Asyn/Await for every async requests.
	async retrieveAsyncData(){
    	try{
    		let response = axios.get('/path/to/the/api');
        }catch(e){
        	//TODO error handling
        }
    }
    
    //DO NOT directly use promises or callbacks. For Example
    retrieveAsyncData(){
    	axios.get('/path/to/the/api').then((response)=>{
        	console.log(response)
        })
        
        //OR
        axios.get('/path/to/the/api', (response)=>{
        	console.log(response)
        })

    }

    render() {
        return (
            <div>Red Velvet Seulki</div>
        )
    }
}
```

-***`Async/Awaitifying`***

If `promise` return is not available in certain package or function, convert it into a promise yourself in the `services` directory.

```jsx
let timeoutFunction = () => {
	return new Promise((resolve, reject) => {
    	setTimeout(resolve, 3000);
    })
}

//Then use as async/await like below
let asyncFunction = async () => {
	await timeoutFunction();
}
```

## Action Types

Each action type is exported as a `const`. All actions are imported together with `import * as TYPES from '/path'` and individual types are fetched by `TYPES.[actionType]`

-***`Exports`***

```jsx
/**
 * Auth Types
 * */
export const REGISTERED_USER = 'registered_user';
export const LOGIN_SUCCESS = 'login_success';
export const LOGOUT_USER_SUCCESS = 'logged_out_user';

/**
 * Profile
 * */
export const FETCHED_MY_PROFILE = 'fetched_my_profile';
export const FETCHED_SPONSOR_PROFILE = 'fetched_sponsor_profile';
export const FETCHED_PROFILE_GRAPH_DATA = 'fetched_profile_graph_data';
export const FETCHED_PROFILE_TABLE_DATA = 'fetched_profile_table_data';

/**
 * Account
 * */
export const FETCHED_ACCOUNTS_DATA = 'fetched_accounts_data';

/**
 * Snackbar
 * */
export const OPEN_SNACKBAR = 'open_snackbar';
export const CLOSE_SNACKBAR = 'clsoe_snackbar';

/**
 * Transaction
 * */
export const FETCHED_TRANSACTION_TREND = 'fetched_transaction_trend';
export const FETCHED_TRANSACTION_HISTORY = 'fetched_transaction_history';
```

-***`Imports`***

```jsx
import * as TYPES from './path/to/types';

//Use like following
dispatch({type:TYPES.FETCHED_TRANSACTION_TREND, payload:data});
```
## Actions and Reducers

- ***`Actions`***

Always use action types constants as the `dispatch` type so as to make sure there is no overlap in the type naming. Make all server requests through `actions` and `reducers` instead of directly using `axios` within `components` or `containers` for better code organization.

```jsx
import axios from 'axios';
import * as TYPES from './types';

export function registerUser(username, password, referee, account) {

    return async dispatch => {
    	try{
          let response = await axios.post(`/api/auth/register`, {username, password, referee, account});

          if(response.status !== 200){
              //TODO error handling
          }

          /**
          * Response
          *  {
          *      error: {
          *          stack: String,
          *          message: String
          *      },
          *      success: Boolean,
          *      data: Object
          *  }
          * */

          dispatch({type: TYPES.REGISTERED_USER, payload: response})
      }catch(e){
      	//TODO error handling
      }
    }
}
```

- ***`Reducers`***

Remmeber to use only pure functions for `redux`

```jsx
import * as TYPES from '../actions/types';

export default function (state = {}, action) {
    switch (action.type) {

        /**
         * Register Payload
         *  {
         *      error: {
         *          stack: String,
         *          message: String
         *      },
         *      success: Boolean,
         *      data: Object
         *  }
         * */

        case TYPES.REGISTERED_USER:
            return {
                ...state,
                data:action.payload.data
            };

        default:
            return state;
    }
}
```

-***`Combining Reducers`***

For the convenience of retrieval and usage, use `combineReducers` to maintain different set of states for each `reducer`

```jsx
import authReducer from './authReducer';

export default combineReducers({
	//Result from authReducer will be available at path state.auth.[key]
    auth: authReducer
})
```

