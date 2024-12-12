# Redux Toolkit Counter App

This project demonstrates how to set up and use Redux Toolkit in a React application with a simple counter example. The app allows incrementing, decrementing, and resetting a counter value.

---

## **Directory Structure**

```plaintext
redux-tool-kit-counter-app/
├── node_modules/
├── public/
├── src/
│   ├── assets/
│   ├── Components/
│   │   └── Counter.jsx
│   ├── store/
│   │   ├── index.js
│   │   └── slices/
│   │       └── counterSlice.js
│   ├── App.jsx
│   ├── main.jsx
│   ├── index.css
├── .gitignore
├── index.html
├── package.json
├── README.md
├── vite.config.js
```

---

## **Steps to Configure Redux Toolkit**

Follow the steps below to set up Redux Toolkit in this React project.

### 1. **Install Redux Toolkit and React-Redux**
First, install the necessary dependencies:
```bash
npm install @reduxjs/toolkit react-redux
```

---

### 2. **Create a Slice**
Create a slice to handle the state and reducers.

**File**: `src/store/slices/counterSlice.js`
```javascript
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    count: 0,
  },
  reducers: {
    increment(state) {
      state.count += 1;
    },
    decrement(state) {
      state.count -= 1;
    },
    reset(state) {
      state.count = 0;
    },
  },
});

export const { increment, decrement, reset } = counterSlice.actions;
export default counterSlice.reducer;
```

---

### 3. **Set Up the Store**
Configure the Redux store and register the slice reducer.

**File**: `src/store/index.js`
```javascript
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './slices/counterSlice';

const store = configureStore({
  reducer: {
    counter: counterReducer, // Register the counter reducer
  },
});

export default store;
```

---

### 4. **Wrap the App with the Redux Provider**
Wrap your application in the `<Provider>` component and pass the store to it.

**File**: `src/main.jsx`
```javascript
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import { Provider } from 'react-redux';
import './index.css';
import App from './App.jsx';
import store from './store/index.js';

createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

---

### 5. **Create the Counter Component**
Create a React component to interact with the Redux state.

**File**: `src/Components/Counter.jsx`
```javascript
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement, reset } from '../store/slices/counterSlice';
import { useEffect } from 'react';

const Counter = () => {
  const count = useSelector((state) => state.counter.count);
  const dispatch = useDispatch();

  useEffect(() => {
    console.log('Count updated:', count);
  }, [count]);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
      <button onClick={() => dispatch(reset())}>Reset</button>
    </div>
  );
};

export default Counter;
```

---

### 6. **Use the Counter Component**
Import and render the `Counter` component in your main application.

**File**: `src/App.jsx`
```javascript
import Counter from './Components/Counter';

const App = () => {
  return (
    <div>
      <Counter />
    </div>
  );
};

export default App;
```

---

## **How It Works**
1. The **slice** (`counterSlice.js`) contains the state and the reducers (`increment`, `decrement`, and `reset`).
2. The **store** (`index.js`) is configured to use the `counterSlice` reducer.
3. The **Counter component** connects to the Redux store using `useSelector` to access the state and `useDispatch` to dispatch actions.
4. The `Provider` component from `react-redux` makes the Redux store available to the entire app.

---

## **Commands**
- **Run the App**:
  ```bash
  npm run dev
  ```

---
