### 1.1 Below is a sequence of statements. What is the result printed by the interpreter in responseto each statement? Assume that the sequence is to be evaluated in the order in which it is presented.

```js
10;
10

5 + 3 + 4;
12

9 - 1;
8

6 / 2;
3

2 * 4 + (4 - 6);
6

const a = 3;
3
const b = a + 1;
4

a + b + a * b;
19

a === b;
false

b > a && b < a * b ? b : a;
4

a === 4
false
? 6
: b === 4
true
? 6 + 7 + a
: 25;
16

2 + (b > a ? b : a);
6

(a > b
false
? a
: a < b
true
? b
: -1)
4
*
(a + 1);
16
```

### 1.2 Translate the following expression into JavaScript

```js
5 + 4 + (2 - (3 - (6 + 4 / 5))) / (3 * ((6 - 2) * (2 - 7)));
```

### 1.3 Declare a function that takes three numbers as arguments and returns the sum of the squares of the two larger number

```js
function sort_arr(arr) {
  return arr.sort((a, b) => a - b);
}

function get_two_largest(arr) {
  return [arr[1], arr[2]];
}

function sum_square(arr) {
  return arr.map((e) => Math.pow(e, 2)).reduce((p, a) => p + a, 0);
}

sum_square(get_two_largest(sort_arr([1, 2, 3])));
```

### 1.4 Observe that our model of evaluation allows for applications whose function expressions are compound expressions. Use this observation to describe the behavior of _a_plus_abs_

```js
function a_plus_abs_b(a, b) {
  if (b >= 0) {
    return a + b;
  }
  return a - b;
}
a_plus_abs_b(1, 2);
```

### 1.5 Ben Bitdiddle has invented a test to determine whether the interpreter he is faced with is using applicative-order evaluation or normal-order evaluation. He declares the following two functions:

```js
function p() {
  return p();
}
function test(x, y) {
  return x === 0 ? 0 : y;
}
test(0, p());
```

What behavior will Ben observe with an interpreter that uses applicative-order evaluation?

```
Se o interpretador estiver usando application-order os argumentos serão avaliados antes da funcão ser aplicada, causando em um loop infinito.
```

What behavior will he observe with an interpreter that uses normal-order evaluation? Explain your answer. (Assume that the evaluation rule for conditional expressions is the same whether the interpreter is using normal or applicative order: The predicate expression is evaluated first, and the result determines whether to evaluate the consequent or the alternative expression.)

```
Nesse caso os argumentos apenas serão avaliado quando necessario, sendo assim o argumento y nunca será chamado.
```
