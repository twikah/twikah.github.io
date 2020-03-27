---
postHero: /images/rubystone.jpg
title: 'Ruby: inject'
categories: work
tags: [web-development, ruby, ruby-methods]
---

Last week I did a code challenge about an IP address converter.

My method had 19 lines, but it worked. Out of curiosity, I looked into other
solutions to see how I could simplify or improve my response.

That was when I found a resopnse... With just 1 line of code 😱😱🤯

<img class="pull-left" src="https://media.giphy.com/media/Um3ljJl8jrnHy/giphy.gif"
alt="mindblown animation" style="width: 200px;">

This solution that I found used the `inject` method. I tried to understand
it but it was a bit confusing.

So I googled for inject examples. I
found [this](http://blog.jayfields.com/2008/03/ruby-inject.html) incredible
article about `Enumerable#inject` and now I want to write down what I
learned from it... You know, for future reference.

<br>

### Example 1: We have an array of numbers and we want the sum of those numbers

<br>

```
[1, 2, 3, 4].inject(0) { |result, element| result + element } # => 10
```

<br>


The inject method takes an *argument* and a *block*.

In the example above, inject is being called on the array [1, 2, 3, 4] and it
takes the integer *0* as the *argument*.

Then, our *block* has its own arguments inside it, *result and element*.

The block will be executed once for each element contained in the array [1,2,3,4].

The first time the block executes, the argument 0 will be yielded as the result
argument of the block. Then, the first element of the array - 1 - will
be yielded to the element argument of the block.

Our block will be executed 4 times, once for every element of our array
[1,2,3,4]. So, to recap, the first time the block executes, the result argument
will become 0 and the element argument will become 1.

The return value of the block will be yielded as the result argument the next
time the block is executed. So, in the first execution, the return value of the
block will be 0 + 1 = 1. Then, 1 will be yielded as the result argument in the
second time the block is executed.

The second time the block is executed, the result argument on the block becomes
1 and the element argument becomes 2 (the second element of the array).
Here, the result, 1, and the element, 2 will be added together, and the second
execution of the block returns 3 as result value.

The above line of thought will be repeated for third and fourth elements of our
example array, and the return value of this inject method will be 10.

<br>

We should know that the argument to inject is optional:

```
[1, 2, 3, 4].inject { |result, element| result + element } # => 10
```

<br>

The argument acts as a default value to be passed on the first time the code
executes. If we don't have an argument, the block yields the first element of
the array - 1 - to become the result argument of the block and the second
element of the array to become the element argument of the block.

In this case the block will only need to be executed 3 times, since the first
execution will yield both the first and the second element.

<br>

### Example 2: We have an array of arrays and we want to convert it into a hash

<br>

```
[[:first_name, 'harvey'], [:last_name, 'specter']].inject({}) do |result, element|
  result[element.first] = element.last.upcase
  result
end

# => {:first_name=>"Harvey", :last_name=>"Specter"}
```

<br>

On example 2, we have an empty hash passed as an argument to inject.

The block iterates through each element in the array, adding the key and value
one at a time to the result. Also, since the result of the block is the next
yielded result, we need to explicitly return the result on the following line.

<br>

### Example 3: We have an array and want to select integers that are even, as strings

<br>

```
[1, 2, 3, 4, 5, 6].select { |element| element % 2 == 0 }.collect do |element|
  element.to_s
end

# => ["2", "4", "6"]
```

<br>

The chained enumerables above can be replaced by the inject method below, making
the code more readable:

<br>

```
[1, 2, 3, 4, 5, 6].inject([]) do |result, element|
  result << element.to_s if element % 2 == 0
  result
end

# => ["2", "4", "6"]
```

<br>

#### All in all, inject allows us to easily convert an enumerable into an object and manipulate it on the fly, making our code more concise.

