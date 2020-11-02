# Junyi Frontend Snippets

## `jc` - Basic React Component

```javascript
/**
 * Copyright (c) 2020 Junyi Academy.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */

import React from 'react'
import PropTypes from 'prop-types'
import { makeStyles } from '@material-ui/core/styles'

// utils

// assets

// components

// self-defined-configs

// self-defined-components
const useStyles = makeStyles(
  (theme) => ({
    root: {},
  }),
  { name: 'App' }
)

const App = ({}) => {
  const classes = useStyles()

  return <div className={classes.root} />
}

App.propTypes = {}

export default App
```

## `jcr` - Basic React Component with redux

```javascript
/**
 * Copyright (c) 2020 Junyi Academy.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */

import React from 'react'
import PropTypes from 'prop-types'
import { connect } from 'react-redux'
import { bindActionCreators } from 'redux'

// utils

// assets

// selectors

// actions

// components
import AppComponent from '../components/App'

// self-defined-configs

// self-defined-components
const App = ({}) => {
  return <AppComponent />
}

App.propTypes = {}

const mapStateToProps = (state) => ({})

const mapDispatchToProps = (dispatch) => bindActionCreators({}, dispatch)

export default connect(mapStateToProps, mapDispatchToProps)(App)
```

## `jcut` - Unit Test for React Component

```javascript
/**
 * Copyright (c) 2020 Junyi Academy.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */

import React from 'react'
import userEvent from '@testing-library/user-event'

// utils
import { render, screen } from '@/tests'

// components
import App from '../App'

test('render App', () => {
  // Arrange
  const options = {
    initialState: {},
  }

  render(<App />, options)

  // Assert

  // Alert
})
```

## `jcutapi` - Unit Test for React Component with API mock

```javascript
/**
 * Copyright (c) 2020 Junyi Academy.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */

import React from 'react'
import { rest } from 'msw'
import { setupServer } from 'msw/node'
import userEvent from '@testing-library/user-event'

// utils
import { render, waitFor, screen } from '@/tests'

// components
import App from '../App'

// setup
const server = setupServer(
  rest.get('/greeting', (req, res, ctx) => {
    return res(ctx.json({ greeting: 'hello there' }))
  })
)

beforeAll(() => server.listen())
afterEach(() => server.resetHandlers())
afterAll(() => server.close())

test('render App', () => {
  // Arrange
  const options = {
    initialState: {},
  }

  render(<App />, options)

  // Assert

  // Alert
})

test('handlers server error', async () => {
  // Arrange
  server.use(
    // override the initial 'GET /greeting' request handler
    // to return a 500 Server Error
    rest.get('/greeting', (req, res, ctx) => {
      return res(ctx.status(500))
    })
  )

  const options = {
    initialState: {},
  }

  render(<App />, options)

  // Assert

  // Alert
})
```

## `jsl` - Redux Slice

```javascript
/**
 * Copyright (c) 2020 Junyi Academy.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */

import { createSlice, createAction } from '@reduxjs/toolkit'

const namespace = 'foo'
const initialState = {
  foo: '',
}

const fooSlice = createSlice({
  name: namespace,
  initialState,
  reducers: {
    doSomeThing: (state, action) => {
      const { foo } = action.payload
      state.foo = foo
    },
  },
})

fooSlice.asyncActions = {
  doOtherThingAsync: createAction(`${namespace}/doOtherThingAsync`),
}

export const { doSomeThing } = fooSlice.actions

export const { doOtherThingAsync } = fooSlice.asyncActions

export const { reducer } = fooSlice
```

## `jep` - Redux Observable Epic

```javascript
/**
 * Copyright (c) 2020 Junyi Academy.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */

import { combineEpics, ofType } from 'redux-observable'
import { of, from } from 'rxjs'
import { map, switchMap, catchError } from 'rxjs/operators'

import {
  getAsync,
  getSuccess,
  getFailure,
  postAsync,
  postSuccess,
  postFailure,
} from './slice'

export const postEpic = (action$, state$, { post }) =>
  action$.pipe(
    ofType(postAsync.type),
    switchMap(() =>
      from(post('/api/foo', { foo: 'bar' })).pipe(
        map((response) => postSuccess(response)),
        catchError((error) => of(postFailure(error)))
      )
    )
  )

export const getEpic = (action$, state$, { get }) =>
  action$.pipe(
    ofType(getAsync.type),
    switchMap(() =>
      from(get('/api/foo', { foo: 'bar' })).pipe(
        map((response) => getSuccess(response.data)),
        catchError((error) => of(getFailure(error)))
      )
    )
  )

export default combineEpics(postEpic, getEpic)
```

## `jsc` - Material styled Component with consuming props pattern

```javascript
const StyledDiv = styled(({ foo: _foo, ...other }) => <div {...other} />)(
  ({ foo }) => ({}),
  { name: StyledDiv }
)
```

## `jcl` - Copyright and License

```javascript
/**
 * Copyright (c) 2020 Junyi Academy.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */
```
