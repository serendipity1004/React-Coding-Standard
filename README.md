# React Coding Standard

## Table of Contents

1. [Basics](#basics)
    1. [Variables](#basics-variables)


## Basics <a id="basics"></a>

### Variables <a id="basics-variables"></a>

Variable declaration is always done with `let`. `var` jeorpardizes the restridcted scope provided by `let` so it will never be used unless it is absolutely necessary.

#### Example

```jsx
import react from 'react';

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