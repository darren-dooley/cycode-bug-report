### Bug Report
* This project is using `vite@4.5.2`, however, Cycode is incorrectly marking it us using version `4.4.9`.
* This is because the scanner is not taking into account the overrirde that is in the [./pnpm-workspace.yaml](https://github.com/darren-dooley/cycode-bug-report/blob/main/pnpm-workspace.yaml) file.
```
overrides:
  "vite": "4.5.2"
```
* This override can be verified by checking the `vite` version used in the `pnpm-lock.yaml` file [here](https://github.com/darren-dooley/cycode-bug-report/blob/main/pnpm-lock.yaml#L428).
* If  present, I suggest that the scanner should use the `pnpm-lock.yaml` file as the single source-of-truth for the dependencies in a project.
* If no lock file is present, then the the scanner should fall back to using the package.json files in the repository.
