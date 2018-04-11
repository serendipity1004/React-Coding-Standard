# React Coding Standard

## Table of Contents

1. [Basics](#basics)
    1. [Declarations](#basics-variables)
    2. [Exports](#basics-exports)
    3. [Imports](#basics-imports)


## Basics <a id="basics"></a>

### 1. Declarations <a id="basics-variables"></a>

### `Declaration`

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

### `Functions`

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

### `Object`

1. `Default`

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

### `Array`

1. `Default`

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

2. `Array of Objects`

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

### `Spread ES7 syntax`

1. `Spread All`

#### `Objects`

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

#### `Arrays`

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

### Exports <a id="basics-exports"></a>

### `Components`

1. `Default Component`

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

2. `Material UI Component`

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

3. `React Redux`

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

4. `React Redux with Material Ui`

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

### `Action Types`

Each action type is exported as a `const`. All actions are imported together with `import * as TYPES from '/path'` and individual types are fetched by `TYPES.[actionType]`

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

### Imports <a id="basics-imports"></a>

