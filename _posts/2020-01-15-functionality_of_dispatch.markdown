---
layout: post
title:      " Functionality of dispatch"
date:       2020-01-15 22:01:51 -0500
permalink:  functionality_of_dispatch
---


To begin, dispatch is a product of the Redux store. The Redux store is created using thunk and middleware that lets you return a function instead of an object. From there, you are able to call upon that action in the store to create synchronous actions.

`import { createStore, compose, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers/rootReducer'

const composeEnhancer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const store = createStore(
  rootReducer,
  composeEnhancer(applyMiddleware(thunk)),
);

export default store;`

Once the store is created, we then have the ability to use it in our app with `Provider` from React-Redux. Provider gives us the abiity to access the store from our App. 

Dispatch simply allows us to execute an Action in the store in order change the state. You can acceess the dispatch from either `store.dispatch` or `connect`. With `connect` you are able to access the `mapDispatchToProps`, which allows you to create functions to pass properties to your components. In th example below, I am able to access the properties of `editRecipe` and `fetchRecipe` with connect, so I can pass it to my component:  

` componentWillMount() {
        this.props.fetchRecipe(this.state.id)
    }`

`handleSubmit = (event) => {
    console.log(event)
  event.preventDefault()
  let recipe = {...this.state, id: this.props.recipe.id}
   this.props.editRecipe(recipe)
   this.setState({
       name: this.props.name,
       instructions: this.props.instructions,
       ingredients: this.props.ingredients,
       time: this.props.time,
       isClicked: !this.state.isClicked`
		
      `export default connect(null, { editRecipe, fetchRecipe })(RecipeEdit)`
			
			
			 I am able to access the properties in my Actions component that executes the dispatch, by using connect. In order to do so remember to specify the second argument in `connect()`. In the above example, I am using`mapDispatchToProps` in the second argument `connect(null, { editRecipe, fetchRecipe }` to pass the properties. 
			 
			I could however, call `matchDispatchToProps` by explicity calling it my component like so: 
			
			`const mapDispatchToProps = dispatch => {
  return {
    // dispatching plain actions
    editing: () => dispatch({ type: 'RECIPE_UPDATE' }),
    fetching: () => dispatch({ type: 'RECIPE_FETCH' })
		}}```
		
		Then connecting it the store like so: 
		`export default connect(null, (mapDispatchToProps ))(RecipeEdit)`
		
		



