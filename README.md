# Injector

[![npm version](https://img.shields.io/npm/v/@alexey.kornilov/injector.svg?style=flat-square)](https://www.npmjs.com/package/@alexey.kornilov/injector)

This is dependency injector for JavaScript with support for ES6/ES2015. It can 
be applied in both node and browser environments.

## Installation

Execute this command in your environment. 

```
npm install @alexey.kornilov/injector --save
```
or

```
yarn add @alexey.kornilov/injector
```

## Usage

### Constructor registration

One is able to register constructor for a particular class and create
instances of it:

```js
import Injector from "@alexey.kornilov/injector";

class Foo {
    constructor() {
        console.log("Creating instance of Foo.");
    }
    
    get dependencies() {
        return [];
    }
}

const injector = new Injector();
injector.register("foo", Foo);

// Resolve class by its registered name
const foo1 = injector.resolve("foo");

// Resolve class by its constructor reference
const foo2 = injector.resolve(Foo);
```

Expected output will be:

```
[Tue Mar 28 2017 08:39:53 GMT+0300 (MSK)] [Injector] Registering 'foo' component.
Creating instance of Foo.
Creating instance of Foo.
```

### Object registration

One is able to register pure object.

```js
import Injector from "@alexey.kornilov/injector";

const foo = {
    name: "Foo object " + Math.round(Math.random() * 10)
};

const injector = new Injector();
injector.register("foo", foo);

// Resolve registered object
const foo1 = injector.resolve("foo");
console.log(foo1);

// Resolve registered object
const foo2 = injector.resolve("foo");
console.log(foo2);

// We are expecting same object
console.log(foo1 === foo2 ? 
    "Same object resolved." : 
    "WARNING: unexpected resolved object.")
```

Expected output will be:

```
[Tue Mar 28 2017 08:46:31 GMT+0300 (MSK)] [Injector] Registering 'foo' component.
{ name: 'Foo object 5' }
{ name: 'Foo object 5' }
Same object resolved.

```

Also usage examples can be found in `./examples` folder.