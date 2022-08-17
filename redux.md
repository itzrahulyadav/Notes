//to use redux first install react-redux and redux from npm

//create a index.js file and write the following code
-----------------------------------------------------
import {createStore} from 'redux';

const reducerFn = (state = {counter:1},action) => {
       if(action.type === "INC")
       {
           return {counter:state.counter+1};
       }
       if(action.type === "DEC")
       {
           return{counter:state.counter - 1};
       }
       if(action.type === "ADD")
       {
           return{counter:state.counter + action.payload}
       }
       return state;

}
const store = createStore(reducerFn);
export default store;

--------------------------------------------------

// in the index.js file of the react
-------------------------------------
import { Provider } from 'react-redux';
import store from './store';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store = {store}>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </Provider>
);
--------------------------------------

// in the app.js file 

-----------------------------------------
import { useSelector,useDispatch} from 'react-redux';
import './App.css';

function App() {

  const counter = useSelector((state)=>state.counter);
  const dispatch = useDispatch();
  const increment = () => {
     
     dispatch({type:"INC"})
  }
  const decrement = () => {
     dispatch({type:"DEC"})
  }
  const addBy = () => {
    dispatch({type:"ADD",payload : 10})
  }
  return (
    <div className="App">
      <h1>Counter App</h1>
      <h1>{counter}</h1>
      <button onClick = {increment}>increment</button>
      <button onClick = {decrement}>decrement</button>
      <button onClick = {addBy}>add by 10</button>
    </div>
  );
}

export default App;
--------------------------------------------------------

