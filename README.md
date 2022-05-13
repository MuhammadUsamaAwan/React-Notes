# React

## JavaScript Refresher

### Array.map()

```js
const arr = [1, 2, 3, 4]
const map = arr.map(item => item * 2)
console.log(map)
// Output: [2, 4, 6, 8]
```

### Array.filter()

```js
const arr = [1, 2, 3, 4]
const filter = arr.filter(item => item > 2)
console.log(filter)
// Output: [3, 4]
```

### Array.reduce()

```js
const arr = [1, 2, 3, 4]
const initialValue = 0
const reduce = arr.reduce((accumulator, currentValue) => return accumulator + currentValue, initialValue)
console.log(reduce)
// Output: 10
```

### Array.find()

```js
const arr = [1, 2, 3, 4]
const find = arr.find(item => item > 2)
console.log(find)
// Output: 3
```

### Spread Operator

```js
const arr = [1, 2, 3, 4]
const newValue = 5
const spread = [...arr, newValue]
console.log(spread)
// Output: [1, 2, 3, 4, 5]
```

<br>

## Styling in React

### Inline Styling

```js
return <label style={{ color: !isValid ? 'red' : 'black' }}>Course Goal</label>
```

### Dynamic CSS Class

```js
return (
  <label classname={{ !isValid ? "invalid" : "valid" }}>Course Goal</label>
)
```

### Styled Components

```
npm i styled-components
```

#### Container.styled.js

```js
import styled from "styled-components";
export const Container = styled.div`
  padding: ${props => props.variant === 'sm' : '0 20px' ? '0 30px'};
  max-width: 100%;
  width: 1000px;
  margin: 0 auto;
`;
```

#### Button.styled.js

```js
import styled from 'styled-components'
export const Button = styled.button`
  padding: 0.5rem 1.5rem;
  color: ${props => props.color};
  background: #8b005d;

  &:hover,
  &:active {
    background: #ac0e77;
  }
`
```

#### App.js

```js
import { Container } from './Container.styled.js'
import { Button } from './Button.styled.js'
const App = () => {
  return (
    <Container variant={sm}>
      <Button color={white} />
    </Container>
  )
}
```

#### Theme Provider

##### App.js

```js
import { ThemeProvider } from 'styled-components'

const theme = {
  colors: {
    header: '#ebfbff',
    body: '#fff',
  },
}
// wrap around ThemeProvider theme={theme}
```

##### Inside Syled Components

```js
${theme => theme.colors.header}
```

### CSS Modules

#### Button.module.css

```js
.button {
    // your button css here
}
```

#### Button.js

```js
import styles from './Button.module.css'
return <button classname={styles.button}>Button</button>
```

<br>

## React Portals

### index.html

```html
<div id="overlay"></div>
```

### Model.js

```js
import ReactDom from 'react-dom'

return ReactDom.createPortal(
    // your code here
), document.getElementById('overlay')
)
```

<br>

## React Hooks

### useEffect()

#### Diable Annoying Dependency Warning

```js
// eslint-disable-next-line
```

#### Cleanup

```js
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
```

### useRef()

```JavaScript
import { useRef } from 'react'

const Component = () => {
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

### useReducer()

```js
const reducer(state, action) {
    switch(action.type) {
        case 'increment':
            return state + 1
        case 'decrement':
            return state + 2
        default:
            throw new Error()
    }
}

const App = () => {
    const [state, dispatch] = useReducer(reducer, initialState)
    return (
        Count: {state}
        <button onClick={() => dispatch({type: 'decrement'})}>-</button>
        <button onClick={() => dispatch({type: 'increment'})}>+</button>
    )
}
```

### useMemo()

```js
const expensiveCount = useMemo(() => {
  return count * 2
}, [count])
```

### useCallback()

```js
const showCount = useCallback(() => {
    alert(`Count ${count}`)
}. [count])
```

<br>

### Custom Hooks

```js
import { useState } from "react"

export default const useToggle = (defaultValue)  => {
  const [value, setValue] = useState(defaultValue)

  const toggleValue = (value) => {
    setValue(currentValue =>
      typeof value === "boolean" ? value : !currentValue
    )
  }

  return [value, toggleValue]
}
```

<br>

## Context API

### Context File

```js
import { createContext, useState } from 'react'

const AnyContext = createContext();

export const AnyProvider = ({ children }) => {
  const [state, setState] = useState()
  // any other states
  // any methods that change any states
  return (
    <AnyContext.Provider
      value={{
        state,
        {/* along with other states or methods */}
      }}
    >
      {children}
    </AnyContext.Provider>
  )
}
```

### App.js

```js
import { AnyProvider } from './context/AnyContext'

const App = () => {
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

```js
import { useContext } from 'react'
import AnyContext from '../context/AnyContext'

const Component = () => {
  const { state } = useContext(AnyContext)
  // pullout any other state or methods too
}
```

<br>

## API Request

### api/axios.js

```js
import axios from 'axios'

export default axios.create({
  baseURL: 'http://localhost:3500',
})
```

### GetAPI

```js
import axios from './api/axios'
import { baseURL } from '../config'

export const GetAPI = async url => {
  try {
    const res = await axios({
      method: 'get',
      url,
      withCredentials: true,
    })
    return res
  } catch (err) {
    console.error(err)
  }
}
```

### PostAPI

```js
import axios from './api/axios'
import { baseURL } from '../config'

export const PostAPI = async (url, data) => {
  try {
    const res = await axios({
      method: 'post',
      url,
      data,
      headers: {
        Authorization: Auth,
        'Content-Type': 'application/json',
      }
      withCredentials: true
    })
    return res
  } catch (err) {
    console.error(err)
  }
}
```

### API Call Example

```js
const postCall = async () => {
  const url = '/someEndpoint'
  const data = {
    name: 'someName',
  }
  const res = await PostAPI(url, data)
}
```

<br>

## Redux

### Store.js

```js
import { configureStore } from '@reduxjs/toolkit'
import rootReducer from './rootReducer'

export default configureStore({
  reducer: rootReducer,
})
```

### rootReducer

```js
import { combineReducers } from 'redux'
import someSlice from './slices/someSlice'

export default combineReducers({
  someSlice,
})
```

### Slice

```js
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

```js
import { DO_SOMETHING } from '../slices/someSlice'
export const someAction = data => async dispatch => {
  // API Call or Other Stuff
  dispatch(DO_SOMETHING(data))
}
// another action
```

### App.js

```js
import { Provider } from 'react-redux'
import store from './redux/store'

const App = () => {
  return <Provider store={store}>{/*Other components goes here*/}</Provider>
}
```

### Inside Component

```js
import { useSelector, useDispatch } from 'react-redux'
import { someAction } from '../redux/actions/someAction'

const Component = () => {
  const dispatch = useDispatch()
  const someData = useSelector(state => state.someThing.someData)
  dispatch(someAction('someData'))
}
```

<br>

## React Router

### Using Router

```js
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom'

return (
  <Router>
    <Routes>
      {/* single component*/}
      <Route exact path="/" element={<Component />} />

      {/* multiple components*/}
      <Route
        exact
        path="/about"
        element={
          <>
            <Component1 />
            <Component2 />
            <Component3 />
          </>
        }
      />

      {/* not found */}
      <Route path="*" element={<NotFound />}>
    </Routes>
  </Router>
)
```

### Lazy Loading

```js
import { Suspense } from 'react'
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom'

const Component = React.lazy(() => import('./components/component'))

return (
  <Suspense fallback={<LoadingSpinner />}>
    <Router>
      <Routes>
        <Route exact path='/' element={<Component />} />
      </Routes>
    </Router>
  </Suspense>
)
```

### Using Link

```js
    import { Link } from 'react-router-dom'


    return (

        // simple
        <Link to='/'>Home</Link>

        // with query
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

```js
import { NavLink } from 'react-router-dom'

return <NavLink to='/' activeClassName='active'></NavLink>
```

### Using Params

#### In routes

```js
return <Route path='/post/:id/:name' element={<Post />} />
```

#### In Page

```js
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

```js
import { Navigate, useNavigate, useLocation } from 'react-router-dom'
const Post = () => {
  // for redirect
  if (status === 404) return <Navigate to='/notfound' />

  // for event
  navigate = useNavigate()
  const handleClick = () => Navigate('/about')

  // navigate to where they came from
  // useful for successful login
  const location = useLocation()
  const from = location.state?.from?.pathname || '/'
  navigate(from, { replace: true })
  // another way
  const goBack = () => navigate(-1)

  return <Button onClick={handleClick}>Click Me</Button>
}
```

### Nested Routes

#### In Routes

```js
return <Route path='/post/*' element={<Post />} />
```

#### In Page

```js
return (
  <Routes>
    <Route path='/subpost' element={<SubPost />} />
  </Routes>
)
```

<br>

## React Authentication

### useAuth

```js
import { useContext } from 'react'
import AuthContext from '../context/AuthProvider'

const useAuth = () => {
  return useContext(AuthContext)
}

export default useAuth
```

### Protected Routes

#### PrivateRoute.js

```js
import { useLocation, Navigate, Outlet } from 'react-router-dom'
import useAuth from '../hooks/useAuth'

const PrivateRoute = () => {
  const { auth } = useAuth()
  const location = useLocation()

  return auth?.user ? (
    <Outlet />
  ) : (
    <Navigate to='/login' state={{ from: location }} replace />
  )
}

export default PrivateRoute
```

#### Protect Routes

```js
<Route element={<PrivateRoute />}>
  <Route path='/' element={<Component1 />} />
  <Route path='/2' element={<Component2 />} />
  <Route path='/3' element={<Component3 />} />
</Route>
```

### Role-Based Protected Routes

#### PrivateRoute.js

```js
import { useLocation, Navigate, Outlet } from 'react-router-dom'
import useAuth from '../hooks/useAuth'

const PrivateRoute = ({ allowredRoles }) => {
  const { auth } = useAuth()
  const location = useLocation()

  return auth?.roles?.find(role => allowedRoles?.includes(role)) ? (
    <Outlet />
  ) : auth?.user ? (
    <Navigate to='/unauthorized' state={{ from: location }} replace />
  ) : (
    <Navigate to='/login' state={{ from: location }} replace />
  )
}

export default PrivateRoute
```

#### Protect Routes

```js
// better to store role codes in config
<Route element={<PrivateRoute allowedRoles={{2001}}/>}>
  <Route path="/" element={<Component1 />} />
</Route>

<Route element={<PrivateRoute allowedRoles={{1984}}/>}>
  <Route path="/2" element={<Component2 />} />
</Route>

<Route element={<PrivateRoute  allowedRoles={{1984, 5150}}/>}>
  <Route path="/3" element={<Component3 />} />
</Route>
```
