# junyi-frontend-snippets README

## React Components

### `jc`

```javascript
/** @format */

import React from "react";
import PropTypes from "prop-types";
import { makeStyles } from "@material-ui/core/styles";

// utils

// assets

// actions

// components

// self-defined-components
const useStyles = makeStyles(
  (theme) => ({
    root: {},
  }),
  { name: "App" }
);

const App = ({}) => {
  const classes = useStyles();

  return <div className={classes.root} />;
};

App.propTypes = {};

export default App;
```

### `jcr`

```javascript
/** @format */

import React from "react";
import PropTypes from "prop-types";
import { connect } from "react-redux";
import { bindActionCreators } from "redux";

// utils

// assets

// actions

// components
import AppComponent from "../components/App";

// self-defined-components

const App = ({}) => {
  return <AppComponent />;
};

App.propTypes = {};

const mapStateToProps = (state) => ({});

const mapDispatchToProps = (dispatch) => bindActionCreators({}, dispatch);

export default connect(mapStateToProps, mapDispatchToProps)(App);
```

### `jcut`

```javascript
/** @format */

import React from "react";
import { rest } from "msw";
import { setupServer } from "msw/node";
import { render, waitFor, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import "@testing-library/jest-dom/extend-expect";

import App from "../App";

const server = setupServer(
  rest.get("/greeting", (req, res, ctx) => {
    return res(ctx.json({ greeting: "hello there" }));
  })
);

beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());

test("render App", () => {
  // Arrange
  render(<App />);

  // Assert
  // Alert
});

test("handlers server error", async () => {
  server.use(
    // override the initial 'GET /greeting' request handler
    // to return a 500 Server Error
    rest.get("/greeting", (req, res, ctx) => {
      return res(ctx.status(500));
    })
  );

  // Arrange
  render(<App />);

  // Assert
  // Alert
});
```

### `jrs`

```javascript
/** @format */

import { createSlice, createAction } from "@reduxjs/toolkit";

const namespace = "app";
const initialState = {};

const appSlice = createSlice({
  name: namespace,
  initialState,
  reducers: {
    doSomeThing: (state, action) => {
      const { foo } = action.payload;
      state.foo = foo;
    },
  },
});

appSlice.asyncActions = {
  doOtherThingAsync: createAction(`${namespace}/doOtherThingAsync`),
};

export default appSlice;
```

### `jsc`

```javascript
const StyledDiv = styled(({ foo, ...other }) => <div {...other} />)(
  ({ foo }) => ({}),
  { name: StyledDiv }
);
```
