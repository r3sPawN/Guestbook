# 1. Controllers responsibilities. Requirements for methods to qualify as action results

Locating the appropriate action method to call and
validating that it can be called.
– Getting the values to use as the action method's
arguments.
– Handling all errors that might occur during the
execution of the action method.
– Providing the default WebFormViewEngine class for
rendering ASP.NET page types (views)

Requirements for a method to qualify as
action:
– It must be public.
– It can’t be static.
– It can’t be an extension method
– It can’t be a constructor, getter, or setter.
– It can’t have open generic types
– It can’t be a method of the Controller base class.
– It can’t be a method of the ControllerBase base
class.
– It can’t contain ref or out parameters.
– It can’t be decorated with the NonAction action
selector.

# 2. View types in MVC
There are three view types in MVC:
Layout - is the master page in the project. It is possible to have multiple layouts in the same project. HTML DOCTYPE definition is placed in it.
Standard view - associated with a specific action of controller, renders the html for the controller/action/id request.
Partial view - reusable components that can appear on different pages of same page.
---
# 3. Objects in JavaScript
* Objects are containers, basically containing key-value pairs:
var object1 = {
  foo: 'bar',
  baz: 42
}
Object.entries(object1) // returns an array containing arrays, consisting of key and value
Object.entries(object1).map(x => console.log(x[0], x[1])) // foo bar
                                                          // baz 42
* Objects properties can be accessed:
var a = { a: 42 }
via dot notation:
console.log(a.a); // 42
or via bracket notion:
console.log(a['a']); //42


* Anything that is not a primitive type (undefined, null, number, string, boolean) is an object (or an instance) in JavaScript. That means function inherits from object.
var o = {};
console.log(typeof o === typeof []); // true   

var foo = function() { };
var obj = Object.create(foo);
console.log(Object.getPrototypeOf(obj) === foo); // true

OR

var foo = [];

function buzz() {

}

console.log(typeof foo); // "object"


console.log(typeof buzz); // "function"

console.log(foo instanceof Array);

console.log(foo instanceof Object);

console.log(buzz instanceof Array); // false

console.log(buzz instanceof Function); // true

console.log(buzz instanceof Object); // true

* Objects are copied by reference:

Primitive example:
const a = { value: 42 };
console.log(a.value) // 42
const b = a;
console.log(b.value) // 42
b.value = 33;
console.log(b.value) // 33
console.log(a.value) // ?! 33

More complex example:
function square(o) {
  o *= o;
  console.log(o); // inner scope
  return o;
}

function squareObj(o) {
  o.value *= o.value;
  return o;
}

var a = 4;

console.log(a) // 4

square(a)

console.log(a) // ?! 4, because primitive copied by value

var b = {
  value: 4
}

console.log(b.value) // 4

squareObj(b)

console.log(b.value) // ?! 16, because copy by reference

* Objects can be used as namespaces in JavaScript in order to organize variables and functions.
It is interesting to note ES6 and TypeScript which take the concept to more comprehensible manner:

class MyClass { // typescript code
  private _i:string = "private"

  public getValue() { return this._i; }
}

let classInstance = new MyClass();
console.log(classInstance.getValue()); // prints "private" in console

* Object inheritance example:
var o = {
  a: 42
}

var a = {}

console.log(a.a); // undefined

var b = Object.assign({}, o)

console.log(b.a); // 42

b.a = 33;

console.log(b.a); // 33

console.log(o.a); // unchanged

* Members of the object can be removed via delete keyword:
var b = {}

b.a = 33;

console.log(b.a); // 33


delete b.a

console.log(b.a); // undefined

* Function in the object is called a member

* Objects are compared by reference
var a = { a: 42 }
var b = a;
console.log(a === b); // true

var b = Object.assign({}, a)
console.log(a === b); // false, because different references

console.log(JSON.stringify(a) === JSON.stringify(b)); // true, because in deep they are equal

b.a = 33;

console.log(JSON.stringify(a) === JSON.stringify(b)); // false, because in deep they are not equal
---
# 4. Benefits of using AJAX in MVC. JSON and XML comparison.
Benefits of using AJAX in MVC:
+ Better interactivity and responsiveness (page does not reload)
+ Immersive UX(user experience), example would be autosuggestions in Google search, or checking for new emails in Gmail
+ Reduced connections to web server (partial content requests)
+ Reduced bandwidth due to partial content requests

JSON and XML comparison:
Below is example of same information in JSON and XML.
JSON:

{
  "person": {
    "name": "Bob",
    "gender": "male",
    "age": "33",
    "occupation": "programmer"
  }
}

XML:
<person>
	<name>Bob</name>
	<gender>male</gender>
	<age>33</age>
	<occupation>programmer</occupation>
</person>

First of all, it is noticeable, that JSON variant is much shorter in terms of length than XML.
Indeed, JSON variant is just 78 characters long, meanwhile XML is 102 characters long.
JSON can also use arrays, in example:

[
  {
		"person": {
			"name": "Bob",
			"gender": "male",
			"age": "33",
			"occupation": "programmer"
		}
	},
	{
		"person": {
			"name": "Bob",
			"gender": "male",
			"age": "33",
			"occupation": "programmer"
		}
	}
]

Meanwhile, XML would need either custom implementation, for example:

<persons>
	<person>
		<name>Bob</name>
		<gender>male</gender>
		<age>33</age>
		<occupation>programmer</occupation>
	</person>
	<person>
		<name>Bob</name>
		<gender>male</gender>
		<age>33</age>
		<occupation>programmer</occupation>
	</person>
</persons>

or use special namespace, for example xmlns:id="http://schemas.microsoft.com/2003/10/Serialization/Arrays

But most importantly, JSON can be parsed directly in JavaScript, with a use of JSON.parse.
Meanwhile, XML would require a custom parser, which would likely work in the following way:
1. Use the XML DOM to loop through the document
2. Extract values and store in variables

---
# 5. Cross Join and Inner Join in SQL
CROSS JOIN produces the result set, number of rows of which is equal to number of rows of the first table multiplied by number of rows of the second table in case WHERE clause is not provided. In case WHERE clause is provided, CROSS JOIN acts like INNER JOIN.

Example:

Table A:
[A] [B]
 0   1
 1   2
 2   3
Table B:
[B] [C]
 1   0
 0   1
 3   2

CREATE TABLE A (A INT, B INT);
CREATE TABLE B (B INT, C INT);
INSERT INTO A (A, B) VALUES (0, 1), (1,2), (2,3);
INSERT INTO B (B, C) VALUES (1, 0), (0,1), (3,2);

~> SELECT COUNT(*) AS NUMBER_OF_ROWS FROM A CROSS JOIN B;
[number_of_rows]
9

~> SELECT * FROM A CROSS JOIN B;
[A]   [A.B] [B.B] [C]
0	    1	    1	    0
0	    1	    0	    1
0	    1	    3	    2
1	    2	    1	    0
1	    2	    0	    1
1	    2	    3	    2
2	    3	    1	    0
2	    3	    0	    1
2	    3	    3	    2

In contrast, adding WHERE clause would result in:
~> SELECT * FROM A CROSS JOIN B WHERE A.B = B.B;
[A]   [A.B] [B.B] [C]
0	    1	    1	    0
2	    3	    3	    2

which resolved in the same result as SELECT * FROM A INNER JOIN B ON A.B = B.B; would.

It is important to note, that implicit notation for CROSS JOIN exists, which is:
~> SELECT * FROM A, B;

Sandbox demo is available here: http://sqlfiddle.com/#!17/77a1ac/20

INNER JOIN is a subset of CROSS JOIN, and can be deriven from CROSS JOIN by adding WHERE clause, as shown in previous example. During INNER JOIN operation, only tuples from table A and B are kept, which can be linked and these tuples are linked.

Example:
Table A:
[A] [B]
 0   1
 1   2
 2   3
Table B:
[B] [C]
 1   0
 0   1
 3   2

CREATE TABLE A (A INT, B INT);
CREATE TABLE B (B INT, C INT);
INSERT INTO A (A, B) VALUES (0, 1), (1,2), (2,3);
INSERT INTO B (B, C) VALUES (1, 0), (0,1), (3,2);

~> SELECT * FROM A INNER JOIN B ON A.B = B.B;
[A]   [A.B] [B.B] [C]
0	    1	    1	    0
2	    3	    3	    2

It is useful to note, that implicit notation also exists for INNER JOIN:
~> SELECT * FROM A, B WHERE A.B = B.B;
---
# 6. MVC Action results. Action result types.
ActionResult is an abstract class that represents the result of an action method. The class itself inherits from System.Object, and only adds one additional abstract method: ExecuteResult, which is an abstract method that the derived classes of ActionResult will implement themselves.

There are different Types of action results in ASP.NET MVC:
View Result
Partial View Result
Redirect Result
Redirect To Action Result
Redirect To Route Result
EmptyResult
JavaScriptResult
Json Result
File Result
Content Result
HttpStatusCodeResult
HttpUnauthorizedResult
HttpNotFoundResult
---
# 7. Using metadata with models.
It is possible to control editing capabilities and visibility (i.e. HiddenInput), display name for the property, control how to display the data (i.e. Password, Date, DateTime), select a display template.
---
# 8. Prototypal inheritance in JavaScript
Unlike most languages, JavaScript's object system is based on prototypes, not classes.
A prototype is a working object instance. Objects inherit directly from other objects.

Example:
function Grandparent() {
  this.myName = "Grandparent";
}
Grandparent.prototype.printA = function() { console.log("Knowledge From Grandparent, say how to introduce ourselves. Greeting is same, but name is different. So, watch how child introduced by own name and not grandparent's.", this.myName); }
Grandparent.prototype.checkTimeHabit = function() {
  console.log("Look at desk clock")
}
var gp = new Grandparent();
gp.printA(); // Knowledge From Grandparent, say how to introduce ourselves. Greeting is same, but name is different. So, watch how child introduced by own name and not grandparent's. Grandparent

function Parent() {
  this.myName = "Parent";
}
Parent.prototype = new Grandparent();
Parent.prototype.printB = function() { console.log("Knowledge From Parent"); }
Parent.prototype.checkTimeHabit = function() {
  console.log("Look at watch")
}
var p = new Parent();

// p.printA(); // Parent Does not have printA
// p.printB(); // Something that parent knows

// Let's say Grandparent learns something new
Grandparent.prototype.wisdom = function() {
  console.log("Knowledge is power")
}

try {
  Parent.wisdom();
} catch (e) {
  console.error(e); // Whoops, we will have to reinstantiate the parent, however, Child will get wisdom
}

function Child() {
  this.myName = "Child";
}
Child.prototype = new Parent();
Child.prototype.checkTimeHabit = function() {
  console.log("Look at phone")
}

var child = new Child();

child.printA(); // Knowledge From Grandparent, say how to introduce ourselves. Greeting is same, but name is different. So, watch how child introduced by own name and not grandparent's. Child
child.printB(); // Knowledge coming from Parent
child.wisdom(); // Difference
child.checkTimeHabit(); // Look at phone, but what if another child did inherit habit from parent?

function Child2() {
  this.name = "Child 2";
}

Child2.prototype = new Parent();

new Child2().checkTimeHabit(); // yep, checks watch like father


From the example above, it is clear, that printA() was inherited by Children from Grandparent;
checkTimeHabit was changed in Parent and Child. Child2 however, did not receive different function, and "Inherited" from Parent. If Parent didn't receive different function, then Child2 would do the same way as Grandparent. It can be proved by removing
Parent.prototype.checkTimeHabit = function() {
  console.log("Look at watch")
}
which will result in new Child2().checkTimeHabit() printing "Look at desk clock"

The observed effect is what is called "Prototype chaining". A good graphical explanation would be the following diagram: https://cdn-images-1.medium.com/max/1600/1*BfcQCnoGhGMrac2JMYTLPQ.png
---
# 9. Problems with using AJAX in MVC. Progressive enhancement.

Problems with using AJAX in MVC:
- Requires JavaScript enabled in Browser
- Callbacks can lead to overly complex code
- Network latency can break usability, if not handled in Asynchronous manner (JavaScript pauses execution waiting for response)
- Bookmarking is useless ("infinite scroll" is a good example)
- Is AJAX is obtrusive and web app not build in progressive enhancement manner:
  - SEO unfriendly
  - Screenreaders unfriendly => accessibility unfriendly

Progressive enhancement is a strategy, when first the functional website is build for, in case users don't support JavaScript. Then, another layer is added, on which AJAX requests are handled for users, who support JavaScript.
Differentiation of users who support JavaScript and who do not support JavaScript can be implemented in the backed with a help of Request.isAjaxRequest() in C#. I can give a lower-level example of detection, written in PHP:
/* AJAX check  */
if(!empty($_SERVER['HTTP_X_REQUESTED_WITH']) && strtolower($_SERVER['HTTP_X_REQUESTED_WITH']) == 'xmlhttprequest') {
	/* special ajax here */
	die($content);
}
---
# 10. Outer Joins in SQL
Outer join does not require for each record in one table to have a matching (linking by) record in the another table => non-linked records are kept in such case.

Example:

Table A:
[A] [B]
 0   1
 1   2
 2   3
Table B:
[B] [C]
 1   0
 0   1
 3   2

CREATE TABLE A (A INT, B INT);
CREATE TABLE B (B INT, C INT);
INSERT INTO A (A, B) VALUES (0, 1), (1,2), (2,3);
INSERT INTO B (B, C) VALUES (1, 0), (0,1), (3,2);

~> SELECT * FROM A FULL OUTER JOIN B ON A.B = B.B;

Would result as:
[A]	    [A.B]   [B.B]   [C]
(null)  (null)  0       1
0	      1	      1	      0
1	      2	      (null)	(null)
2	      3	      3	      2

From the result we can observe, that matching records (B 1 and B 3) were linked,
however, non matching ones (B 0 and B 2) were either not omitted, and missing values were set to NULL;


There are three types of Outer joins:
Left Outer Join, Right Outer Join and Full Outer Join.

We have already reviewed the result of FULL OUTER JOIN in example above, therefore, will only review LEFT OUTER JOIN and RIGHT OUTER JOIN to contrast.

LEFT OUTER JOIN with same data will resolve into:
~> SELECT * FROM A LEFT OUTER JOIN B ON A.B = B.B;
[A]	    [A.B]   [B.B]   [C]
0	      1	      1	      0
1	      2	      (null)	(null)
2	      3	      3	      2

It is instantly noticeable, that the result differs from previous output in absence of one row!

Because LEFT OUTER JOIN is from OUTER JOIN family, the mechanism should have logical connection to mechanisms of other siblings of the family. Indeed, the output is same in:
[A]	    [A.B]   [B.B]   [C]
0	      1	      1	      0
1	      2	      (null)	(null)
2	      3	      3	      2
and differs in:
[A]	    [A.B]   [B.B]   [C]
(null)  (null)  0       1

This is because
[A]	    [A.B]   [B.B]   [C]
(null)  (null)  0       1
comes from table B, which is right table, and by specifying LEFT, we meant to keep non-linking entries only from the left table, therefore non-linking entries from the right table were omitted.

The mechanism of the RIGHT OUTER JOIN is similar to the LEFT OUTER JOIN, except that non-linking entries are kept only from the right table => non-linking entries from the left table are omitted. It is observable from the output:
~> SELECT * FROM A RIGHT OUTER JOIN B ON A.B = B.B;
[A]	    [A.B]   [B.B]   [C]
(null)	(null)	0	      1
0	      1	      1	      0
2	      3     	3	      2

Again, the output differs from the FULL OUTER JOIN in a single row:
[A]	    [A.B]   [B.B]   [C]
1	      2	      (null)	(null)

and it can be observed, that this row would derive from table A, which is LEFT table => non-linking entries from the LEFT table are omitted and non-linking entries only from the RIGHT table are kept.

The Sandbox with the code introduced above is available at the following link: http://sqlfiddle.com/#!17/77a1ac/11

Different JOIN types are also well illustrated in the following image: https://i.stack.imgur.com/qje6o.png
