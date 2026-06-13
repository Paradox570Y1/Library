#Problem
- Frameworks implemented class based approach much earlier than popular frameworks like react, angular, vue.
- Browser could not understand class.

- Classes are just Constructor Functions only over which Syntax was added to use the same behavior as of Functions.

![[Pasted image 20250828203537.png|400]]
- Here `constructor` keyword is used to create the Constructor.
- You can't declare a member variable inside class using `let` of `var` keyword.
- Instead use `static` keyword to create a variable that is shared across all objects.
- In JavaScript you can define the properties before constructor as well but it's not required as it take properties inside constructor as public properties.

[[Transpiler]]
[[TypeScript]]


# Private Scope in JavaScript

#### Private variables in JS
```js
class Student {
	maxMarks = 500;
    #fName;  // Use hashtag before the variable name
    constructor(fName, obtainedMarks) {
        this.#fName = fName;
        this.obtainedMarks = obtainedMarks;
    }

    checkResult() {
        let percentage = (this.obtainedMarks / this.maxMarks) * 100;
        if (percentage > 40) {
            return percentage;
        } else {
            return percentage;
        }
    }

    getName() {
        return this.#fName;  // to access private field getter methods are used
    }
}
```

- `#fName` and `fName` are two different entities so incase you initialize `fname` inside of constructor instead of `#fname` then `#fname` will remain undefined.

#### Private function in JS

```js
class Student {
	maxMarks = 100; //instance variable
    #fName;  // Use hashtag before the variable name
    constructor(fName, obtainedMarks) {
        this.#fName = fName;
        this.obtainedMarks = obtainedMarks;
    }

    #checkResult() { 
        let percentage = (this.obtainedMarks / this.maxMarks) * 100;
        if (percentage > 40) {
            return percentage;
        } else {
            return percentage;
        }
    }

    getName() {
        return this.#fName;  // to access private field getter methods are used
    }
}
Student s2 = new Student("Apurav", 400);
console.log(s2.#checkResult()); //ReferenceError
```
![[Pasted image 20250830100718.png|400]]


# Static keyword in Java
- Instance variable : It belongs to the instance(object) of the class hence can't be used outside.
- To access the class variable directly outside of class make them public static.
- All the static variables can be accessed in other javascript files as well without exporting and importing if you use `defer` in current file to load javascript in header before the next javascript file then next file can access the static data.

```js
class Student {
    static maxMarks = 500;
    #fName;
    constructor(fName, obtainedMarks) {
        this.#fName = fName;
        this.obtainedMarks = obtainedMarks;
    }

    #checkResult() {
        let percentage = (this.obtainedMarks / this.maxMarks) * 100;
        if (percentage > 40) {
            return percentage;
        } else {
            return percentage;
        }
    }

    getName() {
        return this.fName;
    }
}
var s1 = new Student("Apurav", 400);
console.log(s1.maxMarks); // undefined
console.log(Student.maxMarks); //500
```

- Another way to access class variable directly outside is to declare the variables outside of class and initialize them inside it.
- `static` is a public property which is bound to the class and it can be used anywhere outside the class.

### Private static in JS

- Using '#' keyword you can make `static` property as private so that it can only be accessed inside of class.

```js
class Student {
    static #maxMarks = 500;
    #fName;
    constructor(fName, obtainedMarks) {
        this.#fName = fName;
        this.obtainedMarks = obtainedMarks;
    }

    checkResult() {
        let percentage = (this.obtainedMarks / this.#maxMarks) * 100;
        if (percentage > 40) {
            return percentage;
        } else {
            return percentage;
        }
    }

    getName() {
        return this.fName;
    }
    getMarks() {
        return this.#maxMarks
    }
}
```