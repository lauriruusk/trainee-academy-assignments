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

Another recurring assignment, where the mission is to give orders to a robot, and print it's final location. As with previous assignment, I selected the latest version for this.

### The Assignment

Let us return to the robot in assignment 4.
There we had the x and y variables as globals (global variables). However, what if we want to have multiple robots?
Create a Robot class with x and y properties. Inside the class, also create a handleCommandList function that takes a command list (string) as a parameter and handles it exactly like in task 3, except that it must affect the x and y coordinates of the Robot class instance rather than global variables.
Create an instance of the class and run the "NNEESSWWCNNEEENNNCEESSSWNNNECEESWWNNNEEEBENNNEEE" command list through the robot. Print the robot afterwards and verify its coordinates to be x === 8, y === 7 to make sure your class works correctly.

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

Commands were handled with a function:

```js
function commandAction(cmd, values) {
    let j = 0;
    this.x = values[0];
    this.y = values[1];
    do {
        if(cmd.charAt(j) === 'B') {
            break;
        }
        switch (cmd.charAt(j)) {
            case 'N':
                this.y = this.y + commandHandlers.N();
                break;
            case 'E':
                this.x = this.x + commandHandlers.E();
                break;
            case 'S':
                this.y = this.y + commandHandlers.S();
                break;
            case 'W':
                this.x = this.x + commandHandlers.W();
                break;
            default:
                break;
        }
        j++;
    } while (true);
    return ([this.x, this.y]);
}
```
The function gets command string and initial x and y values as parameters. Then the function goes through command strings one by one inside a while loop until the command is "B", at which point the loop ends and the function returns an array with final x and y values.
Changing x and y values is done via subfunctions. They are very simple - they just return either +1 or -1, depending on command.

In hindsight, updating x and y after every command would've been more useful, as that would've allowed me to follow the "path" the robot took. But still, this solution did fulfill assignment requirements.

## Assignment 3: Harder recursion with merge-sort

This one I picked due to it's real life usefulness. While I initially thought of the next assignment, which dealt with recursive structure, I ended up with this as it's likely somtething I'll end up using more frequently.

### The Assignment

Merge-sort is a common recursive algorithm for sorting lists / arrays.

It works by splitting the list into two, _resursively_ sorting the sub-lists and then _merging_ the lists back into one.

What doing this recursively means is that when the list is divided into two sub-lists, the sub-lists are divided again into smaller sub-lists, those divided again into smaller lists.. and so on, until every sub-list only has 1 entry which is deemed sorted with itself.

Then, each 1-element sub-list is merged with another 1-element sub-list so that the 2 elements are in order. Then each 2-element sub-list is merged with another 2-element sub-list, forming a merged list of 4 elements. This merge process goes on until the entire list has been merged and sorted.

Below is an illustration of the algorithm:

```
[4, 19, 7, 1, 9, 22, 6, 13]
-> split into left and right

Left: [4, 19, 7, 1]   Right: [9, 22, 6, 13]
-> split these further

L [4, 19]   R: [7, 1]   L: [9, 22]   R: [6, 13]
-> split these further

L [4]   R [19]   L [7]   R [1]   L [9]   R [22]   L [6]   R[13]
-> merge these

L [4, 19]  R[1, 7]   L[9, 22]  R[6, 13]
-> merge these

L [1, 4, 7, 19]   R[6, 9, 13, 22]
-> merge these

Finally, the list is sorted!
[1, 4, 6, 7, 9, 13, 19, 22]

```

Implement the two functions `mergeSort` and `mergeSubLists` so that the program sorts the array of numbers as intended.

```js
function mergeSort(array) {
    // Your code here.

    // You need to:
    // 1. handle the base case (if the array only has 1 element)
    // 2. split the list into two separate lists
    // 3. recursively merge the lists by calling this function for them
    // 4. call the mergeSubLists function for the "now-sorted" sublists and return its result
}


function mergeSubLists(leftList, rightList) {
    // Your code here.

    // Merge the sub-lists.
    // Add all elements from one list to the other list
    // to the correct index so that the "combined" list
    // remains sorted.
    // Then return the combined list.
}


const array = [ 4, 19, 7, 1, 9, 22, 6, 13 ];
const sorted = mergeSort(array);
console.log(sorted); // prints [ 1, 4, 6, 7, 9, 13, 19, 22 ]
```

**EXTRA-extra:** Add one more element to the above array. This makes it impossible to divide the array into one even bits of 1, because it has an uneven amount of numbers. This forces you to handle a case of empty lists in `mergeSubLists` and make a decision on how to split an array with an uneven number of elements (whether to include the "extra" element on the left or right list).

### Initial thoughts

Initial briefing seemed simple enough, although merge-sort is one of those things that, while seemingly easy, it took me a little while to wrap my head around. I did have to look around a bit to understand the concept little bit better. I ended up using [Doable Danny's](https://www.doabledanny.com/merge-sort-javascript) article about merge-sort to understand the concept better and as a base for my own functions.

### Solution

```js
function mergeSort(array) {
    if (array.length <= 1) {
        return array;
    }
    let mid = Math.floor(array.length / 2);
    let left = mergeSort(array.slice(0, mid));
    let right = mergeSort(array.slice(mid));

    return mergeSubLists(left, right);
}
```
First function splits the array recursively into halves, as long as it is long enough to be halved. after that, it calls on the merging function on return, with halved arrays as parameters.

```js
function mergeSubLists(leftList, rightList) {
    let sortedList = [];
    while (leftList.length && rightList.length) {
        if(leftList[0] < rightList[0]) {
            sortedList.push(leftList.shift());
        } else {
            sortedList.push(rightList.shift());
        }
    }
    return [...sortedList, ...leftList, ...rightList]
}
```
Second function merges given arrays into sorted array. it also checks which array's content has higher valus in order to determine which one is pushed first into the new array. After that, function returns sorted array, along with what's left of the original arrays. As the funtion is called at mergeSort's return, it is used recursively to put original array back together, only this time in order.

While my functions ended up being almost identical to Doable Danny's ones, it did take me some time to understand what the functions actually do. Also, another problem was that I initially used splice, took me some time to realise it wasn't the ideal tool for this. All in all, a fun assignment that seemed easy at first, but turned out to be anything but.