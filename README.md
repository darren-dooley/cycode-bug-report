### Bug Report
* This project is using `vite@4.5.2`, however, Cycode is incorrectly marking it as using version `4.4.9`.
* This is because the scanner is not taking into account the override that is in the [./pnpm-workspace.yaml](https://github.com/darren-dooley/cycode-bug-report/blob/main/pnpm-workspace.yaml) file.
```
overrides:
  "vite": "4.5.2"
```
* This override can be verified by checking the `vite` version used in the `pnpm-lock.yaml` file, as seen [here](https://github.com/darren-dooley/cycode-bug-report/blob/main/pnpm-lock.yaml#L428).
* If a lockfile exists, the scanner should use it as the primary source for dependencies. This guarantees an accurate list of all resolved dependencies in the pnpm workspace.  
  * Note: Some package.json files in the repository may not be part of the same pnpm workspace, so the scanner should check workspace membership before relying on the lockfile for those packages.
