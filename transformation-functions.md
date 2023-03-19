# Introduction

The `Transformation` namespace contains a set of functions that allow you to transform your variables in a convenient way.

## pipe

# Signature

```php
function pipe(mixed $value, Closure $closure): mixed
```

### Definition

This function takes a value and applies a transformation to it using a closure.
If the value is a closure, it will be invoked before applying the transformation.
The result of the transformation will be returned.

### Examples

```php
use function PhpRepos\ControlFlow\Transformation\pipe;

$value = 5;
$closure = fn ($x) => $x * 2;
$result = pipe($value, $closure);
assert_true($result === 10);

$callable = fn () => 5;
$closure = fn ($x) => $x * 2;
$result = pipe($callable, $closure);
assert_true($result === 10);
```
