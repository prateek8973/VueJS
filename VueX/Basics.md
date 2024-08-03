# Vuex

Vuex is a state management pattern and library for Vue.js applications. It serves as a centralized store for all the components in an application, allowing for a predictable state management.

## Installation

To use Vuex in your Vue.js project, you need to install it first. You can do this by running the following command:

```bash
npm install vuex
```

## Getting Started

To get started with Vuex, you need to create a store. A store is an object that holds the application's state, and provides methods to mutate and access the state.

Here's an example of how to create a store:

```javascript
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

const store = new Vuex.Store({
    state: {
        count: 0
    },
    mutations: {
        increment(state) {
            state.count++;
        },
        decrement(state) {
            state.count--;
        }
    },
    actions: {
        increment(context) {
            context.commit('increment');
        },
        decrement(context) {
            context.commit('decrement');
        }
    },
    getters: {
        getCount: state => {
            return state.count;
        }
    }
});

export default store;
```

State of an app is just the data that you want to keep track of. In the above example, we define a state with a single property `count` initialized to `0`. OR in other words,

A **store** is basically a **container that holds your application state**. There are two things that make a Vuex store different from a plain global object:
1. Vuex stores are **reactive**. When Vue components retrieve state from it, they will reactively and efficiently update if the store's state changes.

2.You **cannot directly mutate the store's state.** The only way to change a store's state is by explicitly committing mutations. This ensures every state change leaves a track-able record, and enables tooling that helps us better understand our applications.

In the above example, we create a store with an initial state of `count: 0`. We also define two mutations (`increment` and `decrement`) to update the state, and two actions (`increment` and `decrement`) to commit the mutations. Additionally, we define a getter (`getCount`) to access the state.

To use the store in your Vue components, you need to import it and add it to the `store` option:

```javascript
import store from './store';

new Vue({
    store,
    // ...
});
```

## Getters

- Object which helps us to get the state of the store. 
- It is like computed properties for stores.
- Can be accessed in other components using `this.$store.getters.getterName`
- It takes two arguments, state and getters.
- It returns the state of the store.
- It is used to filter the state of the store.
- It is used to get the state of the store in a different format.

## Mutations

- Object which helps us to change the state of the store.
- It is like methods for stores.
- Can be accessed in other components using `this.$store.commit('mutationName')` in the computed properties and not the methods.
- It takes two arguments, **state** and **payload.**
- `Strict` mode in a component ensures that store data is not changed outside of it in some another components.
- Limitations
    - Mutations must be **synchronous.**
    - Mutations must be pure functions.
    - Mutations must be committed.

## Actions
Sit between the mutations and the components. They can commit mutations, but they can also do other things like async operations.
- Call the mutation using `context.commit('mutationName')` from within the action.
- Can be accessed in other components using `this.$store.dispatch('actionName')`
- It takes two arguments, **context** and **payload.**

Now you can access the state, mutations, actions, and getters in your components using the `$store` object.

## Using the Store

To access the state in a component, you can use the `$store.state` object:

```javascript
this.$store.state.count //accessing the count property of the state 
```

To commit a mutation, you can use the `$store.commit` method:

```javascript
this.$store.commit('increment');
```

To dispatch an action, you can use the `$store.dispatch` method:

```javascript
this.$store.dispatch('increment');
```

To access a getter, you can use the `$store.getters` object:

```javascript
this.$store.getters.getCount
```
## Mapping Techniques
1. **mapState**: It is used to map the state of the store to the component.
2. **mapMutations**: It is used to map the mutations of the store to the component.
3. **mapActions**: It is used to map the actions of the store to the component.
4. **mapGetters**: It is used to map the getters of the store to the component.

Example code:
```javascript
import { mapState, mapMutations, mapActions, mapGetters } from 'vuex';
import store from './store';

export default {
    computed: {
        ...mapState(['count']),
        ...mapGetters(['getCount'])
    },
    methods: {
        ...mapMutations(['increment', 'decrement']),
        ...mapActions(['increment', 'decrement'])
    }
}
```
Here we are using the `mapState` helper to map the `count` state to the component, 

the `mapGetters` helper to map the `getCount` getter to the component, 

the `mapMutations` helper to map the `increment` and `decrement` mutations to the component, 

and the `mapActions` helper to map the `increment` and `decrement` actions to the component.






