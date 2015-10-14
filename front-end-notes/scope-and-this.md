# Scope and This

### Scope

In JavaScript, scope refers to the current context of your code. Scopes can be globally or locally defined. Understanding JavaScript scope is key to writing bulletproof code and being a better developer. You'll understand where variables/functions are accessible, be able to change the scope of your code's context and be able to write faster and more maintainable code, as well as debug much faster.

This article has a great explanation of scope: [Everything You Wanted To Know About Scope](http://toddmotto.com/everything-you-wanted-to-know-about-javascript-scope/)
### This

'This' is a keyword that refers to the current call site's scope. For example:

```
/*
  Example one: call site and call stack
 */
var fubar = "42";

function baz() {
    console.log( "baz" );
    bar();
}

function bar() {
    console.log( "bar" );
    foo();
}

function foo() {
    var fubar = "666";

    console.log( "foo" );
    console.log( this );
    console.log( this.fubar );
}

baz();

```

In this example, `baz()` is called in the global scope. So even though baz calls bar, which calls foo, the console log in foo `console.log(this)` will return the global scope.

```
/*
  Example two: context objects
 */
var a = 20;

function foo() {
    a = 50;
    console.log( this.a );
}

var obj = {
    a: 2,
    foo: foo
};

obj.foo();
```

In this example, foo is called on obj. So `console.log(this.a)` will return 2.

```
/*
  Example three: context objects
 */
function foo() {
    console.log( this.a );
}

var obj2 = {
    a: 42,
    foo: foo
};

var obj1 = {
    a: 2,
    obj2: obj2
};

obj1.obj2.foo();
```

In this example, foo is called on obj2, so `console.log( this.a )` will return 42.

```
/*
  Example four: losing original binding
 */
function foo() {
    console.log( this.a );
}

var obj = {
    a: 2,
    foo: foo
};

var bar = obj.foo;
var a = "global warming";

obj.foo();
bar();
```

In this example, `obj.foo()` will return 2 because foo is called on obj. `bar()` will return "global warming" because it is called in the global scope.

```
/*
  Example five: losing original binding with callbacks
 */
function foo() {
    console.log( this.a );
}

function doFoo(fn) {
    fn();
}

var obj = {
    a: 2,
    foo: foo
};

var a = "oops, global";

doFoo( obj.foo );
```

In this example, doFoo() is called in the Global Scope, so `console.log( this.a )` in foo will return 'oops, global'.
