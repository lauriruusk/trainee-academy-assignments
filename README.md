# Trainee Academy Assignments
Retrospection on a collection of assignments done on Buutti Trainee Academy. Some of the assignments have been chosen due to how challenging they were, others due to how interesting they were.

I will only display essential code in this work. rest of the code can be found [here](https://gitlab.com/lauriruusk/ruuskanen-lauri-trainee-academy)

## Assignment #1: Book List Service (React)

This has been a recurring assignment, coming up several times during front end assignments. I like the way this allows me to see just how much of an impact more complex techniques can have on a program. In this entry I will be discussing the React version of this assignment.

### The assignment

There are numerous ways to use Bootstrap in React. Perhaps the most convinient way is to use the npm pagacke [react-bootstrap](https://www.npmjs.com/package/react-bootstrap). Read the [React Bootstrap introduction](https://react-bootstrap.github.io/getting-started/introduction) for instructions on how to install and use React Bootstrap. 

The minimum you need to do to get it running is the following:

Install react-bootstrap with the following command: `npm install react-bootstrap bootstrap` 

Add `import 'bootstrap/dist/css/bootstrap.min.css';` in the beginning of your `App.js` file.

Add the following inside the `<head>` of your `index.html` which is found in the `public` folder:  


```html
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css"
  integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65"
  crossorigin="anonymous"
/>
```  
When you have React Bootstrap up and running replicate this familiar UI from the previous assignments. You don't need to generate the list from an array this time. It is enough to hard code it. You probably want to check out [grid](https://react-bootstrap.github.io/layout/grid/) and [forms](https://react-bootstrap.github.io/forms/overview/) from the React Bootstrap documentation. 

![book-list.png](https://buuttilab.com/education/trainee-academy-joensuu/assignments/-/blob/master/React/Assignment%20Set%201/book-list.png)

Note that you can replace many of the familiar classes of bootstrap with React Bootstrap -components. For example:

```jsx
// Bootstrap
<div class="container">
  <div class="row">
    <div class="col">
     <p>Hello!</p>
    </div>
  </div>
</div>

// React-Bootstrap
<Container>
  <Row>
    <Col>
      <p>Hello!</p>
    </Col>
  </Row>
</Container>
```

Depending on how you made the exercise 2 you might have to fine tune it after you add the Bootstrap styling to your app!

**EXTRA-EXTRA:** Generate the list from an array and 
make the button work! 

### Initial thoughts

I had previous experience from React and Bootstrap, so this wasn't too hard to do. However, with earlier versions of this assignment in mind, it was interesting to see just how much easier it was to make functional pages with React. 

### Solution

For the book display, I simply made a Bookshelf component where I mapped known books into a list. 

As for adding of a new book, I utilised Bootstrap's default Form function for layout, and for the book adding itself I used the following function:

```js
const bookAdder = (event) => {
      event.preventDefault();
      const n = event.target.name.value;
      const p = Number(event.target.pagecount.value);
      const book = { name: n, pagecount: p };
      console.log(book);
      setBookList([...bookList, book]);
  }
```

Function is quite simple: I store book's name and pagecount into separate temporary variables. I also force pagecount into a number to ensure proper display. After that, I just make an object out of them and add it to the book list. After that, the book will be displayed in the bookshelf.

## Assignment #2: Command List, with a class

Another recurring assignment, where the mission is to give orders to a robot, and print it's final location.

### Initial thoughts

As with previous assignment, it's interesting how much the program changes with more complex technology. The command list has stayed the same throughout all versions of this assignment, but solutions have differed greatly.

### Solution

for the robot itself, I made a simple class:

```js
class Robot {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    handleCommandList(str) { 
        let tempXY = [];
        tempXY = commandAction(str, [this.x, this.y]);
        this.x = tempXY[0];
        this.y = tempXY[1];
    }       
}
```
Nothing too special in here either- the robot gets initial position into constructor, and it has a built-in function to handle the list of commands. This function in turn uses another function to go through the command list and determine final location, which is updated to robot upon completing the function. This function is fairly simple despite being bit long: all it does is go through command list one character at a time, and stopping either at the end of the list, or if it encounters the letter B.

In hindsight, updating x and y after every command would've been more useful, as that would've allowed me to follow the "path" the robot took. But still, this solution did fulfill assignment requirements.


