# Introducing JSX

```
const element = <h1>Hello, world!</h1>;
```

This is JSX - it is recommended to be used with React to describe what the UI should look like.

## Why JSX

React embraces the fact that rendering logic is inherently coupled with other UI logic - how events are handled, how
state changes over time, how the data is prepared for display.

- React separates concerns with components.

## Embedding Expressions in JSX

```
const name = 'Andrew Weisbeck'
const element = <h1>Hello, {name}</h1>
```

We can put any JavaScript expression in for name.

Here we embed the result of calling a JS function formatName(user) into an <h1> element

```
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = {
  <h1>
    Hello, {formatName(user)}!
  </h1>
);
```

## JSX is an Expression

JSX expressions become regular JS function calls and evaluate JS objects after compilation. You can use JSX inside
of `if` and `for` loops, assign it to variables, accept as arguments, and return from functions.

```
function getGreeting(user) {
  if (user) {
    return <h1>hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

## Specifying Attributes with JSX

You can use qutotes to specify string literals as attributes

```
const element = <a href="https://www.reactjs.org"> link </a>
```

You may also use curly braces to embed a JS expression in an attribute

```
const element = <img src={user.avatarUrl}></img>;
```

*Don't put quotes around curly braces when embedding a JS expression in an attribute. Use quotes for string values or
curly braces for expressions, but not both in same attribute.

## Specifying Children with JSX

if tag is empty, close it immediately with />

```
const element = <img src={user.avatar.Url} />;
```

JSX may contain children:

```
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to ee you here.</h2>
  </div>
);
```

## JSX Prevents Injection Attacks

it is safe to embed user input in JSX

```
const title = response.potentiallyMaliciousInput;
// this is safe
const element = <h1>{title}</h1>;
```

React DOM escapes any values embedded in JSX before rendering them, by default. It ensures you can never inject anything
that's not explicitly written in your application. Prevents XSS cross site scripting attacks.

## JSX Represents Objects

Babel compiles JSX down to React.createElement() calls
THese two samples are identical:

```
const element = {
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

React.createElement() runs a few checks, essentially creates this object:

```
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

These objects are known as react elements!