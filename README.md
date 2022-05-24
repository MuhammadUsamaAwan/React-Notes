# React

## Javascript Refresher

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

### Array.findIndex()

```js
const arr = [1, 2, 3, 4]
const find = arr.findIndex(item => item > 2)
console.log(find)
// Output: 2
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

### 1. Inline Styling

```js
return <label style={{ color: !isValid ? 'red' : 'black' }}>Course Goal</label>
```

### 2. Dynamic CSS Class

```js
return (
  <label classname={{ !isValid ? "invalid" : "valid" }}>Course Goal</label>
  <label classname={{ !isValid && "invalid" }}>Course Goal</label>
)
```

### 3. Styled Components

```
npm i styled-components
```

#### Container.styled.js

```js
import styled from 'styled-components'
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

### 4. CSS Modules

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

<br>

## React Hooks

### useState

```js
const [count, setCount] = useState(0)
const App = () => {
  const [count, setCount] = useState(0)
  return (
    <>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </>
  )
}
```

### useEffect

```js
useEffect(() => {
  // API calls or other stuff
  return () => {
    // Clean up
  }
}, [dependencies])
// eslint-disable-next-line = to diable annoying warning
```

### useReducer

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

### useCallback

```js
const showCount = useCallback(() => {
    alert(`Count ${count}`)
}. [count])
// will return a change only if dependencies changes
```

### useMemo

```js
const expensiveCount = useMemo(() => {
  return count * 2
}, [count])
```

### useRef

```js
const App = () => {
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

### useTransition

```js
const App = () => {
  const [isPending, startTransition] = useTransition()
  const [count, setCount] = useState(0)

  function handleClick() {
    startTransition(() => {
      setCount(c => c + 1)
    })
  }

  return (
    <div>
      {isPending && <Spinner />}
      <button onClick={handleClick}>{count}</button>
    </div>
  )
}
```

### useDeferredValue

```js
// similar to useTransition but when you have no control over call
const ProductList => ({ products }) = {
  const deferredProducts = useDeferredValue(products);
  return (
    <ul>
      {deferredProducts.map((product) => (
        <li>{product}</li>
      ))}
    </ul>
  );
}
```

### useId

Hook for generating unique IDs. useId is not for generating keys in a list. For multiple IDs in the same component, append a suffix using the same id

```js
const App = () => {
  const id = useId()
  return (
    <>
      <label htmlFor={id}>Do you like React?</label>
      <input id={id} type='checkbox' name='react' />
    </>
  )
}
```

### Custom Hooks

```js
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

## React.memo

```js
const MyComponent = props => {
  /* render using props */
}
const areEqual = (prevProps, nextProps) => {
  /*
  return true if passing nextProps to render would return
  the same result as passing prevProps to render,
  otherwise return false
  */
}
export default React.memo(MyComponent, areEqual)
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

return (
  ReactDom
    .createPortal
    // your code here
    (),
  document.getElementById('overlay')
)
```

<br>

## API Calls

### Axios Instance

```js
import axios from 'axios'
const BASE_URL = 'https://icanhazdadjoke.com'

export default axios.create({
  baseURL: BASE_URL,
  headers: {
    'Content-Type': 'application/json',
  },
})
```

### useAxios Custom Hook

```js
import { useState, useEffect } from 'react'

const useAxios = configObj => {
  const { axiosInstance, method, url, requestConfig = {} } = configObj

  const [response, setResponse] = useState([])
  const [error, setError] = useState('')
  const [loading, setLoading] = useState(true)
  const [reload, setReload] = useState(0)

  const refetch = () => setReload(prev => prev + 1)

  useEffect(() => {
    const controller = new AbortController()

    const fetchData = async () => {
      try {
        const res = await axiosInstance[method.toLowerCase()](url, {
          ...requestConfig,
          signal: controller.signal,
        })
        setResponse(res.data)
      } catch (err) {
        setError(err.message)
      } finally {
        setLoading(false)
      }
    }

    fetchData()

    return () => controller.abort()

    // eslint-disable-next-line
  }, [reload])

  return [response, error, loading, refetch]
}

export default useAxios
```

### Inside Component

```js
import useAxios from '../hooks/useAxios'
import axios from '../apis/axios'

const [joke, error, loading, refetch] = useAxios({
  axiosInstance: axios,
  method: 'GET',
  url: '/',
})

const [joke, error, loading, refetch] = useAxios({
  axiosInstance: axios,
  method: 'GET',
  url: '/',
  requestConfig: {
    data: {
      someData, // for post request
    },
  },
})

// for refetch simply call refetch()
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

export default AnyContext
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
        About
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
  const location = useLocation()
  const from = location.state?.from?.pathname || '/'
  navigate(from, { replace: true })
  // another way
  const goBack = () => navigate(-1)
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
