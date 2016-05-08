---
 layout: post
 title: Test Driven Development in JavaScript
 subtitle:
---

# Test Driven Development in JavaScript

## Past
When I was first learning to unit test, I began to wonder how this technique was applicable in JavaScript (JS). Around this same time QUnit was one of the more popular testing frameworks. Developed by JQuery, QUnit provided a simple assertion framework. To use this framework, the business logic needed to be decoupled from the presentation logic. For maintainability, this business logic was broken into smaller modules and these were placed in a separate file. These files, along with their third-party dependencies, required bundling to create the JS application. The concept of bundling a JS application was still in its infancy. These early struggles led me to abandon unit testing in JS but I never gave up on JS.

**Presentation and business logic coupled together**

~~~javascript
//index.js
(function(){
	function isTheFormValid(valuesInTheForm){
		//validate the form
	}

	$(document).ready(function(){
		$('#submit').click(function(){
			var valuesInTheForm = {
				//store the values from the form
			};
			if(isTheFormValid(valuesInTheForm)){
				//do something
			}
		});
	})
}());
~~~

~~~html
<!-- index.html -->
<html>
	<head>
		<!--load third-party modules-->
		<script src="index.js"></script>
	</head>
	<body>
	</body>
</html>
~~~

**Decoupled presentation and business logic**

~~~javascript
//validation.js
var validation = (function(){
	return function(){
		//perform the validation
	}
());
~~~

~~~javascript
//index.js
$(document).ready(function(){
	//this assumes that the validation module is already loaded
	validation()
})
~~~

~~~html
<!-- index.html -->
<html>
	<head>
		<!--load third-party modules-->
		<!--load local modules-->
		<script src="validation.js"></script>
		<script src="index.js"></script>
	</head>
	<body>
	</body>
</html>
~~~

## Present
As I became proficient in JS it never felt right to code without unit testing. I knew I needed unit testing for my application to succeed. Once JS became widely used in web development, client applications, server application and hybrid applications I started using unit test in my applications.

With build tools like Grunt, Gulp and Webpack it is easier then ever to build and unit test a JS application. These tools allow developers to integrate automated testing into their development process. Once this process is in place, developers can start using test drive development (TDD). Using TDD, developers can improve their JS knowledge by immediately testing an assumption. Testing assumptions can also help in understanding a small part of a new framework. Finally, TDD focuses more on the quality of the code and less on the quantity of code created.

**A modern application that is easier to test**

~~~javascript
//validation.js
export default function(){
	//perform validation
}
~~~

~~~javascript
//index.js
import $ from 'jquery'
import validation from 'validation.js'

$(document).ready(function(){
	//the above import statement guarantees that
	//validation modules is loaded
	validation()
})
~~~

~~~html
<!-- index.html -->
<html>
	<head>
		<!--this single JS file contains every resource in the application-->
		<script src="bundle.js"></script>
	</head>
	<body>
	</body>
</html>
~~~

## Future
Presently, the next challenge facing developers is testing the presentation layer. Automated testing of the presentation layer is possible if the application is correctly designed. I think this challenge will become easier with the use of a virtual document object model (DOM).


With TDD in place I am less fearful of releasing and of the response from users. TDD is where I start when creating a new JS application. For every application I have written TDD is the underlying reason for success.
