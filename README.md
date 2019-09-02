std/lib: unofficial new std runtime kit
====

`std-lib` is a type-safe collection of helper utilities and safe implementations of several php “core” functions.

For more about the guarantees of `std/lib`, see [the stdlib website](http://std-lib.github.io).

**This library is currently on hold undergoing very basic QA.  It should be generally available by the end of September 2019.**

## Methods Provided:


### `Std\Str` functions

`Str` is the standard name for the UTF-8 ready string utilities.

### `Std\Arr` functions

`Arr` is the standard name for array utilities (due to `Array` being reserved).

###### `\Std\Arr::callRecursive(array $array, callable $method)`

###### `\Std\Arr::arrayUniqueRecursive(array $array)`
###### `\Std\Arr::keyWalk(array $inputArray, callable $fn)`
###### `\Std\Arr::count($array) : array`
​	Counts the value or throws an exception.



###### `\Std\Arr::countAny($arrayOrOther): int`

​	Accepts any value, not just countables, returning zero for non-countables and throwing no exception. 



###### `\Std\Arr::getColumn($array)`

​	Same as `array_column`, but preserves keys and additional type-checks.
​	If the key (column) does not exist within the sub-element, a `Array\MissingKeyException` is thrown.
​	If any of the sub-elements are not arrays, a `Array\UnexpectedElementException` is thrown.



###### \Std\Arr::pileByColumn(array $inputArray, string $column) : array`

Returns a newly structured array with an additional dimension added, so that the input array

```php
    [
      ['id' => 'ipsum', 'a' => '1', 'b' => '2', 'c' => 'charlie'],
      ['id' => 'lorem', 'd' => '4', 'e' => '2', 'f' => 'foxtrot'],  // Note these are both id "lorem"
      ['id' => 'lorem', 'g' => '1', 'h' => '2', 'z' => 'zeta'],     // Note these are both id "lorem"
    ]
```

If "piled" by the column "id", would become:
```php
[
	['ipsum'] => [
		['id' => 'ipsum'', ''a' => '1', 'b' => '2', 'c' => 'charlie']     
	],
	['lorem'] => [
		['id' => 'lorem', ''d' => '4', 'e' => '2', 'f' => 'foxtrot'],
		['id' => 'lorem', ''g' => '1', 'h' => '2', 'z' => 'zeta'],
	]
]
```



###### \Std\Arr::rekeyByColumn(array[] $inputArray, string $columnName): array`

​	Assuming each element of `$inputArray` is an array, and within it a sub-element with key `$columnName` with a valid key as the value, re-keys the array using that value.  
​    
​	If the values of these values are not unique, an `LossyOperationException` exception will be thrown.  
​	If any of elements aren't an array, a `Array\MissingKeyException` or `Array\UnexpectedElementException` is thrown.



###### `\Std\Arr::rekeyByColumnLossy(array[] $inputArray, string $columnName) : array`
​	See `\Std\Arr::rekeyByColumn`, however this allows losses during conversion.



###### `\Std\Arr::columnPopLeft(array[] $inputArray) : array`

​	Pops the "left" or "top" (first-most, or lowest-indexed) element off of each sub-array element, returning an array of these values.   
​	If any element contains zero elements, `NULL` is returned in it's place.  
​	If it is any other type than `array`, `Array\UnexpectedElementException` is thrown.   



`\Std\Arr::columnPopLeft(array[] $inputArray) : array`
	Pops the "right" or "bottom" most element off each sub-array element.



##### Undocumented

###### `\Std\Arr::columnRecursive(Iterable $haystack, ...$subKey)`

###### `\Std\Arr::columnSearch(Iterable $haystack, $needle)`

###### `\Std\Arr::columnSearchRecursive(Iterable $haystack, $needle)`
###### `\Std\Arr::combineWith($value, $keyKey, $valueKey, $keyInsensitive = false)`
###### `\Std\Arr::idiff($x, $y)`
​	Effectively: array_unique(array_merge(array_intersect($x, $y), array_intersect($y, $x)));
###### `\Std\Arr::keyEach($array, $callback)`
###### `\Std\Arr::mapReduce(callable $mapReduceFn, ... $values)`
###### `\Std\Arr::merge(array $array1, array $array2 = null, array $_ = null)`
###### `\Std\Arr::multisort(array $arr, $arg = null, $arg = null, $_ = null)`
###### `\Std\Arr::popLeft(array $array)`
###### `\Std\Arr::popRight(array $array)`
###### `\Std\Arr::push(array $array, ...$vars)`
###### `\Std\Arr::reduce_j(callable $reduceFn, $values)`
###### `\Std\Arr::search($needle, array $haystack, $strict = null)`
###### `\Std\Arr::shift(array $array)`
###### `\Std\Arr::slice(array $array, $offset, $length = null)`
​	See Also: Std\List::slice(array $array, $offset, $length = null)
###### `\Std\Arr::splice(array $input, $offset, $length = null, $replacement = null)`
###### `\Std\Arr::unshift(array $array, ...$vars)`
###### `\Std\Arr::walk(array $array, $funcname, $userdata = null)`
###### `\Std\Arr::walkRecursive(array $input, $funcname, $userdata = null)`
###### `\Std\Arr::trim($array)`

#### Exceptions

 - \Std\ExceptionInterface
   - \Std\RuntimeException
   - \Std\UnexpectedTypeException - For non-typehinted methods
   - \Std\UnexpectedValueException
   - \Std\UnsafeOperationException
   - \Std\InformativeExceptionInterface - Provides user-friendly error message

 - \Std\Array\ExceptionInterface
   - Array\UnexpectedElementException
   - Array\KeyCollisionException
   
#### `Std\Introspect`

Introspection and internals functions

###### Introspect::getCallableName($callable)
