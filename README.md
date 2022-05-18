# jest-runner-iansu

This is a patched version of [`jest-runner`](https://github.com/facebook/jest/tree/main/packages/jest-runner) that shuts down the worker when it has used more than 80% of the available heap memory. Jest will automatically spawn a new worker and continue running the tests. This prevents any out of memory errors.

## Usage

Install the runner with npm or Yarn. Make sure you install the version that corresponds to your Jest version. For example, if you are using Jest 27:

```sh
npm i -D jest-runner-iansu@27
```

```sh
yarn add --dev jest-runner-iansu@27
```

Add this line to your Jest config:

```js
runner: 'jest-runner-iansu'
```

## License

The original `jest-runner` is released under the MIT license as are all changes in the patched versions.
