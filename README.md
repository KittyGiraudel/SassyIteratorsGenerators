SassyIterators
==============

Iterators implementation in Sass. Just for the heck of it.

## Initialize an iterator

```scss
$iterator: iterator('Hello world!');
// (done: false, value: null, collection: 'Hello world!', position: 0)
```

## Get next value in iterator

```scss
$value: iterator-next($iterator);
// (done: false, value: 'H', collection: 'Hello world!', position: 1)
```

## Have a clean view of the iterator

```scss
$iterator-api: iterator-api($iterator);
// (done: false, value: 'H')
```

## Reset iterator

```scss
$iterator: iterator-rewind($iterator);
// (done: false, value: null, collection: 'Hello world!', position: 0)
```

## Check if iterator is still valid

```scss
$is-valid: iterator-valid($iterator);
// true
```

## Example

```scss
.example {
  $iterator: iterator('Hello');

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
  content: ("done": false, "value": "e");
  content: ("done": false, "value": "l");
  content: ("done": false, "value": "l");
  content: ("done": false, "value": "o");
  content: ("done": true, "value": null);
}
```