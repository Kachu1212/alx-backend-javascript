# 0x03. ES6 data manipulation
An introductory project on:
- How to use map, filter and reduce on arrays
- Typed arrays
- The Set, Map, and Weak link data structures

## Requirements
- The code should use the js extension
- The code will be tested using the [Jest Testing Framework](https://jestjs.io/) and the command `npm run test`
- The code will be analyzed using the linter [ESLint](https://eslint.org/) along with specific rules that we’ll provide
- All of the functions must be exported

## File Descriptions
### Mandatory
1. [0-get_list_students.js](./0-get_list_students.js) - Create a function named `getListStudents` that returns an array of objects.
	- Each object should have three attributes: `id` (Number), `firstName` (String), and `location` (String).
	- The array contains the following students in order:
		- `Guillaume`, id: `1`, in `San Francisco`
		- `James`, id: `2`, in `Columbia`
		- `Serena`, id: `5`, in `San Francisco`

	**Execution Example**:
	```
	bob@dylan:~$ cat 0-main.js
	import getListStudents from "./0-get_list_students.js";

	console.log(getListStudents());

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 0-main.js 
	[
	  { id: 1, firstName: 'Guillaume', location: 'San Francisco' },
	  { id: 2, firstName: 'James', location: 'Columbia' },
	  { id: 5, firstName: 'Serena', location: 'San Francisco' }
	]
	bob@dylan:~$ 
	```
2. [1-get_list_student_ids.js](./1-get_list_student_ids.js) - Create a function `getListStudentIds` that returns an array of ids from a list of object.
	- This function is taking one argument which is an array of objects - and this array is the same format as `getListStudents` from the previous task.
	- If the argument is not an array, the function is returning an empty array.

	**Execution Example**:
	```
	bob@dylan:~$ cat 1-main.js
	import getListStudentIds from "./1-get_list_student_ids.js";
	import getListStudents from "./0-get_list_students.js";

	console.log(getListStudentIds("hello"));
	console.log(getListStudentIds(getListStudents()));

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 1-main.js 
	[]
	[ 1, 2, 5 ]
	bob@dylan:~$ 
	```
3. [2-get_students_by_loc.js](./2-get_students_by_loc.js) - Create a function `getStudentsByLocation` that returns an array of objects who are located in a specific city.
	- It should accept a list of students (from `getListStudents`) and a `city` (string) as parameters.

   **Execution Example**:
   	```
	import getListStudents from "./0-get_list_students.js";
	import getStudentsByLocation from "./2-get_students_by_loc.js";

	const students = getListStudents();

	console.log(getStudentsByLocation(students, 'San Francisco'));

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 2-main.js 
	[
	  { id: 1, firstName: 'Guillaume', location: 'San Francisco' },
	  { id: 5, firstName: 'Serena', location: 'San Francisco' }
	]
	```
4. [3-get_ids_sum.js](./3-get_ids_sum.js) - Create a function `getStudentIdsSum` that returns the sum of all the student ids.
	- It should accept a list of students (from `getListStudents`) as a parameter.
	
   **Execution Example**:
	```
	bob@dylan:~$ cat 3-main.js
	import getListStudents from "./0-get_list_students.js";
	import getStudentIdsSum from "./3-get_ids_sum.js";

	const students = getListStudents();
	const value = getStudentIdsSum(students);

	console.log(value);

	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 3-main.js 
	8
	bob@dylan:~$ 
	```
5. [4-update_grade_by_city.js](./4-update_grade_by_city.js) - Create a function `updateStudentGradeByCity` that returns an array of students for a specific city with their new grade
	- It should accept a list of students (from `getListStudents`), a `city` (String), and `newGrades` (Array of “grade” objects) as parameters.
	- `newGrades` is an array of objects with this format:
	```
	   {
	    studentId: 31,
	    grade: 78,
	  }
 	```
 	- If a student doesn’t have grade in `newGrades`, the final grade should be `N/A`.
	
   **Execution Example**:
  	```
   	bob@dylan:~$ cat 4-main.js
	import getListStudents from "./0-get_list_students.js";
	import updateStudentGradeByCity from "./4-update_grade_by_city.js";
	
	console.log(updateStudentGradeByCity(getListStudents(), "San Francisco", [{ studentId: 5, grade: 97 }, { studentId: 1, grade: 86 }]));
	
	console.log(updateStudentGradeByCity(getListStudents(), "San Francisco", [{ studentId: 5, grade: 97 }]));
	
	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 4-main.js 
	[
	  {
	    id: 1,
	    firstName: 'Guillaume',
	    location: 'San Francisco',
	    grade: 86
	  },
	  { id: 5, firstName: 'Serena', location: 'San Francisco', grade: 97 }
	]
	[
	  {
	    id: 1,
	    firstName: 'Guillaume',
	    location: 'San Francisco',
	    grade: 'N/A'
	  },
	  { id: 5, firstName: 'Serena', location: 'San Francisco', grade: 97 }
	]
	bob@dylan:~$ 
	```

6. [5-typed_arrays.js](./5-typed_arrays.js) - Create a function named `createInt8TypedArray` that returns a new `ArrayBuffer` with an `Int8` value at a specific position.
	- It should accept three arguments: `length` (Number), `position` (Number), and `value` (Number).
	- If adding the value is not possible the error `Position outside range` should be thrown.
	
   **Execution Example**:	
 	```
	bob@dylan:~$ cat 5-main.js
	import createInt8TypedArray from "./5-typed_arrays.js";
	
	console.log(createInt8TypedArray(10, 2, 89));
	
	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 5-main.js 
	DataView {
	  byteLength: 10,
	  byteOffset: 0,
	  buffer: ArrayBuffer {
	    [Uint8Contents]: <00 00 59 00 00 00 00 00 00 00>,
	    byteLength: 10
	  }
	}
	bob@dylan:~$ 
	```
7. [6-set.js](./6-set.js) - Create a function named `setFromArray` that returns a `Set` from an array.
	- It accepts an argument (Array, of any kind of element).
	
   **Execution Example**:
	```
 	bob@dylan:~$ cat 6-main.js
	import setFromArray from "./6-set.js";
	
	console.log(setFromArray([12, 32, 15, 78, 98, 15]));
	
	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 6-main.js 
	Set { 12, 32, 15, 78, 98 }
	bob@dylan:~$
 	```
 8. [7-has_array_values.js](./7-has_array_values.js) - Create a function named `hasValuesFromArray` that returns a boolean if all the elements in the array exist within the set.
	- It accepts two arguments: a `set` (Set) and an `array` (Array).
	
   	**Execution Example**:
   	```
  	bob@dylan:~$ cat 7-main.js
	import hasValuesFromArray from "./7-has_array_values.js";
 
	console.log(hasValuesFromArray(new Set([1, 2, 3, 4, 5]), [1]));
	console.log(hasValuesFromArray(new Set([1, 2, 3, 4, 5]), [10]));
	console.log(hasValuesFromArray(new Set([1, 2, 3, 4, 5]), [1, 10]));
	
	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 7-main.js 
	true
	false
	false
	bob@dylan:~$
    	```
 9. [8-clean_set.js](./8-clean_set.js) - Create a function named `cleanSet` that returns a string of all the set values that start with a specific string (`startString`).
	- It accepts two arguments: a `set` (Set) and a `startString` (String).
	- When a value starts with `startString` you only append the rest of the string. The string contains all the values of the set separated by `-`.
	
   	**Execution Example**:
	```
	bob@dylan:~$ cat 8-main.js
	import cleanSet from "./8-clean_set.js";
	
	console.log(cleanSet(new Set(['bonjovi', 'bonaparte', 'bonappetit', 'banana']), 'bon'));
	console.log(cleanSet(new Set(['bonjovi', 'bonaparte', 'bonappetit', 'banana']), ''));
	
	bob@dylan:~$ 
	bob@dylan:~$ npm run dev 8-main.js 
	jovi-aparte-appetit
	
	bob@dylan:~$ 
	```
### Advanced
