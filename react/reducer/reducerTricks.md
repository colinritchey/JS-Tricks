
source: [Build yourself a Redux](https://zapier.com/engineering/how-to-build-redux/)

Author: Justin Deal

```javascript
//old way
const CREATE_NOTE = 'CREATE_NOTE';
const UPDATE_NOTE = 'UPDATE_NOTE';

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case CREATE_NOTE:
      return // some new state with new note
    case UPDATE_NOTE:
      return // some new state with note updated
    default:
      return state
  }
};

//without switch statement
const handlers = {
  [CREATE_NOTE]: (state, action) => {
    return // some new state with new note
  },
  [UPDATE_NOTE]: (state, action) => {
    return // some new state with note updated
  }
};

const reducer = (state = initialState, action) => {
  if (handlers[action.type]) {
    return handlers[action.type](state, action);
  }
  return state;
};

// ES6 way of returning an unmutated state

return {
  ...state,
  notes: {
    ...state.notes,
    [id]: editedNote
  }
};


// alternative way of executing actions
const actions = [
  {type: CREATE_NOTE},
  {type: UPDATE_NOTE, id: 1, content: 'Hello, world!'}
];

const state = actions.reduce(reducer, undefined);

ReactDOM.render(
  <pre>{JSON.stringify(state, null, 2)}</pre>,
  document.getElementById('root')
);

// What store is doing

const createStore = reducer => {
  let state;
  const subscribers = [];
  const store = {
    dispatch: action => {
      validateAction(action);
      state = reducer(state, action);
      subscribers.forEach(handler => handler());
    },
    getState: () => state,
    subscribe: handler => {
      subscribers.push(handler);
      return () => {
        const index = subscribers.indexOf(handler);
        if (index > 0) {
          subscribers.splice(index, 1);
        }
      };
    }
  };
  store.dispatch({type: '@@redux/INIT'});
  return store;
};
```
