SassyIterators
==============

Iterators implementation in Sass. Just for the heck of it. [Demo](http://sassmeister.com/gist/d94049a3d516e31a8dad).

## Initialize an iterator

```scss
$iterator: iterator('Hello world!');
// (done: false, value: null, collection: 'Hello world!', position: 0, yield: null, args: ())
```

## Get next value in iterator

```scss
$value: iterator-next($iterator);
// (done: false, value: 'H', collection: 'Hello world!', position: 1, yield: null, args: ())
```

## Have a clean view of the iterator

```scss
$iterator-api: iterator-api($iterator);
// (done: false, value: 'H')
```

## Reset iterator

```scss
$iterator: iterator-rewind($iterator);
// (done: false, value: null, collection: 'Hello world!', position: 0, yield: null, args: ())
```

## Check if iterator is still valid

```scss
$is-valid: iterator-valid($iterator);
// true
```

## Specify a yield mapping function in iterator

```scss
$iterator: iterator('Hello world!', 'to-upper-case');
// (done: false, value: null, collection: 'abc', position: 0, yield: 'to-upper-case', args: ())

$value: iterator-next($iterator);
// (done: false, value: 'A', collection: 'abc', position: 1, yield: 'to-upper-case', args: ())
```

## Example

```scss
.example {
  $iterator: iterator('hello', 'to-upper-case');

  @while iterator-valid($iterator) {
    content: inspect(iterator-api($iterator));
    $iterator: iterator-next($iterator);
  }

  content: inspect(iterator-api($iterator));
}
```

Result:

```css
.example {
  content: ("done": false, "value": null);
  content: ("done": false, "value": "H");
  content: ("done": false, "value": "E");
  content: ("done": false, "value": "L");
  content: ("done": false, "value": "L");
  content: ("done": false, "value": "O");
  content: ("done": true, "value": null);
}
```