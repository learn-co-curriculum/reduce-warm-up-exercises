# Reducers Warm Up Exercise

## Array.prototype.reduce

We've used a lot of `.find`, `.forEach`, `.map`, and `.filter` so far.

We've heard of reduce, but haven't used it for anything.

Let's take a look at the reduce function. Like map, forEach, and filter, it takes a callback function that will be invoked with each of the items in an array.

The reduce callback function, though, gets called with different arguments than the others. Instead of just getting the item, it also receives the _return value of the most recent call to the callback function_

```
> [1,2,3].reduce(function (last, item) {      console.log('last', last, 'item', item)
     return item + 10
}, 0)

last 0 item 1
last 11 item 2
last 12 item 3
=> 13
```

This 'most recent value' is usually called the _memo_ or accumulator. The first time the callback is called, the accumulator is set to the _initial value_, passed in as an optional second argument to reduce.

Let's see an example of how reduce can be used!

Say we wanted to add up all the numbers in an array, using reduce.

```
> [7, 18, 2, 35, 91, 7, 30, 66].reduce(function(memo, num) {
     return memo + num
}, 0)
=> 256
```

At each step, we add the current element to our total. The total is passed in to the next call to the callback function. The final result is the sum of all the numbers.

We can see this process step-by-step by adding some logging:
```
> [7, 18, 2, 35, 91, 7, 30, 66].reduce(function(memo, num) {
     console.log('current total: ', memo, 'current element: ', num)
     return memo + num
}, 0)
current total:  0 current element:  7
current total:  7 current element:  18
current total:  25 current element:  2
current total:  27 current element:  35
current total:  62 current element:  91
current total:  153 current element:  7
current total:  160 current element:  30
current total:  190 current element:  66
=> 256
```

Let's practice using reduce to solve more problems.

## Join

We'll take an array of strings and return a single string, with all of the strings concatenated together.

```
["I", " like", " sphagetti", "."].reduce( /* our join reducer */ )
=> "I like sphagetti."
```

## Flatten

- Input: An array of arrays
- Output: an array of items - the contents of each of the nested arrays.

```
flatten([[1,2,3], [4,5,6]])
=> [1,2,3,4,5,6]
```

## Pluck

- Input: An array of objects like: [{ name: "Rob", age: 94 }, { name: 'Sam', age: 95 }]
- Output: An array of just the age values, like [94, 95]

## Histogram (Frequency Map)

- Input: An array of strings
- Output: An object with keys of the strings, values the number of times the word appeared in the array

## Map

Implement a function `map` that behaves like Array.prototype.map using reduce.

## Filter

Implement a function `filter` that behaves like Array.prototype.filter using reduce.

## Pluck + Flatten

Input: An array of objects like
```js
[
  {feeling: 'happy', animal: 'robin', colors: ['blue','green']},
  {feeling: 'tired', animal: 'panther', colors: ['green','black','orange','blue']},
  {feeling: 'sad', animal: 'goldfish', colors: ['green','red']}
];
```

Output: An array of all the colors,
```js
['blue', 'green', 'green', 'black', 'orange', 'blue', 'green', 'red']
```


## Calculator

This one is tricky! The array contains objects like:

```js
{type: "Add", value: 4}
{type: "Multiply", value: 3}
{type: "Divide", value: 2}
{type: "Subtract", value: 3}
```

Your reduce function should do the operation specified. So,

```js
[
  {type: "Add", value: 4},
  {type: "Multiply", value: 3},
  {type: "Divide", value: 2},
  {type: "Subtract", value: 3}
].reduce(/* calculator */, 6)
=> 12
```

Because (((6 + 4) * 3) / 2 ) - 3) is 12

## When to use `reduce`

We can see that the other functions (`filter`, `map`) can be built with reduce. So, should we just use reduce for everything? No! It's more confusing than the others!

High-level heuristic for when to use `reduce` vs the other array methods:

- `map`: I have a list of _n_ things and want a list of _n_ things, transformed.
- `filter`: I have a list of _n_ things and want a subset of those things
- `reduce`: I have a list of _n_ things and want back _one thing_ - a single aggregate of all the things in the list.

The reason that reduce can be used to build `filter` and `map` is that the _aggregate_ that we get from `reduce` could be a list, e.g. a subset or a transform of the original list.

## Functions that use reduce vs. Reducer functions

Functions that use reduce:

```js
function sum(array) {
    return array.reduce(function (total, num) {
        return total + num;
    }, 0)
}
```

Pretty cool! We can pass an array in, and this function will return the sum.

```js
sum([1,2,3,4])
=>  10
```

'Reducer' functions are the _callbacks we pass to reduce_.

```js
function adder(total, num) {
   return total + num
}
```

We can define them this way, and then use them in our reducing functions:

```js
function sum(array, num) {
    return array.reduce(adder, 0)
}
```

For each of the problems above, make sure you've defined the function that uses reduce (`sum` in our example) as well as the _reducer_ (`adder` in our example.)

When we introduce redux, we'll see that we can use reducer functions in more situations than just `reduce`!
