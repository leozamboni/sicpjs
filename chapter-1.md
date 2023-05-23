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

### 1.6 Alyssa P. Hacker doesn’t like the syntax of conditional expressions, involving the characters ? and :. “Why can’t I just declare an ordinary conditional function whose application works just like conditional expressions?” she asks.21 Alyssa’s friend Eva Lu Ator claims this can indeed be done, and she declares a conditional function as follows:

```js
function conditional(predicate, then_clause, else_clause) {
  return predicate ? then_clause : else_clause;
}
```

Eva demonstrates the program for Alyssa:

```js
conditional(2 === 3, 0, 5);
5;
conditional(1 === 1, 0, 5);
0;
```

Delighted, Alyssa uses conditional to rewrite the square-root program:

```js
function conditional(predicate, then_clause, else_clause) {
  return predicate ? then_clause : else_clause;
}

function average(x, y) {
  return (x + y) / 2;
}

function improve(guess, x) {
  return average(guess, x / guess);
}

function square(x) {
  return x * x;
}

function is_good_enough(guess, x) {
  return Math.abs(square(guess) - x) < 0.001;
}

function sqrt_iter(guess, x) {
  if (is_good_enough(guess, x)) {
    return guess;
  }
  return sqrt_iter(improve(guess, x), x);
}

function sqrt(x) {
  return sqrt_iter(1, x);
}
```

```js
function sqrt_iter(guess, x) {
  return conditional(
    is_good_enough(guess, x),
    guess,
    sqrt_iter(improve(guess, x), x)
  );
}
```

What happens when Alyssa attempts to use this to compute square roots? Explain.

Se a raiz quadrada for a esperada retorna a resposta, se não, improve e faz o loop de novo.
Node (application-order): fica em um loop infinito ja que o interpretador avalia primeiro os argumentos e depois aplica a funcao.

### 1.7 The is_good_enough test used in computing square roots will not be very effective for finding the square roots of very small numbers. Also, in real computers, arithmetic operations are almost always performed with limited precision. This makes our test inadequate for very large numbers. Explain these statements, with examples showing how the test fails for small and large numbers. An alternative strategy for implementing is_good_enough is to watch how guess changes from one iteration to the next and to stop when the change is a very small fraction of the guess. Design a square-root function that uses this kind of end test. Does this work better for small and large numbers?

Não será preciso para números pequenos ja que o número de tolerância fixo é de 0.0001.

```js
function is_good_enough(previous, guess, x) {
  return Math.abs(guess - previous) / x < 0.001;
}

function sqrt_iter(previous, guess, x) {
  if (is_good_enough(previous, guess, x)) {
    return guess;
  }
  return sqrt_iter(guess, improve(guess, x), x);
}

function sqrt(x) {
  return sqrt_iter(0, 1, x);
}
```

Solucão acima melhor para números menores mas não muito para número maiores.
