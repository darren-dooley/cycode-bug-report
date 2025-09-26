### Bug Report
* This project is using `vite@4.5.2`, however, Cycode is incorrectly marking it as using version `4.4.9`.
* This is because the scanner is not taking into account the override that is in the [./pnpm-workspace.yaml](https://github.com/darren-dooley/cycode-bug-report/blob/main/pnpm-workspace.yaml) file.
```
overrides:
  "vite": "4.5.2"
```
* This override can be verified by checking the `vite` version used in the `pnpm-lock.yaml` file, as seen [here](https://github.com/darren-dooley/cycode-bug-report/blob/main/pnpm-lock.yaml#L428).
* Perhaps more accurate results could be achieved if the scanner used the output of `pnpm ls -r` as the primary source for dependencies. This guarantees an accurate list of all resolved dependencies in the pnpm workspace.

### Steps to Reproduce
1. Clone this repository
2. `cd` to the project root
3. Run `corepack enable & corepack use pnpm@latest-10`
4. Run `pnpm install`
5. Run `pnpm ls -r` to verify that version `vite@4.5.2` is listed
6. Run `cycode scan --scan-type=sca path .`
6. Observe that Cycode incorretly marks the version as `vite@4.4.9`

### Evidence
#### `pnpm ls -r` output:
<img width="1414" height="418" alt="Screenshot 2025-09-26 at 16 38 39" src="https://github.com/user-attachments/assets/506be882-8aa5-4b26-a643-60f49e2a646f" />


#### `cycode scan --scan-type=sca path .` output:
<img width="2542" height="492" alt="Screenshot 2025-09-26 at 16 18 46" src="https://github.com/user-attachments/assets/32aad0d6-a086-4939-82f2-a042b13454d2" />


