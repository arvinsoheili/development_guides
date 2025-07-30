# What is TypeScript?
Benefits of TS VS JS:
- Static Typing: in Static typing we should declare dataType for Variables like `let x: number = 10;` then you can't change it to a string.
- Code completion
- Refactoring
- Shorthand notations

Drawbacks:
- Compilation: we give codes to TypeScript compiler to compile it into javascript code.
- Discipline Coding: TS is mostly used for larger Project than JS which is better for simple projects. because of disiplined coding in TS you won't waste time on fixing bugs.


# Setting up the Development Enviroment

### Installing TypeScript
1. open terminal type `npm i -g typescript` to install TS compiler.
you can check version by `tsc -v`.

### Creating first TS file
1. make your folder.
2. make file with `.ts` extention. example: `index.ts`.
3. after writing codes run `tsc index.ts` to compile the file into JS file.

when you're declaring variables in TS you should declare the data type by annotations(`:`) mark like:
```TypeScript
let var: number = 10;
```

### Making a confiuraton file for TypeScript Compiler

1. open terminal.

2. type `tsc --init`.

3. this will make a `tsconfig.json` file.

4. in config file we can change value of the "target" key, which will declare the target version of javaScript we want to compile the TS codes. values: from `es2015` to `es2024`. choose carefully. the standard version is `es2016`.

4. in next setting we navigate to modules section, uncomment `rootdir` settings and change value to `./src`. now move index.ts to `src` folder you created.

5. then what we gonna do is navigate to `Emit` section, uncomment `outDir` setting and change value to `./dist`. this will compile the JS file into a distributable folder named "dist".

6. now we can uncomment `removeComments` settings in case of we want to remove any comments when we compile the TS file. remember to set the value to `True`.

7. also it is better to uncomment `noEmitOnError` setting, so if there is any errors in TypeScript code the JavaScript file doesn't generate.

8. now you can run `tsc` in terminal, this will compile every TS file in src folder.

### Debuging TypeScript Codes
1. in cofig file navigate to `Emit`, uncomment the `sourceMap` and set it to `True`. it will maps JavaScript generated code. after executing `tsc` it will generate a map file with `.js.map` extention.
2. now head to TS file add some logic. 
3. add a breakpoint anywhere you want.
4. goto debug panel > create launch.json file > choose Node.js. this will create new file with some configuration.
5. find `program` settings, add `"preLaunchTask": "tsc: build - tsconfig.json",`
6. now you can go to `index.ts` and `launch debug panel` and `launch program`. or you can use `F5`.
7. in debug panel, you can see some dropdowns like `Variables`, `Watch` and etc. you can see some local instances in `Varables>Local dropdown`. you can test some `functions` and `variables` in `Watch` dropdown. 

# Fundimentals
### Built-in Types
JavaScript has these Types: `number`, `string`, `boolean`, `null`, `undefined`, `object`.

In other hands TypeScript has these Types: `any`, `unknown`, `never`, `enum`, `tuple`. also it contains every JavaScript Types.

In TypeScript file when you declare a variable with value the compiler will automatically annotate the type. but if you declare a Variable without a value like: `let x;`, the compiler will annotate the type as `any`.

### The any Type
when you declare a variable without a value, TS compiler will annotate it as `any`. it means that `any` data can assign to this variable.
```TypeScript
let level;
level = 1;
level = 'a';
```
the final level value is `"a"` but we assign a number to it earlier and there will be no errors.

#### it is way more better to avoid using any type, as it will cause alot of error later.

### Arrays
as we say, avoid `any` type when declaring a variable. 

In TypeScript, when declaring an `array` variable you want to annotate the type. so you annotate it like with `string`, then you must add `[]` at the end of the type:
```TypeScript
let numbers: number[] = [1, 2, 3];
```
### Tuples
Speaking of declaring `arrays`, imagine we have `arrays` that the first value is `number`, the second value is `string`. are we going to use `any` type?

Absolutly no.

TypeScript has this feature named tuple. it is working like this:
```TypeScript
let user: [number, string] = [1, 'arvin'];
```
this will help you avoid using `any` type.

### Enums
we can declare enums like this:
```TypeScript
enum Size { Small = 1, Medium, Large };
let mySize: Size = Size.Medium;
console.log(mySize);
```
TypeScript will automatically compile the values of `Medium` and `Large` but this will only work with `numbers`. if you have `strings` you must assign all of the values.

anyway when you compile this code you will get something like this in JavaScript:
```JavaScript
"use strict";
var Size;
(function (Size) {
    Size[Size["Small"] = 1] = "Small";
    Size[Size["Medium"] = 2] = "Medium";
    Size[Size["Large"] = 3] = "Large";
})(Size || (Size = {}));
;
let mySize = Size.Medium;
console.log(mySize);
```
what i wanna point is: if you add a constant(`const`) before `enum` declaring like this:
```TS
const enum Size { Small = 1, Medium, Large};
```
it will compile it in `JS` like this:
```JS
"use strict";
;
let mySize = 2;
console.log(mySize);
```
So, what i meant was with a single `const` you can do a `huge optimize` to your generated JS code. but the output will be the same.

### Functions
if we declare a `function` in TS it will automatically annotate the output to the function: like if you return nothing it will annotate it as `void`, or if you return number it will annotate it as `number`. but the best practice is to always annotate your functions.

also it is best to annotate function `Attributes` too, like: `function(x: number, i: string)`;

for now go to `tsconfig.ts` navigate to `Type Checking` section, uncomment `noUnusedParameters` settings and set it to `True`. this will activate warnings if the parameters of a function isn't used in the function.

Now imagine if we declare a function that looks like this:
```TS
function calculateTax(income: number): number {
    if (income < 50000)
        return income * 1.2;
}
```
this function has a return only if income is less than 50,000. so if the function return unidentified, it will goes against our function rules that we annotate.

for fixure we want to open `tsconfig.ts` again. navigate to `Type Checking` section, uncomment `noImplicitReturns` and set it to `true`. this setting will warn you if the function has such a problem.

another settings you wanna turn on is `noUnusedLocals` in `Type Checking` section. this will warn that a variable has no value. it is helpful to prevent declaring variables with `any` Type.

### Objects
you can declare objects in TS with property types like this:
```TS
let employee: {
    id: number,
    name: string
} = {
    id: 1,
    name: 'arvin'
};
```
what if we don't want to change `ID` accidentally? simply add readonly before declaring `type`: `readonly id: number,`.

how to add a functional property? do this:
```TS
let employee: {
    id: number,
    name: string,
    retire: (date: Date) => void
} = {
    id: 1,
    name: 'arvin',
    retire: (date: Date) => {
        console.log(date);
    }
};
```
you can also make a property `optional` by adding `?` after property name: `fax?: string,`

# Advanced Types
### type Aliases
imagine you going to have another employee object. then you need to declare types again in other object. this is not good. we must use DRY rule: Don't Repeat Yourself.
so what we gonna do is to make a type alias for employee objects:
```TS
type Employee = {// always use pascal case for type aliases name
    readonly id: number,
    name: string,
    retire: (date: Date) => void
}

let employee: Employee = {
    id: 1,
    name: 'arvin',
    retire: (date: Date) => {
        console.log(date);
    }
}
```
now we can add other objects with shape of employee like other employees.

### Union Types
did you know you can assign multiple types to a data?
you can do it like this: `x: number | string`. this called `Union Types`.
therefor you can do `narrowing` on `union types` by using `typeof` like this:
```TS
if(typof x === 'number')
    return x*2;
else
    return parseInt(x)*2;
```
this is called `Narrowing`.

### Intersection Types
you can make types in typeScript.
you make a type like this: (i intentionally declared an empty function for educational purposes.)
```TS
type Draggable = {
    drag: () => void
};
```
but Intesection types are when you combine two custom types to make a single type. imagine i make another custom type named resizable. e.g.
```TS
type UIWidget = Draggable & Resizable;

let textBox: UIWidget = {
    drag: () => {},
    resize: () => {}
}
```
### Literal Types
imagine you want a type that only accepts 50 or 100. what you can do is use Literal Types. e.g.
```TS
type Quantity = 50 | 100;
let quantity: Quantity = 100;

// you can use it on strings too.
type Metric = 'cm' | 'inch';
```

### Nullable Types
in a function we declared there a value that might be null, but typescript compiler don't let us to have null value. so we use null type as a union type in the function:
```TS
function greet(name: string | null | undefined) {
    if (name)
        console.log(name.toUpperCase());
    else
        console.log("Hola!");
}

greet(null);
```
### Optional Chaining
if we have a function that may return a null or undifined value. we should have problems. so we use Optional Chaining, like:
```TS
let customer = getCustomer(1); // 1 is id of the customer we made a function for.
// Optional property access operator
console.log(customer?.birthday?.getFullYear()); // the "?." is "Optionaling the operator".

// Optional element access operator
// will used for arrays that may be empty.
// customers?.[0]

//Optional call
let log: any = null;
log?.('a');
```

### Interfaces
Here we use an `interface` that describes objects that have a `firstName` and `lastName` field. In TypeScript, two types are compatible if their internal structure is compatible. This allows us to implement an interface just by having the shape the interface requires, without an explicit `implements` clause.
```TS
interface Person {
  firstName: string;
  lastName: string;
}
 
function greeter(person: Person) {
  return "Hello, " + person.firstName + " " + person.lastName;
}
 
let user = { firstName: "Jane", lastName: "User" };
 
document.body.textContent = greeter(user);
```

An interface declaration is another way to name an object type:

```TS
interface Point {
  x: number;
  y: number;
}
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

 TypeScript is only concerned with the structure of the value we passed to `printCoord` - it only cares that it has the `expected` properties. Being concerned only with the `structure and capabilities` of types is why we call TypeScript a `structurally typed` type system.

# Narrowing Types
### typeof
as we learn [here](#union-types), we can narrowing type with `typeof` but typeof isn't the only one.`

so we use
### in
imagine a user login page. the user can be either a Standard user or an Admin user.
```TS
declare function getStandardSessionToken(name: string, ttl: number): string;
declare function getAdminSessionToken(name: string, accessLevel: string): string;
```

we gonna declate two types, one for standard and one for admin user:
```TS
type StandardUser = {
    name: string;
    SessionTTL: number;
}

type AdminUser = StandardUser & {
    isAdmin: true,
    access: "read-admin" | "write-admin"
};
```

Now we gonna return tokens is a function that the user can be standard or admin, so we use `in` here.
```TS
function login(user: StandardUser | AdminUser) {
    if ("isAdmin" in user) {
        return getAdminSessionToken(user.name, user.access);
    }
    return getStandardSessionToken(user.name, user.sessionTTL);
}
```
we checked the input type if it has `isAdmin` or not to show the correct response.

### Type predicates
the best use of type predicates is when you want to filter out some data. for example the same user boilerplate.
```TS
type User = StandardUser | AdminUser;

const users: User[] = [
    { name: "jane", sessionTTL: 3 },
    { name: "bob", sessionTTL: Infinity, isAdmin: true, access: "read-admin" },
    { name: "leah", sessionTTL: Infinity, isAdmin: true, access: "write-admin" },
    { name: "joe", sessionTTL: 5 }
];
```
But this time we want to filter only standard users.
```TS
const standardUsers = users.filter((user): user is StandardUser => {
    return !(user as AdminUser).isAdmin;
});
```
alright we used `is` when to filter out only standard users. and the return statment declares that the users are standard or admins with boolean value.

### Discriminated Unions
now we got a user which can have 3 types. we want to have an outcome for each of them. so we use switch:
```TS
type StandardUser = {
    type:"standard";
    name: string;
    sessionTTL: number;
}

type AdminUser = {
    type: "admin";
    name: string;
    access: "read-admin" | "write-admin";
}

type ProspectUser = {
    type: "prospect";
}

type User = StandardUser | AdminUser | ProspectUser;

function login(user: User) {
    switch (user.type) {
        case "standard":
            return getStandardSessionToken(user.name, user.sessionTTL);
        case "admin":
            return getAdminSessionToken(user.name, user.access);
        case "prospect":
            return null;
        default:
            const notPossible: never = user;
            throw new Error(`unexpected user type: ${user}`);
    }
}
```
In this case we got something named `Exhaustive Switch`, we have a `switch` with 3 `cases` which will do a job for every type, and a `default` that returns error.

### Instanceof
The `instanceof` operator checks whether an object is an instance of a particular class or constructor function.

Think of it like this:

> “Was this object created using this class (or constructor)?”

```TS
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

const dog = new Animal("Rover");

console.log(dog instanceof Animal); // true
```
- dog was created using the new Animal(...) constructor.

- So dog `instanceof` Animal returns true.

`instanceof` also helps narrow the type inside conditional blocks.
```TS
class Dog {
  bark() {
    console.log("Woof!");
  }
}

class Cat {
  meow() {
    console.log("Meow!");
  }
}

function makeSound(animal: Dog | Cat) {
  if (animal instanceof Dog) {
    animal.bark(); // ✅ TypeScript knows this is a Dog here
  } else {
    animal.meow(); // ✅ So this must be a Cat
  }
}
```
Thanks to `instanceof`, TypeScript knows which type animal is inside the `if` and `else` blocks.

Also only use `instanceof`:

- When working with classes

- When you need to narrow a union type

- When using new to create objects

<hr/>

- instanceof checks if an object comes from a specific class.

- It uses the prototype chain to do this.

- In TypeScript, it helps narrow types and acts as a type guard.

- Only works with classes or things created using new.


# Type Assertions

A type assertion tells TypeScript:

> “Trust me, I know what I’m doing — this value is actually of this specific type.”

It does not change the actual value at runtime — it just tells the TypeScript compiler how to treat the value at compile time.`value as Type`
```TS
let someValue: unknown = "hello world";

// Tell TypeScript: "Trust me, it's a string"
let strLength = (someValue as string).length;

console.log(strLength); // 11
```
Here:

- TypeScript doesn’t know what `someValue` is (unknown).

- We assert it's a `string` using `as string`.

- Now we can safely call `.length` on it.
  
### When to use Type Assertions

Use them when you’re sure of a value’s type but TypeScript can’t infer it.

Example: Getting a DOM element
```TS
const input = document.getElementById("myInput") as HTMLInputElement;
input.value = "Hello!";
```
Without as HTMLInputElement, TypeScript would think it’s just HTMLElement, which doesn't have a value property.

#### Warning
1. **Doesn’t convert values**
```TS
let num = "123" as number; // ❌ still a string at runtime
```
TypeScript won't turn "123" into a number. It only pretends it's a number, which could lead to bugs.

2. **Be careful — it's your responsibility**

    TypeScript will not verify that the assertion is actually correct. You're telling it to stop checking.

3. **Avoid unless necessary**

    It’s best to let TypeScript infer types when possible. Overusing as can hide real type problems.
