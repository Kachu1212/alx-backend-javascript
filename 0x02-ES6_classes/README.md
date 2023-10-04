# 0x02. ES6 classes
An introductory project on:
- How to define a `Class`
- How to add methods to a class
- Why and how to add a `static` method to a class
- How to `extend` a class from another
- Metaprogramming and symbols

## Requirements
- The code should use the js extension
- The code will be tested using the [Jest Testing Framework](https://jestjs.io/) and the command `npm run test`
- The code will be analyzed using the linter [ESLint](https://eslint.org/) along with specific rules that we’ll provide
- All of the functions must be exported

## File Descriptions
### Mandatory

1. [0-classroom.js](./0-classroom.js) - Implement a class named `ClassRoom`:

	- Prototype: `export default class ClassRoom`
	- It should accept one attribute named `maxStudentsSize` (Number) and assigned to `_maxStudentsSize`

	**Execution Example**:
	```
	bob@dylan:~$ cat 0-main.js
	import ClassRoom from "./0-classroom.js";

	const room = new ClassRoom(10);
	console.log(room._maxStudentsSize)

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 0-main.js 
	10
	bob@dylan:~$ 
	```

2. [1-make_classrooms.js](./1-make_classrooms.js) - Import the `ClassRoom` class from `0-classroom.js`.

	- Implement a function named `initializeRooms`. It should return an array of 3 `ClassRoom` objects with the sizes 19, 20, and 34 (in this order).

	**Execution Example**:
	```
	bob@dylan:~$ cat 1-main.js
	import initializeRooms from './1-make_classrooms.js';

	console.log(initializeRooms());

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 1-main.js 
	[
	  ClassRoom { _maxStudentsSize: 19 },
	  ClassRoom { _maxStudentsSize: 20 },
	  ClassRoom { _maxStudentsSize: 34 }
	]
	bob@dylan:~$
	```

3. [2-hbtn_course.js](./2-hbtn_course.js) - Implement a class named `HolbertonCourse`:

	- Constructor attributes:
		- `name` (String)
		- `length` (Number)
		- `students` (array of Strings)
	- Make sure to verify the type of attributes during object creation
	- Each attribute must be stored in an “underscore” attribute version (ex: `name` is stored in `_name`)
	- Implement a getter and setter for each attribute.

	**Execution Example**:
	```
	bob@dylan:~$ cat 2-main.js
	import HolbertonCourse from "./2-hbtn_course.js";
	
	const c1 = new HolbertonCourse("ES6", 1, ["Bob", "Jane"])
	console.log(c1.name);
	c1.name = "Python 101";
	console.log(c1);
	
	try {
	    c1.name = 12;
	} 
	catch(err) {
	    console.log(err);
	}
	
	try {
	    const c2 = new HolbertonCourse("ES6", "1", ["Bob", "Jane"]);
	}
	catch(err) {
	    console.log(err);
	}
	
	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 2-main.js 
	ES6
	HolbertonCourse {
	  _name: 'Python 101',
	  _length: 1,
	  _students: [ 'Bob', 'Jane' ]
	}
	TypeError: Name must be a string
	    ...
	TypeError: Length must be a number
	    ...
	bob@dylan:~$ 
	```

4. [3-currency.js](./3-currency.js) - Implement a class named `Currency`:
	- Constructor attributes:
		- `code` (String)
		- `name` (String)
	- Each attribute must be stored in an “underscore” attribute version (ex: `name` is stored in `_name`)
	- Implement a getter and setter for each attribute.
	- Implement a method named `displayFullCurrency` that will return the attributes in the following format `name (code)`.

	**Execution Example**:
	```
	bob@dylan:~$ cat 3-main.js
	import Currency from "./3-currency.js";

	const dollar = new Currency('$', 'Dollars');
	console.log(dollar.displayFullCurrency());

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 3-main.js 
	Dollars ($)
	bob@dylan:~$ 
	```

5. [4-pricing.js](./4-pricing.js) - Import the class `Currency` from `3-currency.js`

	- Implement a class named `Pricing`:
	- Constructor attributes:
		- amount (Number)
		- currency (Currency)
	- Each attribute must be stored in an “underscore” attribute version (ex: `name` is stored in `_name`)
	- Implement a getter and setter for each attribute.
	- Implement a method named `displayFullPrice` that returns the attributes in the following format `amount currency_name (currency_code)`.
	- Implement a static method named `convertPrice`. It should accept two arguments: `amount` (Number), `conversionRate` (Number). The function should return the amount multiplied by the conversion rate.

	**Execution Example**:
	```
	bob@dylan:~$ cat 4-main.js
	import Pricing from './4-pricing.js';
	import Currency from './3-currency.js';

	const p = new Pricing(100, new Currency("EUR", "Euro"))
	console.log(p);
	console.log(p.displayFullPrice());

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 4-main.js 
	Pricing {
	  _amount: 100,
	  _currency: Currency { _code: 'EUR', _name: 'Euro' }
	}
	100 Euro (EUR)
	bob@dylan:~$ 
	```
6. [5-building.js](./5-building.js) - Implement a class named `Building`:
	- Constructor attributes:
		- `sqft` (Number)
	- Each attribute must be stored in an “underscore” attribute version (ex: `name` is stored in `_name`)
	- Implement a getter for each attribute.
	- Consider this class as an abstract class. And make sure that any class that extends from it should implement a method named `evacuationWarningMessage`.
		- If a class that extends from it does not have a `evacuationWarningMessage` method, throw an error with the message `Class extending Building must override evacuationWarningMessage`

	**Execution Example**:
	```
	bob@dylan:~$ cat 5-main.js
	import Building from './5-building.js';

	const b = new Building(100);
	console.log(b);

	class TestBuilding extends Building {}

	try {
	    new TestBuilding(200)
	}
	catch(err) {
	    console.log(err);
	}

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 5-main.js 
	Building { _sqft: 100 }
	Error: Class extending Building must override evacuationWarningMessage
	    ...
	bob@dylan:~$ 
	```
7. [6-sky_high.js](./6-sky_high.js) - Import `Building` from `5-building.js`.

	- Implement a class named `SkyHighBuilding` that extends from `Building`:

	- Constructor attributes:
		- `sqft` (Number) (must be assigned to the parent class `Building`)
		- `floors` (Number)
	- Each attribute must be stored in an “underscore” attribute version (ex: `name` is stored in `_name`)
	- Implement a getter for each attribute.
	- Override the method named `evacuationWarningMessage` and return the following string `Evacuate slowly the NUMBER_OF_FLOORS floors`.

	**Execution Example**:	
 	```
	bob@dylan:~$ cat 6-main.js
	import SkyHighBuilding from './6-sky_high.js';

	const building = new SkyHighBuilding(140, 60);
	console.log(building.sqft);
	console.log(building.floors);
	console.log(building.evacuationWarningMessage());

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 6-main.js 
	140
	60
	Evacuate slowly the 60 floors
	bob@dylan:~$ 
	```
8. [7-airport.js](./7-airport.js) - Implement a class named `Airport`:
	- Constructor attributes:
		- `name` (String)
		- `code` (String)
	- Each attribute must be stored in an “underscore” attribute version (ex: `name` is stored in `_name`)
	- The default string description of the class should return the airport `code` (example below).

	**Execution Example**:
 	```
	bob@dylan:~$ cat 7-main.js
	import Airport from "./7-airport.js";

	const airportSF = new Airport('San Francisco Airport', 'SFO');
	console.log(airportSF);
	console.log(airportSF.toString());

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 7-main.js 
	Airport [SFO] { _name: 'San Francisco Airport', _code: 'SFO' }
	[object SFO]
	bob@dylan:~$ 
	```
