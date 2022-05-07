# Higher Order Array Methods

### Array.map()

```javascript
const arr = [1, 2, 3, 4]
const map = arr.map(item => item * 2)
console.log(map)
//expected output: [2, 4, 6, 8]
```

### Array.filter()

```javascript
const arr = [1, 2, 3, 4]
const filter = arr.filter(item => item > 2)
console.log(filter)
//expected output: [3, 4]
```

### Array.reduce()

```javascript
    const arr = [1, 2, 3, 4]
    const initialValue = 0
    const reduce = arr.reduce((accumulator, currentValue) => return accumulator + currentValue, initialValue)
    console.log(reduce)
    //expected output: 10
```

### Array.find()

```javascript
const arr = [1, 2, 3, 4]
const find = arr.find(item => item > 2)
console.log(find)
//expected output: 3
```

&nbsp;

# Other Useful Methods

### Spread Operator

```javascript
const arr = [1, 2, 3, 4]
const newValue = 5
const spread = [...arr, newValue]
console.log(spread)
//expected output: [1, 2, 3, 4, 5]
```

&nbsp;

# React Router

### Using Router

```javascript
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom'

return (
  <Router>
    <Routes>
      {/* single component*/}
      <Route exact path='/' element={<Component />} />

      {/* multiple components*/}
      <Route
        exact
        path='/about'
        element={
          <>
            <Component1 />
            <Component2 />
            <Component3 />
          </>
        }
      />
    </Routes>
  </Router>
)
```

### Using Link

```javascript
    import { Link } from 'react-router-dom'


    return (

        //simple
        <Link to='/'>Home</Link>

        //with query
        <Link
            to={{
                pathname: '/about'
                search: '?sort=name'
                hash: '#33'
            }}

        >

        </Link>
    )
```

### NavLink

```javascript
import { NavLink } from 'react-router-dom'

return <NavLink to='/' activeClassName='active'></NavLink>
```

### Using Params

#### In routes

```javascript
return <Route path='/post/:id/:name' element={<Post />} />
```

#### In Page

```javascript
    import { useParams } from 'react-router-dom'

    const Post = () => {
        const params = useParams();

        return (
            <h1>Post #{params.id}</h1>
            <h1>Post #{params.name}</h1>
        )
    }
```

### Navigate

```javascript
import { Navigate, useNavigate, useLocation } from 'react-router-dom'
const Post = () => {
  //for redirect
  if (status === 404) return <Navigate to='/notfound' />

  //for event
  navigate = useNavigate()
  const handleClick = () => Navigate('/about')

  //navigate to where they came from
  const location = useLocation()
  const from = location.state?.from?.pathname || '/'
  navigate(from, { replace: true })

  return <Button onClick={handleClick}>Click Me</Button>
}
```

### Nested Routes

#### In Routes

```javascript
return <Route path='/post/*' element={<Post />} />
```

#### In Page

```javascript
return (
  <Routes>
    <Route path='/subpost' element={<SubPost />} />
  </Routes>
)
```

&nbsp;

# Protected Routes

### PrivateRoute.js

```javascript
import { useLocation, Navigate, Outlet } from 'react-router-dom'

const PrivateRoute = () => {
  //bring auth from somewhere
  const location = useLocation()

  return auth?.user ? (
    <Outlet />
  ) : (
    <Navigate to='/login' state={{ from: location }} replace />
  )
}

export default PrivateRoute
```

### Protect Routes

```javascript
<Route element={<PrivateRoute />}>
  <Route path='/' element={<Component1 />} />
  <Route path='/2' element={<Component2 />} />
  <Route path='/3' element={<Component3 />} />
</Route>
```

&nbsp;

# API Request

## API Template

```javascript
import axios from 'axios'
import { baseURL } from '../config'

export const APITemplate = async (method, url, data) => {
  try {
    const res = await axios({
      method,
      url: `${baseURL}${url}`,
      data,
      headers: {
        Authorization: Auth,
        'Content-Type': 'application/json',
      },
    })
    return res
  } catch (err) {
    console.error(err)
  }
}
```

## API Call Example

```javascript
const postCall = async () => {
  const url = '/someEndpoint'
  const data = {
    data1: 'someData',
  }
  const res = await APITemplate('post', url, data)
}
```

&nbsp;

# Context API

### Context File

```javascript
import { createContext, useState } from 'react'

const AnyContext = createContext();

export const AnyProvider = ({ children }) => {
  const [state, setState] = useState()
  //any other states
})

//any methods that change any states
  return (
    <AnyContext.Provider
      value={{
        state,
        {/*along with other states or methods*/}
      }}
    >
      {children}
    </AnyContext.Provider>
  )
```

### App.js

```javascript
import { AnyProvider } from './context/AnyContext'

function App() {
  return (
    <AnyProvider>
      <Component1 />
      <Component2 />
      <Component3 />
    </AnyProvider>
  )
}
```

### Inside Component

```javascript
import { useContext } from 'react'
import AnyContext from '../context/AnyContext'

function Component() {
  const { state } = useContext(AnyContext)
  //pullout any other state or methods too
}
```

&nbsp;

# useRef()

```javascript
import { useRef } from 'react'

function Component() {
  const myRef = useRef()
  const handleClick = () => {
    myRef.current.innerText = 'WHY??'
  }
  return (
    <button ref={myRef} onClick={handleClick}>
      Don't Click
    </button>
  )
}
```

> Pro tip: You can also use useRef() to auto foucs like in useEffect() you can auto focus on the form first field

&nbsp;

# useEffect Cleanup

```javascript
function Component() {
  useEffect(() => {
    let isMounted = true
    const controller = new AbortController()
    //API Call
    if (isMounted.current) setState(res)
    return () => {
      isMounted = false
      controller.abort()
    }
  })
}
```

&nbsp;

# Redux

### Store.js

```javascript
import { configureStore } from '@reduxjs/toolkit'
import rootReducer from './rootReducer'

export default configureStore({
  reducer: rootReducer,
})
```

### rootReducer

```javascript
import { combineReducers } from 'redux'
import someSlice from './slices/someSlice'

export default combineReducers({
  someSlice,
})
```

### rootReducer

```javascript
import { createSlice } from '@reduxjs/toolkit'

const slice = createSlice({
  name: 'someSlice',
  initialState: {},
  reducers: {
    DO_SOMETHING: (state, action) => {
      return {
        ...state,
        data: action.payload,
      }
    },
  },
})

export const { DO_SOMETHING } = slice.actions
export default slice.reducer
```

### Action

```javascript
import { DO_SOMETHING } from '../slices/someSlice'
export const someAction = data => async dispatch => {
  //API Call or Other Stuff
  dispatch(DO_SOMETHING(data))
}
//another action
```

### App.js

```javascript
import { Provider } from 'react-redux'
import store from './redux/store'

function App() {
  return <Provider store={store}>{/*Other components goes here*/}</Provider>
}
```

### Inside Component

```javascript
import { useSelector, useDispatch } from 'react-redux'
import { someAction } from '../redux/actions/someAction'

function Component() {
  const dispatch = useDispatch()
  const someData = useSelector(state => state.someThing.someData)
  dispatch(someAction('someData'))
}
```

&nbsp;
