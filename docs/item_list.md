ItemList
========

This class takes a list of items and transforms that list through
functional - style methods.

## Quick example

```php
$list = new \Crutches\ItemList(array('foo', 'bar', 'baz'));

print_r($list->surround('-')->map('strtoupper')->takeRandom(1));
// array('-BAR-');

print_r($list->shuffle()->prefix(':'));
// array(':bar', ':baz', ':foo');

echo $list;
// "foo, bar, baz"

echo $list->human();
// foo, bar and baz
```

## Methods

Note - all of these methods work the same way in MutableItemList
too. The only difference is ItemList returns a new instance every
time, whereas MutableItemList modifies itself.

In addition to this, most ItemList methods have an optional final
argument to return the current instance instead of a new one. Pass
true to any method that takes an $in_place argument to return the same
instance.

Most of these methods allow for method chaining to keep your code clean.

### create

ItemList::create(array $list = array())

Start chaining methods immediately after creation.

```php
$shuffled = ItemList::create(array('foo', 'bar'))->shuffle();
```

### getList

$list->getList()

Get the underlying list as an array.

```php
$list = new ItemList(array('one', 'two'));
print_r($list->getList());
// array('foo', 'bar');
```

### get

$list->get(int $index)

Get an element at the specific index or null if the index is out of
range. Like arrays, the list is zero-indexed.

```php
$list = new ItemList(array('foo', 'bar'));
echo $list->get(1);
// bar

echo $list->get(5);
// null
```

### prefix

$list->prefix(string $string, $in_place = false)

Prepend a string to all elements.

```php
$list = new ItemList(array('one', 'two'));
print_r($list->prefix('item ')->getList());
// array('item one', 'item two')
```

### suffix

$list->suffix(string $string, $in_place = false)

Append a string to all elements.

```php
$list = new ItemList(array('one', 'two'));
print_r($list->suffix('potato')->getList());
// array('one potato', 'two potato')
```

### surround

$list->surround(string $string, $in_place = false)

Append and prepend a string to all elements.

```php
$list = new ItemList(array('one', 'two'));
print_r($list->surround(':')->getList());
// array(':one:', ':two:')
```

### stringify

$list->stringify(string $delimeter = ', ', string $prefix = '', string $suffix = '')

Get the list as a string, separating each value with $delimeter. If
supplied, $prefix and $suffix will be added to each value. The list is
not modified.

```php
$list = new ItemList(array('one', 'two', 'three'));
echo $list->stringify();
// one, two, three

echo $list->stringify(', ', 'item ', '!');
// item one!, item two!, item three!
```

### ___toString

When cast to a string, an ItemList returns the result of stringify().

```php
echo new ItemList(array('foo', 'bar'));
// foo, bar
```

### human

$list->human(string $ending = ' and')

A variation on stringify() that adds a different delimeter at the end
for nicer reading.

```php
$list = new ItemList(array('good', 'quick', 'cheap'));
echo $list->human();
// good, quick and cheap

echo $list->human(', or');
// good, quick, or cheap
```

### map

$list->map($callback, $in_place = false)

Map a function over all items in the list.

```php
$list = new ItemList(array('fOo', 'BaR', 'bAz'));
print_r($list->map('strtolower')->getList());
// array('foo', 'bar', 'baz');
```

### filter

$list->filter($callback, $in_place = false)

Use a function to filter items from the list.

```php
$list = new ItemList(array(1, 2.2, 3.3, 4));
print_r($list->filter('is_int)->getList());
// array(1, 4);
```

### take

$list->take(int $amount, $in_place = false);

Take a specified amount of elements from the start of the list.

```php
$list = new ItemList(array('foo', 'bar', 'baz', 'quo'));
print_r($list->take(2)->getList());
// array('foo', 'bar')
```

### takeRandom

$list->takeRandom(int $amount, $in_place = false);

Take a specified amount of elements randomly from the list.

```php
$list = new ItemList(array('good', 'quick', 'cheap'));
print_r($list->takeRandom(2)->getList());
// array('good', 'cheap');
```

### shuffle

$list->shuffle($in_place = false);

Shuffle the list and return a new instance.

```php
$list = new ItemList(array('foo', 'bar'));
$shuffled = $list->shuffle();

print_r($list->getList());
// array('foo', 'bar');

print_r($shuffled->getList());
// array('bar', 'foo');
```
