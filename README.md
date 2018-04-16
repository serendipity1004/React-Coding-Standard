# React Coding Standard

## Table of Contents

... In Progress

## FS

```
. root
+-- public
+-- src
    +-- assets //all assets that are directly imported to the page
        +-- img //images
    +-- components //React component instances that do not interact directly with redux
        +-- componentName //General name of a group of components e.g. Cards
            +-- componentName.js //JS file of the specific component e.g. ChartCard.js
        +-- index.js //Where all components get import and exported all together
    +-- containers //These are React components that interact directly with redux
        +-- containerName
            +-- containerName.js
    +-- routes
        +-- routeTarget.js //Where the routes will be imported to
        +-- index.js //Where all the routes under routes folder will be imported and exported all together
    +-- views //Views contain all the components and containers in a specific page.
        +-- ViewName //Camel casing with captial start
            +-- Viewname.js //Camel casing with capital start
```


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

## Exports <a id='basics-exports'></a>

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

## Imports <a id='basics-imports'></a>

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

- ***`Default`***
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

- ***`Async/Awaitifying`***

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

## Class PropTypes

Define all props of class using `prop-types`

```jsx
import React from 'react';
import {
    withStyles,
    Card,
    CardContent,
    CardHeader,
    CardActions,
    Typography
} from 'material-ui';
import PropTypes from 'prop-types';

import chartCardStyle from 'variables/styles/chartCardStyle';

function ChartCard({...props}) {
    const {
        classes,
        chartColor,
        statIconColor,
        chart,
        title,
        text,
        statLink,
        statText
    } = props;

    return (
        <Card className={classes.card}>
            <CardHeader
                className={
                    classes.cardHeader + ' ' + classes[chartColor + 'CardHeader']
                }
                subheader={chart}
            />
            <CardContent className={classes.cardContent}>
                <Typography variant='title' component='h4' className={classes.cardTitle}>
                    {title}
                </Typography>
                <Typography component='p' className={classes.cardCategory}>
                    {text}
                </Typography>
            </CardContent>
            <CardActions className={classes.cardActions}>
                <div className={classes.cardStats}>
                    <props.statIcon
                        className={
                            classes.cardStatsIcon +
                            ' ' +
                            classes[statIconColor + 'CardStatsIcon']
                        }
                    />
                    {' '}
                    {statLink !== undefined ? (
                        <a href={statLink.href} className={classes.cardStatsLink}>
                            {statLink.text}
                        </a>
                    ) : statText !== undefined ? (
                        statText
                    ) : null}
                </div>
            </CardActions>
        </Card>
    );
}

ChartCard.defaultProps = {
    statIconColor: 'gray',
    chartColor: 'purple'
};

ChartCard.propTypes = {
    classes: PropTypes.object.isRequired,
    chart: PropTypes.object.isRequired,
    title: PropTypes.node,
    text: PropTypes.node,
    statIcon: PropTypes.func.isRequired,
    statIconColor: PropTypes.oneOf([
        'warning',
        'primary',
        'danger',
        'success',
        'info',
        'rose',
        'gray'
    ]),
    chartColor: PropTypes.oneOf(['orange', 'green', 'red', 'blue', 'purple']),
    statLink: PropTypes.object,
    statText: PropTypes.node
};

export default withStyles(chartCardStyle)(ChartCard);
```

## Action Types

Each action type is exported as a `const`. All actions are imported together with `import * as TYPES from '/path'` and individual types are fetched by `TYPES.[actionType]`

- ***`Exports`***

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

- ***`Imports`***

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

- ***`Combining Reducers`***

For the convenience of retrieval and usage, use `combineReducers` to maintain different set of states for each `reducer`

```jsx
import authReducer from './authReducer';

export default combineReducers({
	//Result from authReducer will be available at path state.auth.[key]
    auth: authReducer
})
```

## Managing Routes

- ***`views/RedVelvet/Seulki.js`***

Create view container using components (notice that views can act as containers and has access to `redux`)

```jsx
import React from 'react';
import {connect} from 'react-redux';

import {
    //import all components
} from 'components';

import seulkiStyle from 'variables/styles/seulkiStyle';

class Seulki extends React.Component {

  render() {
    return (
      <div>
        I am Seulki
      </div>
    );
  }
}

fucntion mapStateToProps(){
    return {
        //State declaration
    }
}

export default withStyles(seulkiStyle)(connect(mapStateToProps)(Seulki));
```

- ***`routes/app.js`***

import all the views from 'views' folder

```jsx
import SeulkiPage from 'views/Seulki/Seulki.js';
import IrenePage from 'views/Irene/Irene.js';

//We may introduce more properties here but that is for future discussion
const appRoutes = [
  {
    path:'/seulki',
    component:SeulkiPage
  },
  {
    path:'/irene',
    component:IrenePage
  }
];

export default appRoutes;
```

- ***`containers/App/App.js`***

Map routes to `Route` components

```jsx
import appRoutes from 'routes/app.jsx'
import {Switch, Route} from 'react-router-dom'

const switchRoutes = (
    <Switch>
        {appRoutes.map((route, index)=>{
            <Route path={route.path} component={prop.component} key={index}/>
        })}
    </Switch>
)

export default class App extends React.Component {
    render(){
        <div>
            {switchRoutes}
        </div>
    }
}
```