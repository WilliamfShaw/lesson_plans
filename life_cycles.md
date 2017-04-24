# React: Lifecycle events, Lifecycle event execution

# Learning objectives

- Identify the React life cycle methods
- Describe the order in which the life cycle methods are executed
- Apply life cycle methods to a multi component React application

## Introduction (5 mins)

This morning we will be diving a little further into React and understanding a little more about how it works.

React enables to create components by invoking the constructor() or without es6 React.createClass() method which expects a render method and triggers a lifecycle that can be hooked into via a number of lifecycle methods.

Understanding the component lifecycle will enable you to perform certain actions when a component is created or destroyed. Further more it gives you the opportunity to decide if a component should be updated in the first place and to react to props or state changes accordingly.

## The Lifecycle(5 mins)

In order to understand the lifecycle of a component and its corresponding methods we need to differentiate between the initial creation phase, where a component is created, state and props changes triggering updates, and components unmounting.


## Initialization phase (10 mins)

During the initialization phase of a react component the following methods are called in the following order:

```
- getDefaultProps()
- getInitialState()
- componentWillMount()
- render()
- componentDidMount()
```

It is important to note that since we are using es6 syntax, we will not be using getDefaultProps() and getInitialState(). We will instead be using the constructor() method for both of these methods.

Following the exectution process above lets break down these methods

- `getInitialState`
    - method enables the programmer to set the inital state values, that then become accessable to the component via, `this.state`.
- `getInitialProps`
    - method enables the programmer to set the initial prop values, that then become accessable to the component via, `this.props`.
- `componentWillMount`
    - method is called before the render method is executed. It is important to note that setting state in this phase will NOT trigger a re-rendering. This is a good place to do something programatically before loading.
- `render`
    - method returns the needed component markup, which can be a single child component, null or false(in the event you dont need rendering for this component).
    This part of the lifecycle is where props and state values are interpreted to create the correct output. It is important that you do not try to the state of props or state in this function, (no this.setState() etc). This is important to remember because the render function has to be pure, meaning the same result is returned every time the method is invoked.
- `componentDidMount`
    - As soon as the render method has been exectued this method is called. The DOM can be accessed in this method, because the DOM has already been rendered. In this method you can define DOM manipulations or data fetching operations.

# State Changes // Prop changes (10 mins)

There will be times when we update a component. The nice part about these methods is that react gives them to you for free. Meaning it does it for you. However it is good to see them as you may come across them in the future.

```
- shouldComponentUpdate()
- componentWillUpdate()
- render()
- componentDidUpdate()
```

- `shouldComponentUpdate`
     - is always called before the `render()` method and enables the programmer to define if a re-rendering is needed or can be skipped. Method is never called on initial rendering. This method must return a boolean.
- `render`
    - we know what render is doing already
- `componentWillUpdate`
    - get called as soon as the shouldComponentUpdate returned true, and only if the shouldComponentUpdate returns true. Any changes to state are prophibited in this method as this method should be used to prepare for an upcoming update not perform the update itself.
- `componentDidUpdate`
    - is called after the render method. Similar to componentDidMount this method should be used for any DOM operations.


The only difference when a component is recieving props is that prior to the shouldComponentUpdate method, componentWillRecieveProps will be called.

- `componentWillRecieveProps`
    - is only called when the props have changed and it is not the initial rendering. This method is can be used to compare the old props to the new props and update state accordingly if you would like. Updating the state will trigger a render.

# You do

# HACKER NEWS BUILD!!!

# Step 1 (10 mins)

```
# TECH NEWS FEED

### Learning Objectives
- Practice using React to create your front end
- Apply best practices for file structuring
- Use `superagent` to retrieve data
- Practice building a multi component react application

Today we will be using the Hacker News API to set up our own news feed!!

Here is the Hacker News https://github.com/HackerNews/API documentation, please take a 10 mins and read through the docs
```

# Step 2 (10 mins)

We are going to set up our file structure. This is not the only way to set this up, but one way. Organization is imperative to maintaining a clean code base.

- `mkdir react_hacker_news`
- `cd react_hacker_news`

**The following command will create a `package.json` file, before moving forward please check that this file is present in the root folder of your project**

- `npm init`

**The following set of commands will set the dependencies of your application, run the commands one by one and check in your `package.json`, in the dependecies section of the object and make sure that the dependencies have been written. You will also see a `node_modules` folder now present.**

- `npm install -S webpack webpack-dev-server`
- `npm install -S react react-dom`
- `npm install -S babel-core babel-loader babel-preset-react babel-preset-es2015`
- `npm install -S superagent`

**Lets finish out our file structure. The tree should look like this when you're finished**

```
├── node_modules
├── src
|   ├── index.js
│   ├── components
│   └── static
│       ├── index.html
│       └── stylesheets
│           └── style.css
├── package.json
└── webpack.config.js

```


# Step 3 (10 mins)

Setting up the `webpack.config.js` file, we will do this together.

# BREAK

# Step 4

#### Setting up our `static folder`


#### index.html
- Get a base structure for your `index.html` file
- create a `div` in the `body` with the `id` of `main`
- create a `script` tag at the bottom of the `body` with a `src` of `bundle.js`
    - Remember in the `webpack.config.js` we told webpack to output the compiled source to `bundle.js`
- in the head of your file set a link to a stylesheet which we will create next, `style.css` and paste the following:

```
<link href='http://fonts.googleapis.com/css?family=Poiret+One' rel='stylesheet' type='text/css'>
<link href='http://fonts.googleapis.com/css?family=Passero+One' rel='stylesheet' type='text/css'>
```

#### style.css
- in your `style.css` in the `stylesheets` folder and paste the following:

```
body {
  text-align: center;
  background: url('http://www.mountairyhabitat.org/wp-content/uploads/2013/05/gray-background1.jpg') no-repeat 50% 50% fixed;
  background-size: cover;
  z-index: -1;
}

#logo {
  font-family: 'Passero One', cursive;
  margin: 3rem auto;
  font-size: 3.5rem;
}

.article {
  font-family: 'Poiret One', cursive;
  background: rgba(166, 209, 255, 0.9);
  margin-top: 1.5rem;
  border-radius: 1.3rem;
}

#article-modal {
  position: fixed;
  height: 100%;
  width: 100%;
  top: 0;
  background: rgb(255, 255, 255);
}

#show-article {
  position: relative;
  height: 100%;
  width: 100%;
}

iframe {
  position: relative;
  height: 90%;
  width: 100%;
}

#close {
  color: blue;
}
```

# Step 5

Lets Break down how we should be thinking about react applications. And how react applications move data around.

![reactimage](https://raw.githubusercontent.com/ga-wdi-lessons/react-continued/master/react-render.png)

Now that we are aware of how data is moving around, lets start thinking about how to structure our applications moving forward. React works on a container based heirarchy, with data flowing down to the child components.

Lets look at our application and break it down into components.

# Step 6

Setting up index.js together

# Step 7

### Our first Component

Now that we've told our application where the point of entry is for the view layer, lets make the component that we referenced in the `index.js` file

- In your `components` folder, make a file called `app.jsx`
- We need to import a few things in order for this file to work. At the top of this file, import `React` for now
- `App` will be a dummy component
- For now lets have the App return a `div` with an `h1` inside with the `id` of logo, that says `Todays Hacker News`
- Lets run the following command in our terminal to start the webpack server `npm run dev`
- In Chrome navigate to `127.0.0.1:8080`, this is the equivalent of `localhost:8080` try both our and see for yourself

# Step 8

When we think about a react application we need to think about the Parent Component / Child Component relationships. We think this way because of the way data flows in a react application.

We currently have this main component which is the point of entry for our view layer. This component really only knows how to put itself on the DOM, that is its sole purpose. We need to create a few more components that will eventually come together to appear as our working application.

Lets start to think about apps form the top down, for this application we can think about it like this:

- The `App` component will return along with the `h1` an `ArticleList` component
- The `ArticleList` component will in its `render` make as many individual `Article` components as it pulls from the API
- The `Article` component will in its `render` function send each individual article to the `ArticleView` component it will also hold all of the events associated with each of the `ArticleViews`
- The `ArticleView` will be a dummy component, meaning it holds no state, it is strictly a component that renders something to the page

# Step 9

#### Making our `ArticleList` Component

- In the `components` folder create a file called `article_list.jsx`
- `ArticleList` will need the following imports `React`, `superagent` as `request`
- `ArticleList` will need a `constructor` a mandatory `render` and a `componentWillMount` life cycle method.
- Be sure to `export` `ArticleList` at the bottom of the file.
- Go back to the `App` component and `import` the newly created `ArticleList` file as `ArticleList`


**Everytime we make a new component that is nested, we will render a simple div with some text in it just to make sure its working. So in our `ArticleList` components render, lets render a `div` with a nested `h1` with some text in it. Go back to the browser and be sure your component is rendering to the page. Remember this component is being rendered by `App` which knows how to go to the page. Once you know the component is working we can move on**

####`ArticleList` will need the following functionality

- `constructor`
    - will call `super`
    - will set `state` of the component with `data` set to an empty array
- `componentWillMount`
    - will make a request to the proper Hacker News endpoint to get all of todays `top stories`
    - then it will set the state of `data` in this component to the body of the returned information
- `render`
    - will map over the new data state and render an `Article` for each item in the `data` state
    - the `Article` component will accept props of `id` and `key` each set to the id of the article

**Remember to export this file**

# Step 10

#### Making an individual Article component

- `Article` will need the following imports: `React`, `request`

#### `Article` will need the following functionality

- `constructor` which accpets a `props` argument
    - will call `super` which accepts a `props` argument
    - will set `state` of the component with `data` set to an empty object
    - will set `state` of the component with `modalOpen` set to `false`
- `componentWillMount`
    - will make a request to the proper Hacker News endpoint to get the individual article from the `id` being passed through props
    - then it will set the state of `data` in this component to the body of the returned information
- `openModal`
    - will set the state of the components `modalOpen` to true
- `closeModal`
    - will set the state of the components `modalOpen` to false
- `render`
  **Test your component to make sure its working with dummy text first**
    - will render an `ArticleView` for the `data` recieved from the API
    - will pass `title`, `author` and `openModal` as `props` to `ArticleView`
    - will render a `ArticleModal` if the state of `openModal` is true

**Remember to export this file**

# Step 11

#### Making our view components!!! :metal: :metal: :metal:

Lets discuss together the idea of `Stateless` components!!



#### Dem Views Doe

The `Article` component renders two sub components `ArticleView` and `ArticleModal`.

####  ArticleView

Is stateless component, which accepts props of `title`, `author` and `openModal`

- this component will need to import only `React`
- this component will return a html structure which will look like this

```
<div class="article">
  <h1 class="title">[TITLE]</h1>
  <h3 class="author">Author: [AUTHOR]</h3>
</div>
```

- when the `article` div is clicked it will call the `openModal` prop


####ArticleModal

Is a stateless component, which accepts `url` and `closeModal` as a prop

- this component will need to import only `React`
- this component will return a html structure which will look like this

```
  <div id="article-modal">
      <div id="show-article">
        <iframe src=[URL]></iframe>
        <h2 id="close">CLOSE</h2>
      </div>
    </div>
```

- when the `close` id is clicked it will call the `closeModal` prop

WHOAAAA!! What is that `iframe` thing???? [Learn about Iframes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)
