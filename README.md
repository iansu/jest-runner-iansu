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

## How it works

This patch only requires adding a few lines of code to the [`testWorker.js`](packages/jest-27/build/testWorker.js) file:

```js
const heap = v8.getHeapStatistics();

if (heap.total_heap_size / heap.heap_size_limit > 0.8) {
  (0, _exit().default)(1);
}
```

When a test is dispatched to the worker we first check if the heap usage is above 80%. If it is, the worker just exits with a non-zero exit code. Jest will automatically detect this and spawn a new worker. If the heap usage is below 80% the worker runs the test as usual.

## License

The original `jest-runner` is released under the MIT license as are all changes in the patched versions.
