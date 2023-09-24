# redux-toolkit

## step-1

### store.js

```js
import {configureStore} from '@reduxjs/toolkit'
import { customReducer } from './Reducers'


const store = configureStore({
    reducer:{
        custom:customReducer
    }
})

export default store
```

#### Now if you've created the store then

## step-2
### Reducer.js

```js

import {createReducer} from '@reduxjs/toolkit'

const initialState = {
    c:0
}

export const customReducer = createReducer(initialState,{
    increment:(state) =>{
        state.c += 1
    },
    incrementByValue:(state,action) =>{
      //  state.c += 1
        state.c += action.payload
    },
    decrement:(state) =>{
        state.c -= 1
    }
})
```

#### within store we've passing customReducer as reducer and used that customReducer for createReducer in 
## Reducer.js file.

#### Now, In the below Components 
## Home.jsx
#### We're dispatching the methodtype and their payload to Reducer.js for further manipulation.

```js
import React from 'react'
import {useDispatch} from 'react-redux'

const Home = () => {
   // const {c} = useSelector((state)=>state.custom)

const dispatch = useDispatch()

const addBtn = () =>{
dispatch({type:"increment"})
}


const addBtn25 = () =>{
    dispatch({
        type:'incrementByValue',
        payload:25
    })
}

const subBtn = () =>{
    dispatch({type:"decrement"})
    }

  return (
    <div>
        {/* <h2>{value}</h2> */}
        <button onClick={addBtn}>Increment</button>
        <button onClick={addBtn25}>IncrementBy25</button>
        <button onClick={subBtn}>Decrement</button>
    </div>
  )
}

export default Home
```

#### Now the last component is 
## App.js
#### And it contains
### useSelector
hook for getting the manipulated data on Screen

```js

import Home from './Home'
import {useSelector} from 'react-redux'
import './App.css';

function App() {
  const {c} = useSelector((state) => state.custom)
  return (
    <div>
      <h1>{c}</h1>
      <Home />
    </div>
  );
}

export default App;

```

#### Now add 
### Provider
#### to
## index,js 
#### file , so that the store is accessible to all components

```js

import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { Provider } from "react-redux";
import store from "./store";


const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);

```


