Generators
==========

Generators implementation in Sass. Just for the heck of it. [Demo](http://sassmeister.com/gist/a23f71cf785bf555c6ed).

## Initialize a generator

```scss
@include generator('foo') {
  $list: 1 2 3 4 5;

  @each $item in $list {
    @include yield($item * $item);
  }
}
```

## Get next value in generator

```scss
$value: generator-next('foo');
// 1
```

## Reset generator

```scss
@include generator-rewind('foo');
```

## Check if generator is still valid

```scss
$is-valid: generator-valid('foo');
// true
```

## Example

```scss
.example {
  @while generator-valid('foo') {
    content: inspect(generator-next('foo'));
  }

  content: inspect(generator-next('foo')); // Done
}
```

Result:

```css
.test {
  content: ("done": false, "value": 1);
  content: ("done": false, "value": 4);
  content: ("done": false, "value": 9);
  content: ("done": false, "value": 16);
  content: ("done": false, "value": 25);
  content: ("done": true, "value": null);
}
```