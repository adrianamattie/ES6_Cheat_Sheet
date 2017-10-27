##Variable Declaration: let & const
let and const are the new ways of utilizing the var key word.

// ES5
var name = 'Adrian Pearman';
var age = 26;
name = 'Pearman Adrian';
console.log(name);
// this will return 'Pearman Adrian'

// ES6
const name = 'Adrian Pearman'
let age = 26
name = 'Pearman Adrian';
console.log(name);
// this will return an error because the const variable is immutable
// var keywords are function scope where let and const is block scope


// ES5
function driversLicense(passedTest){
  if (passedTest) {
    var name = 'Adrian';
    var DOB = 1991;
  }
    console.log(name + ' born in '+ DOB + ', is allowed to drive now');
}
driversLicense(true)
// This function will return the console.log message within the function

// ES6 v1
function driversLicense(passedTest){
  if (passedTest) {
      let name = 'Adrian';
      const DOB = 1991;
  }
  console.log(name + ' born in '+ DOB + ', is allowed to drive now');
}
driversLicense(true)

// this function will return an error as the console.log message is outside of the block scope of the if function.
// in order to have the ES6 version work like the ES5 version, the function would have be written like so:

// ES6 v2
function driversLicense(passedTest){
  let name;
  const DOB = 1991;

  if (passedTest) {
    name = 'Adrian';
  }
  console.log(name + ' born in '+ DOB + ', is allowed to drive now');
}
driversLicense(true)


##Blocks and IIFE
// ES5
(function(){
  var c = 3;
})()
console.log(c); //Will return an error as c is undefined and not available

// ES6
{
  const a = 1;
  let b = 2;
  var c = a+b
}
console.log(a+b); //Will return an error as a & b is not available because of block scope
console.log(c); //Will return 3 as var declaration is not block scope but function scope


##Strings
let firstname = 'Adrian';
let lastname = 'Pearman';
const YOB = 1991

function Age(year){
  return 2017 - year
}

// ES5
console.log('This is ' + firstname + ' ' + lastname + '. He was born in '+YOB+'. Today, he is '+Age(YOB));
// ES6
console.log(`This is ${firstname} ${lastname}. He was born in ${YOB}. Today he is ${Age(YOB)}`);

const n = `${firstname} ${lastname}`
// Validates whether a string begins with a certain character
console.log(n.startsWith('A')); //Returns True
// Validates whether a string ends with a certain character
console.log(n.endsWith('R')); //Return False
// Validates whether a string include with a certain character
console.log(n.includes(' '));
// Repeats a string value by a set amount of times
console.log(firstname.repeat(5));

##Arrow Functions
// Example #1
const years = [1992, 1942, 2001, 1998, 2017]
// ES5
var ages = years.map(function(e){
  return 2017 - e
})
console.log(ages);
// ES6 w/ one arguement
const ages = years.map(el => 2017 - el)
console.log(ages);

// ES6 - w/ multiple arguements
let ages = years.map((el, index) => `Age element ${index + 1}: ${2017 - el}.`)
console.log(ages);

// ES6 - w/ multi line function. MUST HAVE CURLY BRACES IN THE function
let ages = years.map((el, index) => {
  const now = new Date().getFullYear();
  const age = now - el;
  return `Age element ${index + 1}: ${age}`;
})


// Example #2
// ES5
  var box1 = {
    color: 'green',
    position: 1,
    clickMe: function(){
      document.querySelector('selector').addEventListener('click', function(){
        var self = this;
        var str = 'The color of the box is ' +self.color + ' and it is position ' + self.position;
        alert(str)
      })
    }
  }
  box1.clickMe()
// ES6
  var box2 = {
    color: 'blue',
    position: 2,
    clickMe: function(){  
      //Due to the scope, if this function was written with an arrow function,
      // then the 'this' objects would point to the global window as opposed to the object and return unefined.
      document.querySelector('selector').addEventListener('click', () => {
        var str = `The color of the box is $(this.color) and it is position ${this.position}`
        alert(str)
      })
    }
  }

// Example #3
// ES5
function Person(name){
  this.name = name
}

Person.prototype.myFriends = function (friends) {
    var arr = friends.map(function(e){
      return this.name + ' is friends with ' + e
    }.bind(this))
    console.log(arr);
}

var friends = ['bob', 'bill', 'joe', 'john', 'mike']
new Person('greg').myFriends(friends)

// ES6
function Person1(name){
  this.name = name
}

Person1.prototype.myFriends1 = function(friends){
  var arr = friends.map(e =>
    `${this.name} is friends with ${e}`
  )
  console.log(arr);
}

var friends1 = ['bob', 'bill', 'joe', 'john', 'mike']
new Person1('ryan').myFriends1(friends1)



##Destructuring
// Example 1
// ES5
var John = ['John', 26]
name = John[0]
age = John[1]

// ES6
const [name, age] = ['Jane', 30]
console.log(name);
console.log(age);

const obj = {
  firstName: 'Adrian',
  lastName: 'Pearman'
}

// If it is an object, use curly braces
const {firstName, lastName} = obj
const {firstName: a, lastName: b} = obj
console.log(firstName);
console.log(lastName);
console.log(a);
console.log(b);


// Example 2
function calcAgeRetire(year){
  const age = new Date().getFullYear() - year;
  return [age, 65-age]
}

const[age, retirement]=calcAgeRetire(1991)
console.log(age);
console.log(retirement);

##Arrays
// Example #1
const boxes = document.querySelector(selector)
// ES5
var boxArr = Array.prototype.slice.call
boxArr.forEach(function(cur){
  cur.style.backgroundColor = 'blue'
})

// ES6
Array.from(boxes).forEach(cur =>
  cur.style.backgroundColor = 'red'
)

//  This example will iterate through a group of boxes and change the text content
// ES5
for (var i = 0; i < boxes.length; i++) {
  if (boxes[i].className === 'class') {
    continue
    // break is not used in this case as it would stop when the first instance is met
  }
  boxes[i].textContent = 'i have changed'
}
// ES6
for(const cur of boxes){
  if (boxes.className === 'class') {
    continue
  }
  cur.textContent = 'i have changed...again'
}

// Example #2
var ages = [12,23,11,34,67,17];

// ES5
var fullAge = ages.map(function(cur){
  return cur >= 34
})

console.log(fullAge) // Return the boolean value of the array values
console.log(fullAge.indexOf(true)); // Displays the first instance where it's true
console.log(ages[fullAge.indexOf(true)]); // Displays the value of the first true value

// ES6
console.log(ages.findIndex(cur => cur >= 34));  // Displays the first instance where it's true
console.log(ages.find(cur => cur >= 34)); // Displays the value of the first true value

##Spread Operators - takes an array and splits them into single values
// Example #1
function addAges(a,b,c,d){
  return a+b+c+d
}

var sum1 = addAges(18,23,45,12)
console.log(sum1);

// The above function works fine for inputted values, but what about array values instead?
// ES5
var ages = [18,23,45,12]
var sum2 = addAges.apply(null, ages)
console.log(sum2);
// ES6
const sum3 = addAges(...ages)
console.log(sum3);

// Example #2
const family1 = []
const family2 = []
// This will join the two arrays while also adding in a new member
const bigFamily = [...family1, 'Jim', ...family2]
console.log(bigFamily);

// Example #3
// This example will find all of the queried elements and change theyre font color
const h = document.querySelector('h1')
const boxes = document.querySelector('.box')
const all = [...h, ...boxes]
Array.from(all).forEach(cur => cur.style.color = 'orange')

##Rest and Default Parameters - receives single values and transforms them into an array with multiple parameters
##rest
// ES5
function fullAge(){
  // This below function will coerced the values into an array as opposed to creating a new object
  var arg = Array.prototype.slice.call(arguments)
  arg.forEach(function(e){
    console.log((2017 - e) >= 18) ;
  })
}

fullAge(1991, 2006, 2017, 1992, 1923)
// ES6
function fullAge6(...years){
  // because of the rest '...', we no longer need to coerce into an array
  years.forEach(cur => console.log((2017-cur)>=18))
}
fullAge6(1991, 2006, 2017, 1992, 1923)

#default
function family1(firstname, DOB, lastname, nationality){
  // In ES5, the ternary operators are placed within function scope
  lastname === undefined ? lastname = 'Pearman' : lastname = lastname
  nationality === undefined ? nationality = 'Canadian' : nationality = nationality
  this.firstname = firstname;
  this.lastname = lastname;
  this.DOB = DOB;
  this.nationality = nationality
}

var adrian = new family1('Adrian', 1991)
var emily = new family1('Emily', 1983, 'Diaz', 'Mexican')

// ES6
// In ES6 the ternary operator are placed with the arguemens list, makin it easier to input
function family2(firstname, DOB, lastname = 'Pearman', nationality = 'Canadian'){
  this.firstname = firstname;
  this.lastname = lastname;
  this.DOB = DOB;
  this.nationality = nationality
}

var mackenzie = new family2('Mackenzie', 2000)
var peanut = new family2('Peanut', 2013, 'Emery', 'Bermudian')

##Maps - great for creating hash maps and allows iteration as opposed to obj in the past
const question = new Map()
question.set('question', 'what is the name of the latest JavaScript version?')
question.set(1, 'ES5')
question.set(2, 'ES6')
question.set(3, 'ES2015')
question.set(4, 'ES7')
question.set('correct', 3)
question.set(true, console.log('correct answer!'))
question.set(false, console.log('unfortunately its false..'))

// the .get moethod will grab the instance in the map
console.log(question.get('question'))
console.log(question.size);

// This will delete the forth value within the map function
question.delete(4)

// This will delete everything out of the map function
question.clear()

// validating the prescense of the map element
if (question.has(4)) {
  console.log('Answer 4 is here')
}

// loop through tthe map object
question.forEach((value, key) =>
  console.log(`This is ${key} and it's set to ${value}`);
)

for (let [key, value] of question.entries()){
  console.log(`This is ${key} and it's set to ${value}`)
}

// Console logs the responses if the key matches the number type
for (let [key, value] of question.entries()){
  if (typeof(key) === 'number') {
    console.log(`Answer ${key}: ${value}`);
  }
}

// Creates a prompt request to take in a user input
const ans = parseInt(prompt('Write the correct answer?'))
// Compares the user input and validates if it is correct
console.log(question.get(ans === question.get('correct')))

##Classes and Subclasses - nothing inherently new but adds syntactical sugar for new ES6 code
##Classes
// ES5
var person5 = function(name, dob, job){
  this.name = name;
  this.dob = dob;
  this.job = job
}

person5.prototype.calcAge = function(){
  var age = new Date().getFullYear() - this.dob
  console.log(age);
}

var jim = new person5('jim', 1992, 'mailman')
jim.calcAge()

// ES6
class person6 {
  constructor (name, dob, job){
    this.name = name;
    this.dob = dob;
    this.job = job
  }
  calcAge(){
    var age = new Date().getFullYear() - this.dob
    console.log(age);
  }

  // this is only callable when calling the class name but not to the new objects
  static greeting(){
    console.log('Hey there!');
  }
}

const bill = new person6('bill', 1956, 'roadman')
bill.calcAge()
person6.greeting()

##Subclasses
// ES5
var person5 = function(name, dob, job){
  this.name = name;
  this.dob = dob;
  this.job = job
}

person5.prototype.calcAge = function(){
  var age = new Date().getFullYear() - this.dob
  console.log(age);
}

// This object below inherits all the properties of the person5 object
var athlete5 = function(name, dob, job, olyGames, medals)
{
    person5.call(this, name, dob, job)
    this.olyGames = olyGames
    this.medals = medals
}

athlete5.prototype = Object.create(person5.prototype)

athlete5.prototype.wonMedal = function(){
    function(){
      this.medals++
      console.log(this.medals);
    }
}

var johnathlete = new athlete5('john', 1989, 'runner', 2, 3)
johnathlete.calcAge()
johnathlete.wonMedal()

// ES6
class person6 {
  constructor(name, yearOfBirth, job){
    this.name = name,
    this.yearOfBirth = yearOfBirth,
    this.job = job
  }
  calculateAge(){
    var age = new Date().getFullYear - this.yearOfBirth;
    console.log(age);
  }
}

class athlete6 extends Person6{
  constructor(name, yearOfBirth, job, olyGames, medals){
    super(name, yearOfBirth, job)
    this.olyGames = olyGames
    this.medals = medals
  }

  wonMedal(){
    this.medals++
    console.log(medals);
  }
}

const johnathlete6 = new athlete6('john', 1991, 'runner', 3, 9)

johnathlete6.calcAge()
johnathlete6.wonMedal

##Best uses of ES6
For browsers that aren't ready for ES6, the code must be converted to ES5. The most common transpiler on the market is Babel.
