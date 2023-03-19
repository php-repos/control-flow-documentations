# Introduction

The `Conditional` namespace provides functions for conditional statements in phpkg.
It offers `when`, `unless`, and `when_exists` functions that allow you to perform conditional checks 
and execute code blocks based on the result of these checks.

## when

# Signature

```php
function when(bool $condition, Closure $then, Closure $otherwise = null): mixed
```

### Definition

The `when` function executes the `$then` closure if the `$condition` is `true`.
If the `$condition` is `false`, the `$otherwise` closure is executed if it is not `null`.
The function returns the result of the executed closure.

### Examples

```php
use function PhpRepos\ControlFlow\Conditional\when;

$result = when(true, fn () => 'yes', fn () => 'no');
assert_true('yes' === $result);

$result = when(false, fn () => 'yes', fn () => 'no');
assert_true('no' === $result);

$result = when(true, fn () => 'yes');
assert_true('yes' === $result);

$result = when(false, fn () => 'yes');
assert_true(is_null($result));
```

## unless

# Signature

```php
function unless(bool $condition, Closure $then, Closure $otherwise = null): mixed
```

### Definition

The `unless` function executes the `$then` closure if the `$condition` is `false`.
If the `$condition` is `true`, the `$otherwise` closure is executed if it is not `null`.
The function returns the result of the executed closure.

### Examples

```php
use function PhpRepos\ControlFlow\Conditional\unless;

$result = unless(false, fn () => 'yes', fn () => 'no');
assert_true('yes' === $result);

$result = unless(true, fn () => 'yes', fn () => 'no');
assert_true('no' === $result);

$result = unless(true, fn () => 'yes');
assert_true(is_null($result));

$result = unless(true, fn () => 'yes');
assert_true(is_null($result));
```

## when_exists

# Signature

```php
function when_exists(mixed $value, Closure $then, Closure $otherwise = null): mixed
```

### Definition

The `when_exists` function executes the `$then` closure if the `$value` is not `null`.
If the `$value` is `null`, the `$otherwise` closure is executed if it is not `null`.
The function returns the result of the executed closure.

### Examples

```php
use function PhpRepos\ControlFlow\Conditional\when_exists;

$result = when_exists('hello', fn ($value) => strtoupper($value));
assert_true('HELLO' === $result);

$result = when_exists(null, fn ($value) => strtoupper($value));
assert_true(is_null($result));

$result = when_exists(null, fn ($value) => strtoupper($value), fn () => 'value is null');
assert_true('value is null' === $result);

$result = when_exists(null, fn ($value) => strtoupper($value));
assert_true(is_null($result));
```
