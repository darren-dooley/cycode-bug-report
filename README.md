### Bug Report
* Cycode is reporting a vulnerability in the package `vite@4.4.9`.
* This is because `vite@4.4.9` is in the list of dependencies in `packages/broken-package/package.json`, however, this package version has been overridden in the `./pnpm-workspace.yaml` file via the following snippet:
```
overrides:
  "vite": "4.5.2"
```
* This override can be verified by checking `vite` version used in the `pnpm-lock.yaml` file. Below is a snippet from the lock file
