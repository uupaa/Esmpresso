| [English](README.md) | [Japanese](README.ja.md) |

# Esmpresso (pronounce as "Espresso")

The Esmpresso is a package system of the ES Modules era.
It can treat modules published in GitHub and GitLib.

## Roast (publish)

ES Modules base code can be converted to Esmpresso style. We call this a roast.

1. Setting up GitHub Pages.
    - `Settings` -> `GitHub Pages` -> `Source` -> change to `master branch` and `save`.
2. Add the `.esm.conf.js` file to the top directory, and specify the path of the entry point to` main`.
3. Register the module at https://esmpresso.com.

```js
// .esm.conf.js
export default {
  main: "index.js"
};
```

The roasted modules are shipped to the world.

## Drip (import)

Import and use the roasted module. We call this a drip.

The following is a way to dynamically drip.

```html
<script type="module">
  const Modules = { // as Roasted Modules
    Foo: "https://uupaa.github.io/Foo/index.js",
  };

  (async() => {

  //const { default: Foo } = await import(Modules.Foo); // Drip (default export)
    const { Foo } = await import(Modules.Foo); // Drip (named export)

    console.log(Foo);
  })();
</script>
```

The following is a way to statically drip.

```html
<script type="module">
  (async() => {

  //import Foo from "https://uupaa.github.io/Foo/index.js"; // Drip (default export)
    import { Foo } from "https://uupaa.github.io/Foo/index.js"; // Drip (named export)

    console.log(Foo);
  })();
</script>
```

## FAQ

- Q. How can I roast a script written in ES5?
    - A. First you need to rewrite to ES Modules style.

- Q. What should I do if I want to roast modules that others have published?
    - A. Fork the repository and roast.
        If the file corresponding to the entry point (index.js) does not exist, create it.
        Then make a merge request to the original repository.

