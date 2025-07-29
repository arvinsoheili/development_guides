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
