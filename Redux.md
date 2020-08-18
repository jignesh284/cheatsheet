## JavaScript Fundamentals

### what is functional Programming?


Other paradigms: Functional, Object-oriented, procedural, Event-driven

1. Breaks problems into funtions which takes input and returns output. (can be run in parallel)
2. JS Functions are first class citizens: can treat then as any other variables, can be passed to another function, return it other function, assign it to variable 
3. **Higher Order Function**: can take funtion as argument or return function as output. array.map(x => 2*x) here map is higher order function.
4. **Lodash**: compose, it takes functions and return composition of all the functions.
               pipe: list in the order we apply it.
5. Curring: Is a technique that takes a funtion with N arguments and converts it to a funtion which takes single argument
```
Example of curring:

function add(a) {
  return function(b) {
    return (a+b);
  }
}

or 

const add2 => a => b => a+b;
add2(1)(2);
```
5. Pure functions: if we give same arguments it will return same results every single time. Pure functions cannot have/change: random values, current date time, Global States(DOM, files, db, etc), Cannot mutate parameters 
                   It depends only on the input params and not on global output. 
```diff
+ pros
+ self documenting
+ Easily Testable
+ Concurrency
+ Cacheable
```

6. Immutable: Strings are immutable in JS, they don't get changed on copy
7. Const does not means Immutable as we can change the property of const variable. It means that we cannot reassign value to object.
``` diff
const book = {}
book.title = "Ram"

+ pros immutablity
+ Predictability
+ faster Change Detection
+ Concurrency

- Cons
- Performance
- Memory Overhead (Can be reduced by structural sharing)
``` 
8. Maintaing Immutablity:
```js
Both of these methods does a shallow copy:

const person = {name: "John"}.  
Object.assign({}, person, {name: "BoB", age: 30}). // it is similar to spread operator

const updated = { ...person, name: "BoB", age: 30}; 


// Example of shallow copy:

const person = {
  "name" : "John",
  "address": {
    "country": "USA",
    "city": "LA" 
  } 
}

const updated = { ...person, name: "bob"}
updated.address.city = "SF";

# changes the adress of both the person.
console.log(person);
console.log(updated);


// Example of Deep Copy:

const updated = {
  ...person,
  address: { ...person.adress, city: "SF"},
  name: "BoB"
}

```

8. Immutablity with Updating Arrays:
```js
const numbers  = [1,2,3]

// Adding
const added = [ ...numbers,4 ] // Adding at the end of array 
const added = [ 0, ...numbers ] // Adding in the beginning of array 
// in the middle before 2
const index = numbers.indexOf(2);
const added = [ ...numbers.slice(0, index), 
                4,
                ...numbers.slice(index)
              ]
              
 // Removing 
 const array_without_2 = numbers.filter(n => n != 2) 
 
  // map 
 const array_replace_2_w_20 = numbers.map(n => n === 2 ? 20 : n) 
```

9. Enforcing Immutablity (for objects in javascript): libraries ** Immutable, Immer, Mori ** 

```js 
import { Map } from 'immutable' ;

// Doesnot use plain javascript object. Hard to integrate
let book = Map({ 'title': 'Harry Potter' });

function publish(book) {
  return book.set("isPublished", true);
}

book = publish(book)

console.log(book.toJs())

toJS: converts to JavaScript object
set: to set the value,
get: to get the value of property
```

10. Immer:
```js

import { produce } from. 'immer';

let book = {"title": "Harry Potter"};

function publish(book) {
  return produce(book, draftBook => {
    draftBook.isPublished = true;
  });
}

updated = publish(book)

console.log(updated);
```

## Redux

**Store**: is single javascript object that stores application state. 
**Reducer**: is a function that takes the current state and returns the updated state for a store.
**Action**: is something which tells which fields to be updated.


Action ---dispatch--> Store ---> Reducer 

                      Store <--- Reducer
                      
                     
```js
// Reducer.js

let lastId = 0;
                // Default statement
function reducer (state = [], action) {
    switch( action.type) {
        case 'bugAdded':
            return  [
                    ...state,
                    {
                        id: ++lastId,
                        description: action.payload.description,
                        resolved: false, 
                    }
                ]
            break;
        case 'removeBug':
            return state.filter(bug => bug.id !== action.payload.id);
            break;
        default:
            return state;
    }

}
```

### Store
```js
// Store.js

import { createStore } from 'redux';
import reducer from './reducer';  // because we are doing default export for reducer function


const store = createStore(reduder);

export default store; 
```


### Dispatchers 
```js

import store from './store';
 
console.log(store);

store.subscribe(() => {
     console.log("State Changed", store.getState())
 });

const unsubscribe  = store.subscribe(() => {
    console.log("State Changed", store.getState())
});


store.dispatch({
    type: "bugAdded",
    payload: {
        "Description": "Bug-1"
    }
})

unsubscribe();

store.dispatch({
    type: "bugRemoved",
    payload: {
        "id": "1"
    }
})

```

Actions
```js
import store from './store';
import * as actions from './actionTypes';
 
console.log(store);

store.subscribe(() => {
     console.log("State Changed", store.getState())
 });

const unsubscribe  = store.subscribe(() => {
    console.log("State Changed", store.getState())
});


store.dispatch({
    type: actions.BUG_ADDED,
    payload: {
        "Description": "Bug-1"
    }
})

unsubscribe();

store.dispatch({
    type: "bugRemoved",
    payload: {
        "id": "1"
    }
})
```
              













                   
