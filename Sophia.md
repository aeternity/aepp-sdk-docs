# Sophia Introduction and tutorial

## Intro
Sophia is a new programming language which has been created for writing smart contracts which run on the æternity virtual machine and the ethereum virtual machine. It is in the same family as languages such as [reason](https://reasonml.github.io/), which makes it a functional language (on which more later).

### What is a smart contract?
A smart contract is a piece of code that lives on the blockchain. It holds data in its state and can perform mutations through its functions. State data and contract code is stored on the blockchain. Publication of a contract can not be reveresd. Once a contract is published the state can only be changed according to the contract code. Contracts are similar to classes in object oriented languages and support local state and inheritance.

### What can I do with a smart contract?
You can write applications that run on the blockchain. These applications can store data, manage and transact funds, create oracles, register names, and pretty much any other computaional tasks like ‘normal’ applications. By using oracles, smart contracts can get data from the outside world, and so they can be used just like normal contracts, to formalise agreements between 2 or more parties.

### How is Sophia different from Solidity?
Sophia is a functional language, based on ReasonML, and Solidity is an imperative language, based on Javascript. Although you can do the same things in both languages there are important differences:
- Sophia's functional basis should, all other things being equal, make it easier to write correct, well-structure code.
- æternity's features, such as oracles, names and state channels are supported natively in Sophia, which not only makes them more natural to use, but will translate to a lower gas price, hence price of execution.

## Hello World
As always, let's start by writing a Hello World contract, and compiling it. 

### hello_world.aes
```
contract MyContract =
  entrypoint hello_world () = "Hello World"

```
### the anatomy of the hello world contract
- the contract starts with the keyword `contract`, followed by the name of the contract, in this case `MyContract`. 
- contracts are similar to classes in OO programming, in the sense that they can be inherited from, and contain local state
- the indentation of the next line indicates that it starts a new block
- the `entrypoint` keyword before the `hello_world` indicates that it can be called from outside the contract
- the `function` keyword starts the function definition, and the empty parantheses `()` that it takes no parameters
- the return value of the function is always the literal `"Hello World"`

### Compiling and deploying
To compile the contract, go to the contract editor at https://contracts.aepps.com and replace the code in the editor window with the example code. Clicking 'Compile' will cause a new UI component, headed with 'Byte Code' to appear. This shows the compiled result. At this stage nothing has been posted to the blockchain--to do this click 'Deploy' at the bottom of the screen. 

The deploy stage requires a Keyblock to be mined--this is explained in the BitcoinNG section of https://dev.aepps.com. At this stage what's important to know is that you may have to wait up to 3 minutes until you can call your contract. The contracts editor deals with this for you, and will block until the Keyblock containing your transaction has been mined.

## Basic language features
### Comments
Single-line comments start with `//` and block comments start with `/*` and end with `*/`. Comments can be nested.

### Blocks
Sophia uses blocks demarcated by indentation, in the python style. A block with more than one element must start on a new line, and be indented further than the block which encloses it. Blocks with only a single element can be written on the same line as the previous statement.

Each element of the block must share the same indentation, and no part may be less indented than the indentation of the block. 

```
contract Layout =
  function foo() = 0  // no layout
  function bar() =    // layout block starts on next line
    let x = foo()     // indented more than 2 spaces
    x
     + 1              // the '+' is indented more than the 'x'
```

### Types and literals

| Type    | Description                     | Example
| ------- | ------------------------------- | -------:
| int     | A 256 bit 2-complement integer  | ```-1```
| address | A 256 bit number given as a hex | ```ff00```
| bool    | A Boolean                       | ```true```
| string  | An array of bytes               | ```"Foo"```
| list    | A homogeneous immutable singly linked list. | ```[1, 2, 3]```
| tuple   | An ordered heterogeneous array   | ```(42, "Foo", true)```
| record  | An immutable key value store with fixed key names and typed values | ``` type balance = { owner: address, value: int } ```
| map     | An immutable key value store with dynamic mapping of keys of one type to values of one type | ```type accounts = map(string, address)```
| state   | A record of blockstate key, value pairs  |
| transactions | An append only list of blockchain transactions |
| events   | An append only list of blockchain events (or log entries) |

### Assignment (let binding), and types 

#### Let bidings
A let binding assigns a value to a named variable. These can be seen and referenced by code following them. They have this form:

```
let greeting = "Hello"
let score = 10
let newScore = 10 + score
let condition = false
```
Bindings are immutable--when you have assigned a value to a variable, you may not assign a new value to that variable. However you may create a new let binding, which will replace the previous one:

```
let message = "Hello" // message has value "Hello"
let message = "Bye" // message has value "Bye"
message = "Hola" // Error
```

#### Type annotations and inference
You may have noticed in the previous examples that we haven't given types for the variables. Sophia will infer the value where this makes sense. However sometimes you may want to tell the compiler what the type is, which you do using this syntax

```
let score: int = 10
```
you can give a type annotation anywhere you introduce a literal or a variable
```
let myInt = (5: int) + (10: int)
let add = (x: int, y: int) : int => x + y  // this is a function definition 
```

You will only normally declare types with more complicated code.

Types can accept parameters, which are indicated by a leading `'`. Parameterised types are useful when you want to avoid duplication, like this
##### before
```
type intCoordinates = (int, int, int);

let buddy: intCoordinates = (10, 20, 20);
```
##### after
```
type coordinates('a) = ('a, 'a, 'a)
```
now you can instantiate the `coordinates` type by giving its type argument
```
let buddy: coordinates(int) = (10,20,30)
```

### Boolean
A boolean has the type bool and can be either true or false. Common operations:

`&&`: logical and
`||`: logical or
`!`: logical not.
`=<`, `>=`, `<`, `>`, '!='
`==`: equal, compares data structures deeply: (1, 2) == (1, 2) is true.

#### Bitwise operators
- `band`: Bitwise AND
- `bor` : Bitwise OR
- `bxor`: Bitwise XOR
- `bsr` : Shift Right
- `bsl` : Shift Left

### List
A list is an ordered sequence of elements of the same type. Lists are fast at adding items (prepending), and splitting into two lists. They are not so fast at finding arbitrary items.

**Syntax**
##### Building
```ocaml
let emplyList = []
let varName = [e1, e2..., en]
// where e1, e2 ... ,en are expressions and has same type t
let xs = [1,2,3,4]
```
```ocaml
e1::e2
```
- ``::`` is called `cons`
- Here e1, e2 are expressions, e1 has value of type- `t`, e2 has type `t list`(list of type t)
- This expression `e1::e2`, adds value of `e1` to the start of list `e2`
- Example:
    ```ocaml
    let a = 2::[3,4,5,6]
    //a = [2,3,4,5,6]
    ```
    
Lists, along with recursion and pattern-matching are used extensively in functional languages.

##### Accessing
Explained in 'pattern matching' section.

### Tuple
Tuples are collections of disparate types. They are introduced in brackets, like this
```
let thirteens = (13, "thirteen", "dreizehn")

```
Tuples are
- immutable
- ordered
- fix-sized at creation time
- heterogeneous (can contain different types of values)

##### Building tuples

```ocaml
let ageAndName = (24, "Lil' Language")
let my3dCoordinates = (20.0, 30.5, 100.0)
```

Tuples' types can be used in type annotations as well. Tuple types visually resemble tuples values.

```ocaml
let ageAndName: (int, string) = (24, "Lil' Language")
/* a tuple type alias */
type coord3d = (float, float, float)
let my3dCoordinates: coord3d = (20.0, 30.5, 100.0)
```

##### Accessing tuples
Pattern matching in tuples (explained later in detail)
```javascript
let my3dCoordinates = (20.0, 30.5, 100.0)
let (x, y, z) = my3dCoordinates /* now you've retrieved x, y, z */
let (_, y, _) = my3dCoordinates /* now you've retrieved y */
// y = 30.5
```

`_` is used in place of values which we do not want to retrieve/use.

### Record
[Source](https://reasonml.github.io/docs/en/record.html)
Records are like 'C' structs, with named members.

#### Usage
##### Building Record
Type (mandatory):
```ocaml
type person = {
  age: int,
  name: string
}

```


Value (this will be inferred to be of type person):
```ocaml
let me = {
  age= 5,
  name= "Big Person"
}
```

##### Accessing Record
The familiar dot notation:
```ocaml
let name = me.name
```

Record Needs an Explicit Definition.

If you only write 
```ocaml
let baby = {age= 5, name= "Baby Person"}
```
without an explicit declaration somewhere above, the type system will give you an error.



### Map
Maps are key: value store mapping key of one type to value of one type.
```ocaml
type accounts = map(string, address)
```
A value can be set using- 
```ocaml
accounts['some_string'] = some_address
```
A value can be looked up in a map using its key:
```
accounts['some_string'] //will return some_address
```

### State

A contract's state is enclosed within its `state` type. Nothing outside of this state will be persisted between contract invocations. 


- Each contract defines a type state encapsulating its mutable state.
```ocaml
type state = { contributions : map(address, int),
                 total         : int,
                 beneficiary   : address,
                 deadline      : int,
                 goal          : int }
```
- The initial state of a contract is computed by the contract's init function. The init function is pure and returns the initial state as its return value. At contract creation time, the init function is executed and its result is stored as the contract state.

```ocaml
entrypoint init(beneficiary, deadline, goal) : state =
    { contributions = Map.empty,
      beneficiary   = beneficiary,
      deadline      = deadline,
      total         = 0,
      goal          = goal }
```
- The value of the state is accessible from inside the contract through an implicitly bound variable state.
- State updates are performed by calling a function `put : state => unit`. 
- Only a function with `stateful` modifier can change state.
```ocaml
public stateful function contribute(amount) =
    put(state{ contributions[call.caller] = amount,
               total = state.total + call.amount })


```

An example showing use of `state, init` and `put`
```ocaml
// a counter contract, where a value is stored in state, and 
//it can be increased by calling function `tick()`
contract Counter =
    type state = { value : int }

    entrypoint init(val)       = { value = val }
    entrypoint get()           = state.value
    stateful entrypoint tick() = put(state{ value = state.value + 1 })
```
### Types not in Sophia
- Arrays
- References
- Objects


### Control Structures
#### If-Elif-Else
```ocaml
if(exp1) exp2 else exp3
```
Example: 
```ocaml
let y = if(5>4) true else false
```
can also be written as:
```ocaml
if(exp1)
    exp2
else
    exp3
```
Example: 
```ocaml
let y = 
    if(5>4) 
        true 
    else 
        false
```
Using `elif`
```ocaml
let x=4
let y = 
    if(x>4) 
        1
    elif(x==4)
        2
    else 
        3
```
#### Switch
```ocaml
switch (expr0) 
        pattern1 => expr1
        pattern2 => expr2
        _    => expr3
```
This is how it works:
- `expr0` is evaluated once
- its value pattern matched(refer section pattern matching) to each pattern.
- `_` is a similar to `default` in other languages, and will be matched in every case
- Value of exprression belonging to pattern which matches is the value of whole block.
 
Equality is a type of pattern match, for other pattern matches, refer to the section 'pattern matching'

**Example**:
```ocaml
switch (x : int) 
        1 => "The int is One"
        2 => "The int is Two"
        _    => "The int is some other than One or Two"
```

### Functions

[Source](https://reasonml.github.io/docs/en/function.html)
Function can be be of type: `entrypoint`, `internal` or `private`
- entrypoint:  These can be used from outside the contract.
- internal: These can be used by contracts inheriting the given contract.
- private: These can only be used locally in the contract

Functions by default cannot change the state of the contract. For a function to change the state, it need to have a modifier `stateful` .
Example:
```ocaml
public function add(x:int, y:int) =
    x + y  //This is returned
```

```ocaml
private function addSquare(x:int, y:int) =
    let sqX = x*x
    let sqY = y*y
    sqX + sqY     //This is returned
```

##### Anonymous functions
```ocaml
(x) => x + 1
```

Annonymous function can have `let binding` and they would behave like a normal function.
```ocaml
let addOne = (x) => x + 1
```
However, these functions can only reside inside another function.
#### Recursive 
Recursion is used extensively in functional programming. A function can call itself with same or different arguements inside its body.
Example:
```ocaml
contract Factorial =    
    function fac(x : int) : int =
        if(x == 0)
            1
        else
            x * fac(x-1)
// A function to calculate factorial of a number
```

Using Switch case in above example:
```ocaml
contract Factorial =    
    function fac(x : int) : int =
        switch(x)
            0 => 1         //If x is 0
            _ => fac(x-1)  //Fallback statement
        
```


### Exceptions

Contracts can fail with an (uncatchable) exception using the function

```
abort(reason : string) : 'a
```
Example:
```ocaml
function balance_required(current_balance, required_balance) =
    if(current_balance < required_balance) 
        abort("balance not sufficient")
```
## Sophia and the Blockchain
### Contract primitives

The block-chain environment available to a contract is defined in three name spaces
`Contract`, `Call`, and `Chain`:

- `Contract.creator` is the address of the entity that signed the contract creation
  transaction.
- `Contract.address` is the address of the contract account.
- `Contract.balance` is the amount of coins currently in the contract account.
  Equivalent to `Chain.get_balance(Contract.address)`.
- `Call.origin` is the address of the account that signed the call transaction that led to this call.
- `Call.caller` is the address of the entity (possibly another contract)
  calling the contract.
- `Call.value` is the amount of coins transferred to the contract in the call.
- `Call.gas_price` is the gas price of the current call.
- `Call.gas_left()` is the amount of gas left for the current call.
- `Chain.get_balance(a : address)` returns the balance of account `a`.
- `Chain.block_hash(h)` returns the hash of the block at height `h`.
- `Chain.block_height` is the height of the current block (i.e. the block in which the current call will be included).
- `Chain.coinbase` is the address of the account getting the coinbase transaction of the current block.
- `Chain.timestamp` is the timestamp of the current block.
- `Chain.difficulty` is the difficulty of the current block.
- `Chain.gas_limit` is the gas limit of the current block.
---
An example contract showing use of Contract primitives. (Come back to this after reading 'transactions' section)

```ocaml
contract Environment =

  // -- Information about the this contract ---

  // Address
  function contract_address() : address = Contract.address
  function nested_address(who) : address =
    raw_call(who, "contract_address", 1000, 0, ())

  // Balance
  function contract_balance() : int = Contract.balance

  // -- Information about the current call ---

  // Origin
  function call_origin()   : address = Call.origin
  function nested_origin() : address =
    raw_call(Contract.address, "call_origin", 1000, 0, ())

  // Caller
  function call_caller() : address = Call.caller
  function nested_caller() : address =
    raw_call(Contract.address, "call_caller", 1000, 0, ())

  // Value
  function call_value() : int = Call.value
  function nested_value(value : int) : int =
    raw_call(Contract.address, "call_value", 1000, value, ())

  // Gas price
  function call_gas_price() : int = Call.gas_price

  // -- Information about the chain ---

  // Account balances
  function get_balance(acct : address) : int = Chain.balance(acct)

  // Block hash
  function block_hash(height : int) : int = Chain.block_hash(height)

  // Coinbase
  function coinbase() : address = Chain.coinbase

  // Block timestamp
  function timestamp() : int = Chain.timestamp

  // Block height
  function block_height() : int = Chain.block_height

  // Difficulty
  function difficulty() : int = Chain.difficulty

  // Gas limit
  function gas_limit() : int = Chain.gas_limit

```

### Events

*Note: events are not currently implemented*

An append only list of blockchain events (or log entries).
Sophia contracts log structured messages to an event log in the resulting blockchain transaction. To use events a contract must declare a type event, and events are then logged using the event function:

`event(e : event) : ()`

declaration:
```
type event = typeOfEvent
```

firing an event:
```javascript
event(expr1)
//expr1 should have type 'typeOfEvent'
```

Example:
```ocaml
contract addition =
    type event = string
    function addOne(x) = 
        event("One added")
        x+1
    function addTwo(x) = 
        event("Two added")
        x+2
```


### Transactions

Sophia can generate blockchain transactions.

### Contracts as objects, calling remotely and in
Sophia's equivalent of modules is the static contract. Contracts take the place of classes in object-oriented languages, and support local state and will support inheritance (when this feature is implemented).

A contract's public API is the functions and types which are annotated with the `public` keyword. These can be used from outside the contract. All other functions and types are part of the internal API and can be used by contracts inheriting from this contract, except those annotated with `private`, which can only be used locally.

#### Calling a function in another contract

The public functions of deployed contracts can be called when you know the address of the contract. The type of the address is a contract. For instance given this abstract contract
```ocaml
// An abstract contract
contract VotingType =
  public stateful function vote : string => ()
```
we can call it in the following manner
```
  function voteTwice(v : VotingType, fee : int, alt : string) =
    v.vote(value = fee, alt)
    v.vote(value = fee, alt)
```
To recover the underlying address of a contract instance there is a field address : address. For instance, to send tokens to the voting contract without calling it you can write
```ocaml
  function pay(v : VotingType, amount : int) =
    Chain.spend(v.address, amount)
```
#### Sending tokens to an address
Contracts can send/spend tokens using `raw_spend` call.
The function is called in following manner:
```
raw_spend(receiver_address: address, amount: int)

```
Here the arguements are:
- receiver_address: The address to whom tokens are to be sent
Type: `address`
- amount: The number of tokens to be sent.
Type: `int`

**In future there will be a native transaction type implemented and supposed to work like following**:
```
transaction(tx : transaction) : ()
```
The transaction type defines the transactions that can be created:

```ocaml
type spend_tx = {recipient : address, amount : int}
type transaction = SpendTx(spend_tx)
                 | ...
```

## Functional Programming Concepts in Sophia

### Variants Types
[Source](http://reasonmlhub.com/exploring-reasonml/ch_variants.html)
[Source2](https://reasonml.github.io/docs/en/variant.html)
Variants let you define sets of symbols. When used like this, they are similar to enums in C-style languages. For example, the following type color defines symbols for six colors.

`type color = Red | Orange | Yellow | Green | Blue | Purple`

There are two elements in this type definition:

- The name of the type, color, which must start with a lowercase letter.
- The names of constructors (Red, Orange, …), which must start with uppercase letters. The | bar separates each constructor.

Variants can be processed via switch and pattern matching:

```ocaml
function invert(c: color) =
  switch(c)
      Red => Green
      Orange => Blue
      Yellow => Purple
      Green => Red
      Blue => Orange
      Purple => Yellow
  
```

This is invert() in action:
```ocaml
invert(Red)
//Green
invert(Yellow)
//Purple
```
#### Variants as data structures
 
A variant's constructors can hold extra data separated by comma.

```ocaml
type account =
  None
  | Instagram(string)
  | Facebook(string, int)

```

Here, Instagram holds a string, and Facebook holds a string and an int. Usage:
```ocaml
let myAccount = Facebook("Josh", 26)
let friendAccount = Instagram("Jenny")
```

Using switch, you can pattern-match (described in later section) a constructor's arguments:
```ocaml
let greeting =
  switch (myAccount)
      None => "Hi!"
      Facebook(name, age) => "Hi " ++ name ++ ", you're " ++ string_of_int(age) ++ "-year-old."
      Instagram(name) => "Hello " ++ name ++ "!"
```

##### `option` variant
It is a variant exposed by default
```
type option('a) = None | Some('a)
```
This is the convention used to simulate a "nullable" (aka undefined or null) value in other languages. Thanks to this convenience type definition, Sophia can default every value to be non-nullable. An int will always be an int

### Destructuring
[Source](https://reasonml.github.io/docs/en/destructuring.html)
"Destructuring" is a visually concise way of extracting fields from a data structure. You can use destructuring anywhere you'd normally use a variable.

Usage:
The following binds variables: ten = 10, twenty = 20

```ocaml
let someInts = (10, 20)
let (ten, twenty) = someInts
```
The following binds variables: name = "Guy", age = 30

```ocaml
type person = {name: string, age: int}
let somePerson = {name: "Guy", age: 30}
let {name, age} = somePerson
```

When you pull out fields, you can optionally rename the fields. The following binds these instead: n = "Guy", a = 30.

```ocaml
let {name: n, age: a} = somePerson
```
Destructuring also allows type annotations.

```ocaml
let (ten: int, twenty: int) = someInts
let {name: (n: string), age: (a: int)} = somePerson
```

Destructuring a function's labeled arguments is also possible.

```ocaml
type person = {
  name: string,
  age: int
}
```

```ocaml
let someFunction = (~person as {name}) => {
  /* you can use `name` here */
}

let otherFunction = (~person as {name} as thePerson) => {
  /* you can use both `name` and the whole record as `thePerson` here */
}
```

### Pattern-matching
[Source](http://reasonmlhub.com/exploring-reasonml/ch_pattern-matching.html)
[Source 2](https://reasonml.github.io/docs/en/pattern-matching.html)
Pattern matching is like destructuring, but comes with even more help from the type system.

Consider a variant:
```ocaml
type payload =
  | BadResult(int)
  | GoodResult(string)
  | NoResult
```

While using the switch expression on it, you can "destructure" it:

```ocaml
let data = GoodResult("Product shipped!")

let message =
  switch (data)
      GoodResult(theMessage) => "Success! " ++ theMessage
      BadResult(errorCode) => "Something's wrong. The error code is: " ++ string_of_int(errorCode)
```

This conditional aspect is what makes it pattern matching rather than plain destructuring. Most data structures with an "if this then that" aspect work with it:

```ocaml
let y = 
    switch (myList)
        [] => "Empty list"
        [hd::tl] => "list with the head value " ++ hd

```

You can even switch on string, int and others. You can even have many patterns going to the same result!

```ocaml
let reply =
  switch (message) 
      "Sophia's pretty cool" => "Yep"
      "good night" => "See ya!"
      "hello" | "hi" | "heya" | "hey" => "hello to you too!"
      _ => "Nice to meet you!"
  
```


Combined with other data structures, pattern matching can produce extremely concise, compiler-verified, performant code:

```ocaml
let message =
  switch (data) 
      GoodResult(theMessage) => "Success! " ++ theMessage
      BadResult(0 | 1 | 5) => "Something's wrong. It's a server side problem."
      BadResult(errorCode) => "Unknown error occurred. Code: " ++ string_of_int(errorCode)
      NoResult => "Things look fine"
  
```
Note: you can only pass literals (i.e. concrete values) as a pattern, not let-binding names or other things. The following doesn't work as expected:

```ocaml
let myMessage = "Hello"
let greet = 
    switch (greeting)
        myMessage => ("Hi to you")

```
Instead, it'd assume you're matching on any string, and binding that to the name myMessage in that switch case, which is not what you wanted. It would match for every string.


#### When clauses
When you really need to use arbitrary logic with an otherwise clean pattern match, you can slip in some when clauses, which are basically if sugar:

```ocaml
let message =
  switch (data) {
  | GoodResult(theMessage) => ...
  | BadResult(errorCode) when isServerError(errorCode) => ...
  | BadResult(errorCode) => ... /* otherwise */
  | NoResult => ...
  }
```

#### Nested Patterns
Nested | work as intended:

```ocaml
switch (student) {
| {name: "Jane" | "Joe"} => ...
| {name: "Bob", Job: Programmer({fullTime: Yes | Maybe})} => ...
}
```

#### Pattern matching and lists:

---
Following table shows different cases of pattern matching 
#### Value in pattern
If a value is passed as patern, it is matched for equality only. Let’s look at a few examples:


| Pattern           | Data                        | Matches 
| ----------------- | --------------------------- | --------
| 3                 | 3                           | yes     |
| 1                 | 3                           | no      |
| (1,true)   | (1, true)             | yes     |
| (1, false)  | (1, true)             | no      |


#### Variable names in patterns
If a variable is passed as patern, it pattern matches for any value, and that value is assigned to the variable.
| Pattern           | Data                        | Matches |Variable bindings
| ----------------- | --------------------------- | --------|----------------
|x	                |3                            |yes	    |x = 3
|(x, y)             |(1,true)                       |yes	  |x = 1, y = true
|(1, y)             |(1, true)                      |yes	  |y = true
|(2, y)             |(1, true)                       |no	    |

The special variable name _ does not create variable bindings and can be used multiple times:

| Pattern           | Data                        | Matches |Variable bindings
| ----------------- | --------------------------- | --------|----------------
|(x, _)             |(1, true)                       |yes	    |x = 1
|(1, _)             |(1, true)                       |yes	    |
|(_, _)             |(1, true)                       |yes	    |

#### Pattern matching, lists and recursion:
- `[]` matches with empty
- `hd::tl` matches with non empty list. 
    - Remember `::` is cons operator, and used to append `hd` to begining of list `tl`
    - when pattern is matched, `hd` is equal to first element and `tl` equals rest of the list.
    -   ```javascript
        //return first element of list if list is non empty
        function head(xs) =
            switch(xs)
                hd::tl => hd
                [] => 0
        //head([1,2,3,4]) = 1
        //head([]) = 0
        ```
    -   ```javascript
        //return tail of list if list is non empty
        function tail(xs) =
            switch(xs)
                hd::tl => tl
                [] => []
        //tail([1,2,3,4]) = [2,3,4]
        //tail([1]) = []
        //tail([]) = []
        ```
    - Note: tail of list containing only one element is `[]`
        

- These two patterns along with recursion are used whenever iterating over lists


Usage explained with an example:
```javascript
function sumList(xs) =
    switch(xs)
        [] => 0
        head::tail => head + sumList(tail)
        // adding head(first element) and sum of rest of list
        // When only one element remain, tail will be `[]` and 
        // function exits from recursion
```
---
Example contract showing various list iteration using above method
```javascript
contract MyContract =
    //gives sum of all elements in the list
    function sumList(xs) =
        switch(xs)
            [] => 0
            x::xs => x + sumList(xs)
    /*
        sumList([1,2,3,4]) 
        gives output 10
    */

    //apply a function f to all elements of a list
    function map(f, xs) = 
        switch(xs)
            [] => 0
            x::xs => f(x)::map(f,xs)
    
    //gives a list where every element of the input list is squared
    function squaresOfList(xs) =
        // function to square a number
        let square = (i) => (i*i)
        map(square, xs)
        
    /*
        squaresOfList([1,2,3,4]) 
        gives output [1,4,9,16]
    */
          
    function up_to_helper(n, xs) =
        switch(n)
            0 => xs
            _ => up_to(n-1,n::xs)
    
    //gives a list of elements upto n
    // up_to(5) gives [1,2,3,4,5]
    function up_to_helper(n) = 
        up_to(n, [])

    //get length of list
    function silly_length(xs) =
        switch(xs)
            [] => 0
            _ :: xs => length(xs) + 1

    
```
---
Implementation of a Stack data structure using lists, recursion and state:

```javascript
contract Stack =

  record state = { stack : list(string),
                 size  : int }

  entrypoint init(ss) = { stack = ss, size = length(ss) }

  private function length(xs) =
    switch(xs)
      [] => 0
      _ :: xs => length(xs) + 1

  stateful entrypoint pop() : string =
    switch(state.stack)
      s :: ss =>
        put(state{ stack = ss, size = state.size - 1 })
        s

  stateful entrypoint push(s) =
    put(state{ stack = s :: state.stack, size = state.size + 1 })
    state.size

  function all() = state.stack

  function size() = state.size
  
  

```
---
Example contract 
Implementation of a Dutch Auction
```javascript
//
// Dutch auction example
//
contract DutchAuction =

  record state = { start_amount : int,
                 start_height : int,
                 dec          : int,
                 beneficiary  : address,
                 sold         : bool }

  // Add to work around current lack of predefined functions
  //private function abort(err) = abort(err)
  
  private stateful function spend(to, amount) =
    let total = Contract.balance
    Chain.spend(to, amount)
    total - amount

  // TTL set by user on posting contract, typically (start - end ) div dec
  entrypoint init(beneficiary, start, decrease) : state =
    require(start > 0 && decrease > 0, "bad args")
    { start_amount = start,
      start_height = Chain.block_height,
      beneficiary  = beneficiary,
      dec          = decrease,
      sold         = false }

  // -- API

  // We are the buyer
  stateful entrypoint bid() =
    require( !(state.sold), "sold")
    let cost =
      state.start_amount - (Chain.block_height - state.start_height) * state.dec
    require( Contract.balance >= cost, "no money")

// //In future it'd be like this:
//    transaction(SpendTx({recipient = state.beneficiary,
//                         amount    = cost }))  // or self.balance ** burn money **
// // But for now, its like this:
    spend(state.beneficiary, cost)
    spend(Call.caller, Contract.balance)
    put(state{sold = true})

```

## Other resources

You can find a good set of example Sophia contracts in the Epoch source tree, in the [sophia example repository](https://github.com/aeternity/aepp-sophia-examples).

An online contract editor to use with testnet is available [here](https://contracts.aepps.com), also a local development environment can be create using the [ForgAE project](https://github.com/aeternity/aepp-forgae-js).

For any question, support or issues use the [forum](https://forum.aeternity.com).

## Licenses

Some parts were adopted from the [Reasonml documentation](https://reasonml.github.io/docs/) released under the MIT license.
Everything else is released under the ISC license.

### The ISC License

ISC License

Copyright (c) 2018-present, Aeternity, Establishment.

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

### The MIT License (for the parts adopted from Reasonml documentation)

MIT License

Copyright (c) 2015-present, Facebook, Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

