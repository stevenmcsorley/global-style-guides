[**↺**BACK](./README.md)
# TypeScript StyleGuide and Coding Conventions


These represent a set of best practices for all UI developers. It was created so the UI code is more consistent, easier to maintain, read and test.
Because every developer has idiosyncrasies it is expected that some of the ideas in this document may raise questions. We are open to discussion and learning new ways of doing code faster and more productive. If that is the case please don't hesitate to contact one of the UI developers.

 - [File structure](#file-structure)
 - [Naming conventions](#naming-conventions)
 - [Rule of One](#rule-of-one)
 - [Linting & Formatting](#linting--formatting)
 - [Testing](#testing)
 - [Barrel](#barrel)
 - [This](#this)
 - [Variable](#variable)
 - [Types](#types)
 - [Class](#class)
 - [Interface](#interface)
 - [Enum](#enum)
 - [Arrow functions](#arrow-functions)
 - [Template strings](#template-strings)
 - [Async & Await](#async--await)
 - [Destructuring](#destructuring)
 - [Spread operator](#spread-operator)
 - [Inspiration for this Guideline](#inspiration-for-this-guideline)

## File structure
* Group files by functionality or type.
  
 ***Avoid***
 ```ts
 /src/button.component.vue
     /api.service.ts
     /utils.ts
     /layout.scss
 ```
 **Do**
 ```ts
 /src/components/button.component.vue
     /apis/client.service.ts
     /shared/utils.ts
     /style/layout.scss
 ```
* Less then 4 nesting levels. 
  
***Avoid***
 ```ts
 /src/components/basic/buttons/big/button-1.vue
                             /small/button-2.vue
                /classic/buttons/animated/button-11.vue
                                         /button-33.vue
      /services/apis/shared/alfa-api.service.ts
                           /beta-api.service.ts
 ```
 **Do**
 ```ts
 /src/components/buttons/button-basic-big-1.vue
                        /button-basic-small-1.vue
                        /button-classic-animated-11.vue
                        /button-classic-animated-33.vue
     /shared_apis/alfa-api.service.ts
                 /beta-api.service.ts
 ```
* Less then 20 file per folder.

>**Why?** Because is easier to find files in a project, to refactor and maintain.


## Naming conventions
* Folders: lowercase with "_" separating words.   
 ```ts
 shared_apis
 customer_orders
 ```
* Files: lowercase with "-" separating words, "." separating types.  
 ```ts
 alfa-api.service.ts
 customer-orders.spec.ts
 login-box.vue
 ```
* Variables/Properies/Attributes/Members/Functions/Methods : camelCase
* Classes/Interfaces/Enums/Types: PascalCase
 ```ts
 const globalAPI = ''
 const user = {
   lastName: 'Foo',
   firstName: 'Bar'
 }
 function getFullName () {
   return `${user.firstName} ${user.lastName}`
 }
 type 
 enum UserType {
   adminManager: 'admin',
   simpleClient: 'client'
 }
 interface UserModel {
   lastName: string
   firstName: string
   usertype?: UserType
 }
 class User {
   lastName!: string
   firstName!: string
   getFullName () {
     return `${this.firstName} ${this.lastName}`
   }
 }
 ```


## Rule of One
* **One thing per file**, such as a component, service, model. 
* Enums, types, and interfaces can make an exception if the files don't get too big to manage.
>**Why?** One component per file makes it far easier to read, maintain, and avoid collisions with teams in source control. It also avoids hidden bugs and makes the code more reusable, easier to read, and less mistake-prone.

## Linting & Formatting
* Use ESLINT with the standardJS rules. Please have a look if you are not familiar with them [standardJS docs](https://standardjs.com/). 
* Use an IDE with preset linting or set it up appropriately and run lint command before a commit.
>**Why?** It is easier to read, maintain code and deal with source control merge/conflict.

## Testing
* Use `jest` for unit testing and if possible implement TDD. For Vue, projects read this more in-depth [guide](https://lmiller1990.github.io/vue-testing-handbook/#what-is-this-guide) on how to write tests for different parts of a project.
>**Why?** Tests keep the code free of bugs and ensure that it does what is suppose to do.

## Barrel
* A barrel is a way to rollup exports from several files into a single convenient module. The barrel itself is a module file that re-exports selected exports of other files. Best used in folders with files that are used in a lot of places.
```ts
// icons/index.ts
import IconAdd from './IconAdd.vue'
import IconArrowLeft from './IconArrowLeft.vue'
import IconArrowRight from './IconArrowRight.vue'
import { IconTypes } from './IconTypes'

const AllIcons = {
 IconAdd,
 IconArrowLeft,
 IconArrowRight,
}

export {
 AllIcons,
 IconAdd,
 IconArrowLeft,
 IconArrowRight,
 IconTypes
}

// use
import { AllIcons, IconTypes } from '.icons'
@Component({
 components: {
 ...AllIcons
 }
})
...
import { 
 IconArrowLeft,
 IconArrowRight
} from '.icons'
@Component({
 components: {
 IconArrowLeft,
 IconArrowRight
 }
})
...
```
>**Why?** The imports became cleaner and easy to read.

## This
* Make sure that you know what `this` is, try to avoid ambiguous situations. If you are not sure here is more on that subject [Microsoft Typescript Handbook](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Functions.md#this).
* Related to [Arrow functions](#arrow-functions).

## Variable
* Use camelCase for variable/property/attribute and function/method names.
* Use `let` or `cont`, avoid *var*.
* Use descriptive and unambiguous names.  
  
***Avoid***
 ```ts
 const ProdTog = true
 var CList = []
 LoadIT () {
 cList = [1, 2, 3]
 }
 ```
**Do**
 ```ts
 const productionToggle = true
 let clientList = []
 loadList () {
 clientList = [1, 2, 3]
 }
 ``` 
 >**Why?** The code is clean, easy to read and less prone to silly bugs.

## Types
* Specify type of variable/property/attribute and function/method so typechecking is unambiguous.
* Use custom types when you might need a union or intersection. Use PascalCase for name.
* Use `keyof` for intersection types.
  ```ts
  type A = { a: string };
  type B = { b: string };

  type T1 = keyof (A & B);  // "a" | "b"
  type T2<T> = keyof (T & B);  // keyof T | "b"
  type T3<U> = keyof (A & U);  // "a" | keyof U
  type T4<T, U> = keyof (T & U);  // keyof T | keyof U
  type T5 = T2<A>;  // "a" | "b"
  type T6 = T3<B>;  // "a" | "b"
  type T7 = T4<A, B>;  // "a" | "b"
  ```
* Use [interfaces](#interface) if possible in place of object or any. 
* Use [enums](#enums) in place of hardcoded strings or numbers.  

***Avoid***
 ```ts
 let theFoo: number | { someProperty: number } = 6
 let zoo = [new Rhino(), new Elephant(), new Snake()];

 function(status: string | boolean) {
 //do stuff to list
 return status
 }

 let clientData: any = {
 id: '101010101',
 name: 'Foo',
 type: 'Bar'
 }
 ```
 **Do**
 ```ts
 type Foo = number | { someProperty: number }

 let zoo: Animal = [new Rhino(), new Elephant(), new Snake()];

 function(status: string | boolean): boolean {
 //do stuff to list
 return !status
 }

 interface ClientModel {
 id: string
 name: string
 type?: string
 }
 let clientData: ClientModel = {
 id: '101010101',
 name: 'Foo',
 type: 'Bar'
 }
 ``` 
 >**Why?** For readability, changeability, extensibility and maintainability.

## Class
* Use PascalCase for name and camelCase for members.
* Use [access modifiers](https://www.typescriptlang.org/docs/handbook/classes.html#public-private-and-protected-modifiers): public (default value), protected, private.
* Use `public` for members that are used outside the class: templates, other classes.
* Use `protected` for members that are used by the class and it's children.
* Use `private` for members that are used only by the class itself.
* Use `readonly` for members that are constants.
* Use `static` for members that can be accessed with an instance of that class.
* Order members by type(property, method) and access modifiers. 
 ```ts
 class Animal {
  static abreviation = 'Aml'
  readonly order = 'vertebrate'
  public name?: string
  protected food: string[] = ['water']
  protected breathesWhat: 'air' | 'water'
  private real: boolean = true

  public lives () {
    this.breathe()
    this.eat()
  } 
  protected breathe () {
    return `breathe ${this.breathesWhat} `
  }
  private eat () {
    const foodString = this.food.join(,)
    return `eat: ${foodString}`
  }
 }
 class Lion extends Animal {
   name: 'lion'
   protected food = ['water', 'meet']
 }
 const abreviation = Animal.abreviation
 ```
>**Why?** For readability, changeability, extensibility and maintainability.

## Interface
* Use PascalCase for name and camelCase for members.
* Optional properties with `?:`.
* Nullable properties with `!:`.
* Use readonly for constant properties.
* Use string index signature for extra properties `[propName: string]: any;`.
* Use to define the signature of methods with attributes and return types `eat: (food: string) => string`.
* Use `implements`, `class Lion implements Animal`, to enforce a class meets a particular structure. 

## Enum
* Use PascalCase for name.
* Use string enums in place of hardcoded strings or numbers. 

***Avoid***
 ```ts
 if (type === 'vertebrates'){
 // do something
 }

 if (code === 3){// what is 3??
 // do something
 }
 ```
 **Do**
 ```ts
 enum AnimalTypes = {
 'invertebrates'='invertebrates',
 'vertebrates'='vertebrates'
 }
 if (type === AnimalTypes.vertebrates){
 // do something
 }

 enum StatusCodes = {
 'Success'= 1,
 'Error',
 'Pending'
 }
 if (code === StatusCode.Pending){
 // do something
 }
 ``` 
 >**Why?** For readability, changeability, extensibility and maintainability.


## Arrow functions
* Use them to better control the meaning of `this`.
* Use them to quickly return a value. Make sure you wrap an object in `()`. 
 ```ts
 var foo = () => ({
  bar: 123
 });
 ```
* *Don't* use them if you want `this` to be calling the context or you need `arguments`. To read more go [here](https://www.typescriptlang.org/docs/handbook/functions.html#this-and-arrow-functions).
  ```ts
  // with libs like jQuery allways use function
  $.each([ 52, 97 ], function( index, value ) {
    alert( index + ": " + value );
  });

  function doSomething () {
    let args = arguments
  }
  ```
* Related to [This](#this).
 >**Why?** Becase they are faster to write and read.

## Template strings
* Use them in place of concatenated strings.
* Use them for multiline strings. 

***Avoid***
 ```ts
 let fullName = firstname + ' ' + lastname
 let template = '<div class="foo"><h4>The Foo</h3><p>Foo bar bar foo</p></div>'
 ```
 **Do**
 ```ts
 let fullName = `${firstname} ${lastname}`
 let template = `<div class="foo">
  <h4>The Foo</h3>
  <p>Foo bar bar foo</p>
  </div>`
 ```
 >**Why?** Easyer to read and refactor.

## Async & Await
* Use them to better control asynchronous behavior.
* Use them with `for..of`.
  ```ts
  async function f() {
    for await (const x of g()) {
      console.log(x);
    }
  }
  ```
* Read more about it [here](https://github.com/basarat/typescript-book/blob/master/docs/async-await.md).

## Destructuring
* Use for Object destructuring.
* Use for Array destructuring 

***Avoid***
 ```ts
 function getFullName(user) {
 const firstName = user.firstName;
 const lastName = user.lastName;

 return `${firstName} ${lastName}`;
 }

 function getFirstTwo(list) {
 const first = list[0]
 const second = list[1]
 return {first, second}
 }

 function getPadding(input) {
 ...
 return [top, right, bottom, left];
 }
 const [top, __, bottom] = getPadding(data)
 ```
 **Do**
 ```ts
 function getFullName(user) {
 const { firstName, lastName } = user;
 return `${firstName} ${lastName}`;
 }

 function getFirstTwo(list) {
 const [first, second] = list
 return {first, second}
 }

 function getPadding(data) {
 ...
 return {top, right, bottom, left};
 }
 const {top, bottom} = getPadding(data)
 ```
 >**Why?** Cleaner code, easy to read and refactor.

## Spread operator
* Use to assign args to a function.
 ```ts
 function log(a, b, c) {}
 const params = [ a, b, c]
 log(...params)
 ```
* Use to merge arrays or objects.
 ```ts
 let list1 = [1,2,3]
 let list2 = [4,5,6]
 let list3 = [...list1, ...list2]

 let user = {id: '001', name: 'Foo Bar', initials: 'FB'}
 let account= {id: '110', email: 'foo@bar.co'}
 let userAccount = {...acount, ...user} //{id: '001', name: 'Foo Bar', initials: 'FB', email: 'foo@bar.co'}
 let accountUser = {...user, ...account} //{id: '110', name: 'Foo Bar', initials: 'FB', email: 'foo@bar.co'}
 ```
* Use when destructuring with rest.
 ```ts
 const { z, ...point2D } = {x: 1, y: 2, z: 3}
 console.log(point2D) // {x: 1, y: 2}

 let [x, , ...remaining] = [1, 2, 3, 4]
 console.log(x, remaining) // 1, [3,4]
 ```
 >**Why?** Cleaner and more to the point code.



## Inspiration for this Guideline
* [TypeScript Language Handbook](https://www.typescriptlang.org/docs/handbook/basic-types.html)
* [Microsoft Typescript Handbook](https://github.com/microsoft/TypeScript-Handbook)
* [Basarat TypeScript Book](https://github.com/basarat/typescript-book/blob/master/docs/styleguide/styleguide.md)

[**⇪**TOP](#typescript-styleguide-and-coding-conventions)