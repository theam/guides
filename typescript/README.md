# The Agile Monkeys' TypeScript Guide 📖

**This guide can be overwhelming, JUST CHILL, we have a code review process. :wink:**

The intention of this guide is not to do everything like this
just because, it rather serves as a place where to come if
someone mentions a concept.

Code as you know, dont get stressed with whats here. Make sure
you skim over the guide, but dont force yourself to do stuff in
a way you dont know/understand yet. That's what the code
review process is for, **to help each other make their code better**.

<!-- TOC -->

- [1. Why a guide? 🤔](#1-why-a-guide-)
- [2. Getting Started 🚀](#2-getting-started-)
    - [2.1. Yarn](#21-yarn)
    - [2.2. TypeScript](#22-typescript)
    - [2.3. Visual Studio Code](#23-visual-studio-code)
    - [2.4. React DevTools](#24-react-devtools)
    - [2.5. Linter](#25-linter)
- [3. Required libraries 📚](#3-required-libraries-)
    - [3.1. React](#31-react)
    - [3.2. fp-ts](#32-fp-ts)
    - [3.3. newtype-ts](#33-newtype-ts)
    - [3.4. io-ts](#34-io-ts)
    - [3.5. monocle-ts](#35-monocle-ts)
    - [3.6. elm-ts](#36-elm-ts)
    - [3.7. typesafe-actions](#37-typesafe-actions)
    - [3.8. remote-data-ts](#38-remote-data-ts)
- [4. Code Style 👗](#4-code-style-)
    - [4.1. Use `const`](#41-use-const)
    - [4.2. Program using expressions, not statements](#42-program-using-expressions-not-statements)
    - [4.3. The ternary operator is your friend](#43-the-ternary-operator-is-your-friend)
    - [4.4. NEVER, EVER, return null/undefined](#44-never-ever-return-nullundefined)
- [5. Typing stuff ⌨️](#5-typing-stuff-️)
    - [5.1. Type inference](#51-type-inference)
    - [5.2. Avoid classes](#52-avoid-classes)
    - [5.3. Avoid primitives](#53-avoid-primitives)
    - [5.4. Defining records](#54-defining-records)
    - [5.5. Choice types](#55-choice-types)
    - [5.6. Signaling adversity](#56-signaling-adversity)
        - [5.6.1. Option](#561-option)
        - [5.6.2. Either](#562-either)
    - [5.7. Schema validators](#57-schema-validators)
    - [5.8. Types for React actions](#58-types-for-react-actions)
    - [5.9. Modeling remote data](#59-modeling-remote-data)
- [6. Thinking functionally ⚗️](#6-thinking-functionally-️)
    - [6.1. ~~Array~~ Data transformations](#61-array-data-transformations)
    - [6.2. Avoid promises](#62-avoid-promises)
    - [6.3. Using IO for side effects](#63-using-io-for-side-effects)
    - [6.4. Testing in a functional way](#64-testing-in-a-functional-way)
- [7. Architecting React Apps 🏗](#7-architecting-react-apps-)
    - [7.1. elm-ts vs redux](#71-elm-ts-vs-redux)
    - [7.2. The basic pattern](#72-the-basic-pattern)
    - [7.3. Handling app events](#73-handling-app-events)
    - [7.4. Nesting components](#74-nesting-components)

<!-- /TOC -->

# 1. Why a guide? 🤔

We think a lot all day long. How do we connect this service to this queue? How do I store this JSON in
my React app state? Why does this crash with `undefined is not a function`?

We should think in solutions that bring us value, and not in stuff like code organization, or how to deserialize something.

This guide is about this. Stop thinking in superfluous things and just **do**.

# 2. Getting Started 🚀

## 2.1. Yarn

For package management, we use [Yarn](https://yarnpkg.com/) instead of NPM. It provides a nicer interface, more security, reliability, and it is retrocompatile with NPM.

[Install it in your system](https://yarnpkg.com/en/docs/install)

If you use brew in macOS, just run:

    brew install yarn

## 2.2. TypeScript

We use [TypeScript](https://www.typescriptlang.org/) because it is JavaScript, with types.
When you drive a car, you use a seatbelt. Not because you are going to do crazy stuff, but just in case.
Same happens with types, they prevenent **A LOT** of runtime errors.

To install it:

    yarn global add typescript

And in your project:

    yarn add --dev typescript

## 2.3. Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com/) is a code editor written in TypeScript, that has **great** support for TypeScript, and it is very simple to use.

We recommend some plugins for you to install:

_Install them from VSCode by doing `CMD + SHIFT + P` in macOS or `CTRL+P` in other systems and then typing `ext install`, or open the following links and install them from the VS marketplace website:_

* [Auto Import - ES6, TS, JSX, TSX by **Sergey Korenuk**](https://marketplace.visualstudio.com/items?itemName=NuclleaR.vscode-extension-auto-import) (must be this one)
* [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
* [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
* [Quokka.js](https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode)
* [TSLint](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-typescript-tslint-plugin)
* [Vim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim) (if you like Vim keybindings)
* [vscode-icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)
* [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) - Make sure you go to settings and enable the "Format on save" option.

## 2.4. React DevTools

Install the [chrome extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi).

## 2.5. Linter

All of our projects should be configured with [TSLint](https://palantir.github.io/tslint/) and with the `useStrict: true` flag
of TypeScript. This will save us from a lot of
burden and debugging.

# 3. Required libraries 📚

## 3.1. React

[React](https://reactjs.org/) is a rendering library that allows you to define your own HTML components and
their properties. It is the current industry standard, and there are a lot of reusable components
on the internet.

To add it to your project:

    yarn add react
    yarn add --dev @types/react

## 3.2. fp-ts

[`fp-ts`](https://github.com/gcanti/fp-ts
) is **the** functional programming library for TypeScript. It adds lots of important stuff like `Option` and `Either` to help us model
our logic more concisely. It also comes with a
referentially transparent alternative to the
JavaScript `Promise<T>`: **`Task<T>`**.

There is an important ecosystem based on this library,
so it is a must.

    yarn add fp-ts

We want to have this as it provides many useful abstractions
that do not come with TypeScript by default, for example:

* [Optionals](#561-option)
* [Either](#562-either)
* [Function utilities](FIXME)
* [Task](#62-avoid-promises)
* [IO](#63-using-io-for-side-effects)
* [Date](FIXME)

## 3.3. newtype-ts

[`newtype-ts`](https://github.com/gcanti/newtype-ts
) allows us to make compile time
wrappers for primitive types, we shouldn't use a
`string` where we are using an email. Neither should
we use an `int` for a server port.

This library allows you to model much better these
"small" types. Check the [section about avoiding primitives](#53-avoid-primitives).

    yarn add newtype-ts

## 3.4. io-ts

[`io-ts`](https://github.com/gcanti/io-ts
) is a library that allows writing object schemas and validators. If things go wrong
validating the input, it provides some great error
pretty printers.

    yarn add io-ts io-ts-types

There is more info on [the schema validation section](#57-schema-validators).

## 3.5. monocle-ts

[`monocle-ts`](https://github.com/gcanti/monocle-ts
) allows you to access and update deeply nested fields of an object in an immutable way.

    yarn add monocle-ts

## 3.6. elm-ts

[`elm-ts`](https://github.com/gcanti/elm-ts
) leverages [React](#31-react), [rxjs](https://rxjs-dev.firebaseapp.com/), and [fp-ts](#32-fp-ts) to simplify the
architecture of React applications.

    yarn add elm-ts

## 3.7. typesafe-actions

While in [React](#31-react)/Redux one would define an event as a
string, this is a very error-prone technique, and we
could end up debugging a whole hour just because a typo.

[`typesafe-actions`](https://github.com/piotrwitek/typesafe-actions
) give us a way of defining
actions that are checked by the TypeScript compiler.

    yarn add typesafe-actions

It really improves a lot, look at the example of [the React actions section](#58-types-for-react-actions).

## 3.8. remote-data-ts

Sometimes, we have a null field in an object because
we haven't retrieved yet with an HTTP request. This is bad, as we have to check for nulls now.

Then, we make the field optional, and we make it be
`None` if we haven't retrieved it yet and/or we got a error. This doesn't explain what went wrong.

[`remote-data-ts`](https://github.com/devex-web-frontend/remote-data-ts
) gives us a data type that
represents:

* Initial (no request made yet)
* Pending
* Failure
* Success

A small tutorial is available on the [modeling remote data](#59-modeling-remote-data) section.

    yarn add remote-data-ts

# 4. Code Style 👗

## 4.1. Use `const`

Wherever you are declaring a variable or a function,
do it with `const`. This avoids unexpected mutation
and side-effects.

**Constant values:**

Instead of doing:

```typescript
let x: number = 42
```

Do this:

```typescript
const x: number = 42
```

**Function example:**

[Did you know you can modify a function in runtime](https://stackoverflow.com/a/3472440)?

Horrible, isn't it? Let's prevent that!

Instead of doing:

```typescript
function add(a: number, b: number): number {
    return a + b
}
```

Do this:

```typescript
const add = (a: number, b: number): number =>
    a + b
```

If you use `const` for functions you get two main
benefits: 

* Implicit returns 
* The compiler limits you to one expression per function.

## 4.2. Program using expressions, not statements

The difference between an expression and a statement
can be seen mostly like this:

**Expression:**

```typescript
sqrt(10 - 1) //  => 3
```

**Statement:**
```typescript
console.log("Hi") // => undefined (or void)
```

The main difference is that expressions, after
applying all the functions that they are composed
of, they evaluate to a **value**, which can be
then passed to another function.

Statements, on the other hand, can be executed
line by line and are part of an imperative program.
They generally involve side effects, and are stuff
like variable assignation, calls to services, etc...

If you program using expressions you get many things
for free:

* **Referential transparency:**
    You can be sure that if you run a function, it
    will behave always the same way, no matter how
    the environment is.
* **Predictability:**
    You can specify the inputs and outputs of your
    functions, and by checking them, you can see
    what does the function do.
* **Autodocumentation:**
    Given predictability, the types act as a strong
    documentation tool, helping new crew members
    with the onboarding process.

**The only exception** to this rule is when you
refactor chained function calls to many `const`:

This code:

```typescript
const myComplexOperation = (n: number): string =>
    "Look: " + (sum(range(1, n))).toString
```

Would become:

```typescript
const myComplexOperation = (n: number): string => {
    const numbers = range(1, n)
    const sumString = sum(numbers).toString
    const message = "Look: " + sumString
    return message
}
```
## 4.3. The ternary operator is your friend

When working with conditions, it is very natural
and addicting to write code like this:

```typescript
const validateEmail = (email: string): Option<string> => {
    if (email.contains("@")) {
        return some(email)
    } else {
        return none
    }
}
```

Everything is great, no side effects, purity,
all cool. But then two months pass by, a coworker
comes, and adds this:

```diff
 const validateEmail = (email: string): Option<string> => {
     if (email.contains("@")) {
+        const newEmail = validationService.validate(email)
+        return some(newEmail)
     } else {
         return none
     }
 }
```

The function is not pure anymore, and if our validation service is not online, our application will probably crash. By using an `if`, we have
opened the door to adding more statements!

In languages like Haskell and Scala, the `if` clause returns an expression, but we are not in Haskell and Scala.

Luckily, TypeScript has a great equivalent,
**the ternary operator**. So the function from
before can be written like:

```typescript
const validateEmail = (email: string): Option<string> =>
    email.contains("@")
    ? some(email)
    : none
```

It is much more concise, and now we cannot do what
we did before, without changing the type. Which
means, that we cannot crash our app this way.

## 4.4. NEVER, EVER, return null/undefined

If for some reason, there is a way that your function
might have an input for which an output doesn't
exist, don't return `null` or `undefined`.

Use an appropriate type like `Option`:

Instead of:

```typescript
const divide = (a: number, b: number): number =>
    b == 0
    ? undefined
    : a/b
```

Do this:

```typescript
import { some, none, Option } from 'fp-ts/lib/Option';

const divide = (a: number, b: number): Option<number> =>
    b == 0
    ? none
    : some(a/b)
```

If you find that you are losing error information and
would need to throw an exception, don't do this:

```typescript
const divide = (a: number, b: number): number =>
    b == 0
    ? throw Exception("Division by zero")
    : a/b
```

Do this instead:

```typescript
import { left, right, Either } from 'fp-ts/lib/Either';

const divide = (a: number, b: number): Either<string, number> =>
    b == 0
    ? left("Division by zero")
    : right(a/b)
```

`Either<Left, Right>` returns the `Right` type
when everything went **right**, and `Left` when
something failed.

You can change `string` for your own error type. (And you should).

Now when calling this function you might see that it
doesn't return the type you expected anymore. To
extract it, you can do so by using `getOrElse`:

```typescript
divide(6, 2).getOrElse(-1) // => 3
divide(3, 0).getOrElse(-1) // => -1
```

In following sections we will see how to operate
in a much more expressive way.


# 5. Typing stuff ⌨️

The idea behind types is to have the compiler catch
as much runtime errors as possible in compile time.

Languages like Haskell can achieve 100% no runtime
errors thanks to this, and TypeScript can get very
close to that.

Don't be afraid of having to type everything, like Java, as TypeScript has type inference.

## 5.1. Type inference

Type inference is the ability of the compiler to
figure out which type is a value has.

So if we write `const x = 42` it will probably know
that `x` is a `number`. But this has one limitation:

TypeScript gives us **local** type inference, but not
global. What does this mean?

For example, given this code:

```typescript
// Dont do this! Use expressions instead
const addOne = (x: Number): Number => {
    const r = x + 1  // Infers that r: number
    return r
}

const myNumber = 41  // Error, myNumber has 'any' type
const result = addOne(myNumber)  // Error, result has 'any' type
```

TypeScript will know that `r` has type `number`, but will now complain about `myNumber` and `result`.
It has no way of inferring which types are they, as
they are in the **global scope**.

Generally, we do not want global constants, but if
for some reason you need one, make sure you type its type.

## 5.2. Avoid classes

TypeScript has classes, but they come with two main
concerns:

* They hide mutation
* Inheritance comes into play

Due to this, we generally avoid them. Unless, of
course, we require them for something like React,
where you have to make a class that inherits from
the `React.Component` class to work properly.

## 5.3. Avoid primitives

Primitives are great, but even the SOLID principles
state that primitive obsession is bad. They don't follow the single responsibility principle, and
like an `int` can be a port, it can also be minutes.

Not only this, primitive types can make a mess in a
system if you call a function that takes many
arguments of the same type, but are designated for
different things.

Do you remember [the NASA Mars incident](https://en.wikipedia.org/wiki/Mars_Climate_Orbiter#Cause_of_failure)?
They probably had some code like this:

```typescript
const land(distance: number): ... => ...
```

This code doesn't tell us anything, we can screw it
up very badly (and lose $125 millions like NASA) if
we use the wrong distance unit.

Instead, we can help our team, and make clear our
intention with some newtypes:

```typescript
import { iso, Newtype } from 'newtype-ts'

// Compile time wrapper over 'number'
type Meters = Newtype<'Meters', number>
// Companion object to wrap/unwrap
const Meters = iso<Meters>()

type Feet = Newtype<'Feet', number>
const Feet = iso<Feet>()

// We use a clear unit here
const land(distance: Meters): ... => ...
```

Now to use it:

```typescript
const distanceM: Meters = Meters.wrap(120)
const distanceF: Feet = Feet.wrap(120)

land(distanceM)  // => Everything ok!
land(distanceF)  // => Compile error: Expected Meters, got Feet
```

The best part about newtypes is that they don't
introduce performance issues, as their runtime
representation is just the type they are wrapping,
in this case `number`.

## 5.4. Defining records

As we said before, we have to avoid classes.

How do we define structured data then? **Interfaces**:

```typescript
interface Person {
    name: string,
    age: int,
    address: Adress
}
```

## 5.5. Choice types

Sometimes, it is very useful to define a **choice type** to provide better
semantics to our code. Instead of doing this:

```ts
const tellStatus(isTurnedOn: boolean): string =>
    isTurnedOn
    ? "It is on 💡"
    : "It is off 😫"

tellStatus(true)  // What does 'true' mean here?
```

We will provide better knowledge to our teammates with this:

```ts
type BulbStatus = "on" | "off"
const BulbStatus = {
    on: "on",
    off: "off"
}

const tellStatus(status: BulbStatus): string =>
    (status === "on")
    ? "It is on 💡"
    : "It is off 😫"

tellStatus(BulbStatus.on)  // Much better semantics
```

If we wanted to extend this with intensity, we can do so like this:

```ts
type BulbStatus = { type: "on", intensity: int }
                | { type: "off" }

const BulbStatus = {
    on: (intensity) => { type: "on", intensity },
    off: { type: "off" }
}

const tellStatus(status: BulbStatus): string =>
    (status.type === "on")
    ? ("It is on at intensity " + status.intensity.toString())
    : "It is off 😫"

tellStatus(BulbStatus.on(35))  // We provide the intensity value
```

Generally our types will remain the same throughout the project, so this
makes them reusable.

Of course, use this as you need it. If you are creating just a helper function,
don't bother doing this.

## 5.6. Signaling adversity

Many times, we need to signal that something went wrong. `fp-ts` provides
many ways of doing this.

### 5.6.1. Option

Optionals are great, they remove the necessity of using `null` and,
even better, they provide a nice API to work with nullable values.

The representation of an `Option<T>` looks more or less like this:

![optional uml](https://blog.xebia.fr/wp-content/uploads/2012/03/Options.png)

* The `Some` class represents an existing value. Meaning that we can safely
operate using its value
* The `None` class represents a non-existent value. Meaning that we have no
way of working with it.

Luckily, we have a nice API that abstracts us from this.

To provide an example, lets suppose we have some functions in our project:

```ts
// Takes a text and parses all the lottery numbers it contains
readLotteryNumbers(s: string): Option<array<number>>

// Returns the first element of a string
head(lst: array<number>): Option<number>

// Converts a number like 11 into "eleven"
numberToLetters(n: number): string
```

Now, you happen to need to implement the `announceWinner` function, 
which you know that says the first number in the text.

If these functions didn't return `Option`, we probably should be doing
stuff like:

```ts
const txt = readFile("lotto.txt")
const nums = readLotteryNumbers(txt)
if (nums !== null) {  // It can fail to parse
    const winner = head(nums)
    if (winner !== null) {  // The array might be empty
        return (numberToLetters(winner) + " has won the lottery!"
    } else {
        return null
    }
} else {
    return null
}
```

As our code returns `Option`s, we can now proceed to use its API:

```ts
const txt = readFile("lotto.txt")
const nums = readLotteryNumbers(txt)
if (nums.isSome()) {
    const winner = head(nums.getValue())  // NOTE: getValue doesnt exist
    if (winner.isSome()) {
        return (numberToLetters(winner) + " has won the lottery!"
    } else {
        return none
    }
} else {
    return none
}
```

But this is not much better than `null`, our code is still very ugly with these
`None` checks.

Luckily, `Option` provides us with a `map` method, that acts like the `map`
from `array`. You give it a function to transform whats inside, and it will
apply it to whats inside. But what if it is `None`? It wont do nothing.

With this, now we can refactor the inner `if`:

```ts
const txt = readFile("lotto.txt")
const nums = readLotteryNumbers(txt)
if (nums.isSome()) {
    const winner = head(nums.getValue())  // NOTE: getValue doesnt exist
    return winner.map(x => numberToLetters(x) + " has won the lottery!")
} else {
    return none
}
```

Great! Thats one level of indentation less. You'd wish to use `map` with
`head` but it wont work, as it would create a `Option<Option<number>>` and
we dont want that.

You're lucky, there is another method, `chain` that applies a function that returns an Option and then "flattens" them into
one, allowing us to refactor the last `if`:

```ts
const txt = readFile("lotto.txt")
return readLotteryNumbers(txt)
        .chain(head)
        .map(winner => numberToLetters + " has won the lottery!")
```

This code is exactly the same that we did before with the `if`s, but now,
we have abstracted ourselves from the error handling.

And speaking about errors, if something fails, we have no idea what it was.
What if we need error messages?

Here is when the next type from `fp-ts` comes in handy:

### 5.6.2. Either

`Either<E, T>` is the same thing as `Option<T>` except that it takes an additional
type for signaling error messages:

![Either uml](https://blog.xebia.fr/wp-content/uploads/2012/04/Either.png)

We have now two classes:

* `Right` when everything went Right
* `Left` when something went wrong

Imagine our functions from before now return `Either`s instead of
`Option`:

```ts
readLotteryNumbers(s: string): Either<string, array<number>>
head(lst: array<number>): Either<string, number>
numberToLetters(n: number): string
```

The resulting code remains the same, as `Either` provides exactly the same API
as `Option`:

```ts
const txt = readFile("lotto.txt")
return readLotteryNumbers(txt)
        .chain(head)
        .map(winner => numberToLetters + " has won the lottery!")
```

Now, suppose something fails during the process. `map` and `chain` dont touch
the error message, and only operate if it is a `Right` value.

This means that the error propagates, and we can handle it afterwards:

```ts
const foo = left("Im an error")
const bar = right(3)

foo.map(x => x + 1)   // => left("Im an error")
bar.map(x => x + 1)   // => right(4)
```

## 5.7. Schema validators

A lot of times, we get data from a third party, but we have to validate that
it is structured according to a schema. For this, the `io-ts` library
provides us a way of defining schemas:

```ts
import * as t from 'io-ts' 

const ProductSchema = t.type({ 
    caption: t.string, 
    description: t.string, 
    id: t.string,
    images: t.array(t.string) 
})
```

Now, to use this schema as a type in our code, we do the following:

```ts
type Product = t.TypeOf<typeof ProductSchema> 
```

We can now write a function that validates a JSON string and returns a
product:

```ts
const decodeProduct(s: string): Either<Errors, Product> =>
    ProductSchema.decode(JSON.parse(s))
```

As you can see, it returns an `Either`, meaning that it wont blow up if the
validation fails, and rather, we can use a `PathReporter` to pretty print the
validation errors, or another thing:

```ts
const p = decodeProduct("LOL")

// We check if the value contains errors
if (p.isLeft()) {
    // '.report' returns an array of strings
    PathReporter.report(p).foreach(msg =>
        console.log(msg)
    )
// If it doesnt contain errors, it is a Right<Product>
} else {
    console.log("Decoded successfully")
}
```

Note that `Either` allows you to do nice stuff like `map`, `getOrElse`, etc...

## 5.8. Types for React actions

When using React, specially when using Redux, we dispatch actions to trigger
changes on the component state, or side effects.

The issue is, most people model their actions as a `string`. What if we have
an action called `"initCatalog"`?

When calling it, we can forget it:

* Was it `initializeCatalog`?
* Was it `catalogInit`?
* Or maybe `catalogInitialize`?

In the best case, you will go to the action handler and see what is going on.

In the worst, you will spend 15 minutes figuring what is going on.

Luckily, `typesafe-actions` provides us a way of defining actions in a type
safe way, with an extra bonus, you can add additional info to the actions.

Instead of relying on strings:

```tsx
<button onClick={() => dispatch("say-hello")}>
    Click me!
</button>
```

Where we can also mess up the handler:

```ts
function update(msg: Msg, model: Model) {
  switch (msg) {
    case "say_hello":
        alert("Hello")

    default:
        return
  }
}
```
 _(Did you see the typo? An underscore instead of a hyphen!)_

We make some boilerplate to make the compiler yell at us if we do something
wrong:

```ts
// Message 
type Msg = ActionType<typeof Msg>

// Companion object to create new instances of the messages
const Msg = {
    sayHello: createAction('myComponentName/sayHello', resolve =>
        () => resolve()
    ),
}
```

Now we can use it in the component:

```tsx
<button onClick={() => dispatch(Msg.sayHello())}>
    Click me!
</button>
```

And to check what action it is:

```ts
function update(msg: Msg, model: Model) {
  switch (msg.type) {
    case getType(Msg.sayHello):
        alert("Hello")

    default:
        return
  }
}
```

Now we reduced the possibilities of the errors a lot. It is not possible to
create an action that doesnt exist :wink:.

## 5.9. Modeling remote data

Mostly always, we will request data from external services. Until the data
is available, we have no idea on how to model this state of the app.

Because of this, most people end up modelling pending data with `null`.

This is horrible, as it represents an erroneous state (a state that leads to a crash) in our app. Thankfully, the `remote-data-ts` library helps us with this.

Imagine we have the state of our component modelled like this:

```ts
interface Model {
    username: string,
    profileInfo: ProfileInfo
}
```

The `profileInfo` field will be retrieved from the backend, so the type doesnt
reflect the reality. Another possibility would be to use `Option`:

```ts
interface Model {
    username: string,
    profileInfo: Option<ProfileInfo>
}
```

Better, but how do we differentiate between the data that hasnt been requested
yet, and the failed request? Here is where the `RemoteData` comes handy:

```ts
interface Model {
    username: string,
    profileInfo: RemoteData<Error, ProfileInfo>
}

type Error = String
```

Now, the code is much better documented, and even better, we have **four**
functions to set the data:

* `initial`
* `pending`
* `failure`
* `success`

```ts
// before doing the request
const init = {
    username: "Bob",
    profileInfo: initial
}

// while the request is being done, we set the field to
pending

// after doing the request
// if the request was succesful, we use
success(data we got from response)

// if it failed
failure("Oh no!")
```

We can pattern match on the different possibilities using the `foldL` method:

```tsx
profileInfo.foldL(
    // initial
    () => <p>No data has been requested</p>,

    // pending
    () => <p>Request in progress</p>,

    // failure
    err => <p style="color: red">ERROR! {err}</p>,

    // success
    data => <ProfileComponent data={data} />
)
```

# 6. Thinking functionally ⚗️

## 6.1. ~~Array~~ Data transformations

Mostly, we can do most of our work using the basic functions that come with
TS, but they are somewhat limited.

`fp-ts` comes with a wide variety of functions to work with arrays and
ways of composing the functions:

* https://gcanti.github.io/fp-ts/modules/Array.ts.html
* https://gcanti.github.io/fp-ts/modules/function.ts.html

## 6.2. Avoid promises

Avoid using promises, as they arent referentially transparent, and run instantly, rather than lazily, unlike Task<T> from fp-ts.
To create one:

```ts
const myTask = new Task<T>(
  () => myPromise
)
```

## 6.3. Using IO for side effects

The great part of using the `IO` type is that it makes your code rely pure.

For instance, the `Console` module that comes with `fp-ts` has all the
counterparts of the regular `console` module, but all of them return `IO`.

Why is this so great? It allows the compiler to help you to detect bugs
induced by side effects, making it much more explicit. Also, it is lazy:

```ts
const foo: IO<void> = new IO(() => {
    // stuff with side effects
    // like write data to DB
})

const x = foo // not run
const y = foo // not run
```

Even better, we can map over it and chain more actions!

```ts
IO(() => "test")
    .map(s => s.length)
    .chain(Console.log)
```

## 6.4. Testing in a functional way

While regular unit testing is great, it is not as reliable as we'd like.
With a unit test, you are testing just one case, but we want to test **all**
the cases.

This is where **property based testing** comes to help.

Imagine you are testing that a function reverses a string. You could do it
like:

```ts
describe('reverse', () => { 
    it('reverses', () => { 
        expect(reverse(reverse('hello')))).toBe('hello') 
    }) 
}
```

But what if we havent checked for other things? Does it support empty strings?
What about UTF8 characters? Does it work for all lengths of string?

These questions not only are hard to answer, but also, hard to come up with.

We can ask [`fast-check`](https://github.com/dubzzz/fast-check) to do the test
for all strings:

```ts
describe('reverse', () => { 
    it('reverses', () => { 
        fc.assert(fc.property(fc.string(), text =>
            reverse(reverse(text)) === text
        );
    }) 
}
```

We are `assert`ing a `property` for all `string`s called `text`.
FastCheck will make lots of random cases, trying to break our
function.

For more info, you can check [the official docs](https://github.com/dubzzz/fast-check/blob/master/documentation/HandsOnPropertyBased.md).

# 7. Architecting React Apps 🏗
## 7.1. elm-ts vs redux

Both libraries provide you a nice way of structuring state. Redux might look
like the best choice, given that it is the most popular one, but it comes
with a few drawbacks:

* The developer is in charge of configuring how the state is stored
* Many plugins modify the store to add weird hooks in runtime
* Although the state update (reducer) **should** be pure, no guarantee of that
* Side effects are handled by secondary libraries, like Saga or Redux 
Observable. They make code much more complex, as you have to configure them 
too
* Possibility of storing manually state in the store, leading to an error

`elm-ts` is an abstraction over Redux, handling all the state storage
internally, and providing a much simpler way of passing state around.

The architecture becomes much simpler also. Consider the following Redux app,
it makes a GET request and shows how many times it has been clicked:

```tsx
// root component
ReactDOM.render( 
  <Provider store={configureStore()}> 
  <App /> 
  </Provider>, 
  document.getElementById('root') as HTMLElement 
);

// times it has been clicked
type State = number

// actions
type Actions = "clicked" | "noop"

// boilerplate required by redux
const mapStateToProps = (state: State) => { 
  return {state} 
} 

// props, required by redux also
type Props = { state: State } & Actions

// our component
class ConnectedApp extends React.Component<Props> { 

  public componentDidMount() { 
    this.props.initialize() 
  } 

  public render() { 
    return ( 
        <div>
        Clicked {this.props.state} times
        <button onClick={"clicked"}> Click me </button>
        </div>
    ) 
  } 
} 

// connection of react and redux
const App = connect( 
  mapStateToProps, 
  mainActions 
)(ConnectedApp)

// redux state updater
const mainReducer: Reducer<State, MainAction> = (state: State = initialState, action: MainAction) => { 
    switch (action) { 
        case getType("clicked"): 
             return state + 1 

        default: 
            return state 
    } 
}

// redux-observable function to run side effects
const mainEpic: Epic<MainAction, MainAction, State> = (action$: Observable<MainAction>) => 
    action$.pipe( 
        filter(action => action === "clicked"), 

        concatMap((): Observable<string> =>  
            // we have to convert our request to an Observable,
            // as it works like that
            from(request.get("http://my-endpoint.com"))), 

        map((data: string): MainAction =>
            "noop"
    ) 
)

// redux-observable boilerplate
const epicMiddleware: EpicMiddleware<MainAction, MainAction, State> =  
    createEpicMiddleware() 

// connecting redux and redux-observable
const configureStore = () => { 
    const store: Store<State> = 
        createStore( 
            mainReducer,  
            applyMiddleware(epicMiddleware) 
        ) 

    epicMiddleware.run(mainEpic) 
    return store 
}
```

Now take a look at the `elm-ts` counterpart:

```tsx
// root initialization
const main = React.program(Counter.init, Counter.update, Counter.view)
React.run(main, dom => render(dom, document.getElementById('root')!))


// times it has been clicked
type Model = number

// initial state
const init: [Model, Cmd<Msg>] =
    [0, cmd.none]


// Message type
type Msg = "clicked" | "noop"


// state updater
const update = (msg: Msg, model: Model): [Model, Cmd<Msg>] => {
  switch (msg.type) {
    case "clicked":
      return [model + 1, doRequest()]

    default:
      return [model, cmd.none]
  }
}


// function that performs the request,
// note how the implementation is hidden from us
const doRequest = (): Cmd<Msg> => {
    const req = http.get("http://my-endpoint.com")
    return http.send(req, res => "noop")
}


// render
const view = (model: Model): Html<Msg> =>
  dispatch => (
    <div>
      Count: {model}
      <button onClick={() => dispatch("clicked")}>Click me</button>
    </div>
  )
```

Note how it is much shorter, and more concise. Even better, if we nest
components, we dont have to do the config passing downstream, and just
call the appropriate `update` or `view` function.

Another stone in our way in code organization is the way that Redux
organizes their code. Suppose we had two components: `Slider` and
`Dropper`. With Redux their code would be organized like:

```text
src
- epics
    - Slider.ts
    - Dropper.ts
- reducers
    - Slider.ts
    - Dropper.ts
- components
    - Slider.tsx
    - Dropper.tsx
- @types
    - Slider.ts
    - Dropper.ts
```

This doesnt make any sense. We do not even know what imports who. If we use
on the other hand `elm-ts`, the code would be like this:

```text
src
- Slider
    - State.ts
    - Types.ts
    - View.tsx
    - Http.ts
- Dropper
    - State.ts
    - Types.ts
    - View.tsx
    - Http.ts
```

If we happened to nest our components, we'd just move the folder inside the
other one! **Still, if you dont need to split your component, dont do it.**


## 7.2. The basic pattern

The logic of your app will basically break into three parts:

* **Model** - The state of your app
* **Update** - A way to update your state
* **View** - A way of viewing your state as HTML

It is so robust that you can always start with the following skeleton:

```tsx
import { cmd } from 'elm-ts'
import { Html } from 'elm-ts/lib/React';
import * as React from 'react'
import { ActionType, createAction, getType } from 'typesafe-actions';



// MODEL
type Model = ...



// UPDATE
type Msg = ActionType<typeof Msg>
const Msg = {
    myAction: createAction('myComponent/MY_ACTION', resolve =>
        (...) => resolve(...)
    )
}

const update = (msg: Msg, model: Model): [Model, cmd.Cmd<Msg>] => {
  switch (msg.type) {
    case getType(Msg.myAction):
      return [...]

    default:
      return [model, cmd.none]
  }
}



// VIEW
const view = (model: Model): Html<Msg> =>
  dispatch => (
    <div>
        <button onClick={() => dispatch(Msg.myAction(...))}>
            Click me
        </button>
    </div>
  )
```

## 7.3. Handling app events

As you could see in the previous example, we assigned an action to an
`onClick` event. This pattern is always the same for all the events:

* Create the `Msg` type and its companion object
* Match on the `.type` field of it in our `update` function
* If needed, access the data it carries in the `.payload` field
* Assign it to an event in the `view` function

For instance, if we were to create a counter, it would look like this:

```tsx
type Model = number

type Msg = ActionType<typeof Msg>

const Msg = {
    incrementBy: createAction('main/INCREMENT_BY', resolve =>
        (n: number) => resolve(n)
    ),
    decrementBy: createAction('main/DECREMENT_BY', resolve =>
        (n: number) => resolve(n)
    ),
}

function update(msg: Msg, model: Model): [Model, cmd.Cmd<Msg>] {
  switch (msg.type) {
    case getType(Msg.incrementBy):
      return [model + msg.payload, cmd.none]

    case getType(Msg.decrementBy):
      return [model - msg.payload, cmd.none]

    default:
      return [model, cmd.none]
  }
}

function view(model: Model): Html<Msg> {
  return dispatch => (
    <div>
      Count: {model}
      <button onClick={() => dispatch(Msg.incrementBy(1))}>+</button>
      <button onClick={() => dispatch(Msg.decrementBy(1))}>-</button>
      <button onClick={() => dispatch(Msg.incrementBy(5))}>Add five<button>
      <button onClick={() => dispatch(Msg.decrementBy(5))}>Subtract five<button>
    </div>
  )
}
```

## 7.4. Nesting components

When nesting components, one should define in the parent the
fields and actions of the children, so the parent can pass them
downstream.

```tsx
type Model = {
  // Field to store state of a child
  counterModel: number,

  // Another one
  catalogModel: Catalog.Model
}

type Msg = ActionType<typeof Msg>
const Msg = {
   // Actions of one child
   counterAction: createAction('myComponent/COUNTER_ACTION', resolve =>
        (counterAction: Counter.Msg) => resolve(counterAction)
    ),

   // Actions of the other
   catalogAction: createAction('myComponent/CATALOG_ACTION', resolve =>
        (catalogAction: Catalog.Msg) => resolve(catalogAction)
    )
}

const update = (msg: Msg, model: Model): [Model, cmd.Cmd<Msg>] => {
  switch (msg.type) {
    case getType(Msg.counterAction):
      // We pass the action downstream
      const newState = Counter.update(msg.payload, model.counterModel)

      // We return the field updated, and the cmd mapped to the upper
      // action
      return [
          {...model, counterModel = newState[0]}, 
          cmd.map(newState[1], Msg.counterAction)
      ]

    case getType(Msg.catalogAction):
      // We pass the action downstream
      const newState = Catalog.update(msg.payload, model.catalogModel)
      // We return the field updated, and the cmd mapped to the upper
      // action
      return [
          {...model, catalogModel = newState[0]}, 
          cmd.map(newState[1], Msg.catalogAction)
      ]

    default:
      return [model, cmd.none]
  }
}

const view = (model: Model): Html<Msg> =>
  dispatch => (
    // We map the view to the upper actions also
    <div>
        { html.map(Counter.view(model.counterModel), Msg.counterAction) }
        { html.map(Catalog.view(model.catalogModel), Msg.catalogAction) }
    </div>
  )
```
