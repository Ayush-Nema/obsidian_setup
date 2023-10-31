# Click-to-view image and text

1. Code for presenting a click-to-view image (and text).
   
```html
<details>
   <summary>Click to see image</summary>
   <br>
   <img width="100%" src="dirname/filename.png">
   ---
</details>
```

2. For viewing the text

```md
<details>
  <summary>Click me</summary>
  
  ### Heading
  1. Foo
  2. Bar
     * Baz
     * Qux

  ### Some Javascript
  ```js
  function logSomething(something) {
    console.log('Something', something);
  }
  ```
</details>
```


## Reference link(s):
- [How to add a collapsible section in markdown](https://gist.github.com/pierrejoubert73/902cc94d79424356a8d20be2b382e1ab)
