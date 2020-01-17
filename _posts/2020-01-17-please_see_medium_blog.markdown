---
layout: post
title:      " Please see Medium Blog"
date:       2020-01-17 17:59:19 +0000
permalink:  please_see_medium_blog
---


https://medium.com/@carltondgrandison/flow-of-code-in-a-request-response-cycle-98ae2e560155



In this particular blog, I will walk you through cycle of a user input for react/redux. 

To begin, when a user starts to type in the data in specific fields, the form is constantly being updaed; therefore, behind the scenes, the page is constantly being re-rendered. For example, below is the recipe form that allows you to enter data in the input fields: 

```const RecipeForm = (props) => {
  console.log(4)
In this particular blog, I will walk you through cycle of a user input for react/redux.
To begin, when a user starts to type in the data in specific fields, the form is constantly being updated and behind the scenes, the page is constantly being re-rendered. For example, below is a form that allows you to enter data in the input fields:

Form Field
To reiterate, when entering in data in the fields the fields are constantly being re-rendered.

Once the submit button is hit, a dispatch is called and it’s job is to change the state with the this.setState({}). Once the button Add Recipe is clicked to submit, you can see in the function below the handleOnSubmit is now called:
handleSubmit = (event) => {
//console.log(event)
event.preventDefault()
this.props.createRecipe(this.state)
this.setState({
   name: '',
   instructions: '',
   ingredients: '',
   time: ''
})
}
But before we reach this.setState({}), we hit this.props.createRecipe(this.state). In order to access the properties of createRecipe, we pass the properties from our store with mapDispatchToProps down to this component. The access is created with a simple connect():
export default connect(null, {createRecipe})(RecipePage)
So now, lets go to our Action Component to view our createRecipe const:

Create Object
The createRecipe const handles the creation of a new object. As you can see, it fetches the data from our backend, where an API request is called. But before it renders any information, what is happening here is that the a Promise is instantiated. A Promise returns the results at a later point in time. So with that being said, we will come back to the createRecipe at a later point in this blog.
Now the initial state is ready to going to change, so in this cycle, we then go back to the handleOnSubmit function where the setState({}) is being created:
handleSubmit = (event) => {
//console.log(event)
event.preventDefault()
this.props.createRecipe(this.state)
this.setState({
   name: '',
   instructions: '',
   ingredients: '',
   time: ''
})
}
And the page is now being re-rendered again. During this stage, it then goes back to createRecipe const where we had the Promise to time to complete the render process. Finally, it dispatches the type RECIPE_CREATE in our store to update the state.
    return (
      <div className="RecipeForm">
        <form onSubmit={props.onSubmit}>
          <div className="field">
            <input 
            type='text' 
            placeholder='Enter Recipe Name' 
            value={props.name} 
            name='name' 
            onChange={props.onChange}/>
            </div>
            <br/>
          <div>
            <textarea 
            type='text' 
            placeholder='Enter Instructions' 
            value={props.instructions} 
            name='instructions' 
            onChange={props.onChange}/>
            </div>
            <br/>
            <div>
            <input 
            type='text' 
            placeholder='Enter Ingredients' 
            value={props.ingredients} 
            name='ingredients' 
            onChange={props.onChange}/>
            </div>
            <br />
            <div>
            <input 
            type='text' 
            placeholder='Enter Cook Time' 
            value={props.time} 
            name='time' 
            onChange={props.onChange}/>
            </div>
            <br />
          <Button variant="success" type='submit'>Add Recipe</Button>
        </form>
      </div>
    )
}

export default RecipeForm


