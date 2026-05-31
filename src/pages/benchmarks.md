# Benchmarks of JavaScript Package Managers

**Last benchmarked at**: _May 31, 2026, 3:54 AM_ (_daily_ updated).

This benchmark compares the performance of npm, pnpm, Yarn Classic, and Yarn PnP (check [Yarn's benchmarks](https://yarnpkg.com/benchmarks) for any other Yarn modes that are not included here).

Here's a quick explanation of how these tests could apply to the real world:

- `clean install`: How long it takes to run a totally fresh install: no lockfile present, no packages in the cache, no `node_modules` folder.
- `with cache`, `with lockfile`, `with node_modules`: After the first install is done, the install command is run again.
- `with cache`, `with lockfile`: When a repo is fetched by a developer and installation is first run.
- `with cache`: Same as the one above, but the package manager doesn't have a lockfile to work from.
- `with lockfile`: When an installation runs on a CI server.
- `with cache`, `with node_modules`: The lockfile is deleted and the install command is run again.
- `with node_modules`, `with lockfile`: The package cache is deleted and the install command is run again.
- `with node_modules`: The package cache and the lockfile is deleted and the install command is run again.
- `update`: Updating your dependencies by changing the version in the `package.json` and running the install command again.

## Lots of Files

The app's `package.json` [here](https://github.com/pnpm/pnpm.io/blob/main/benchmarks/fixtures/alotta-files/package.json)

| action  | cache | lockfile | node_modules| npm | pnpm | [pnpm 🦀](https://github.com/pnpm/pacquet) | Yarn | Yarn PnP |
| ---     | ---   | ---      | ---         | --- | --- | --- | --- | --- |
| install |   |   |   | 39.1s | 9s | n/a | 8.3s | 3.5s |
| install | ✔ | ✔ | ✔ | 1.4s | 485ms | n/a | 6.1s | n/a |
| install | ✔ | ✔ |   | 10.2s | 2.3s | 626ms | 6s | 1.3s |
| install | ✔ |   |   | 14.9s | 4s | n/a | 8.3s | 2.9s |
| install |   | ✔ |   | 13.3s | 9s | 3.4s | 6.1s | 1.3s |
| install | ✔ |   | ✔ | 1.9s | 3.9s | n/a | 8.2s | n/a |
| install |   | ✔ | ✔ | 1.4s | 487ms | n/a | 6s | n/a |
| install |   |   | ✔ | 1.9s | 4.5s | n/a | 8.2s | n/a |
| update | n/a | n/a | n/a | 8.2s | 12.4s | n/a | 6.6s | 3s |

<img alt="Graph of the alotta-files results" src="/img/benchmarks/alotta-files.svg?v=9a32ed59" />

### pnpm vs pnpm 🦀

pnpm v12 will use a new installation engine for fetching and linking written in Rust. See [pacquet](https://github.com/pnpm/pacquet).

| action  | cache | lockfile | node_modules| pnpm | [pnpm 🦀](https://github.com/pnpm/pacquet) |
| ---     | ---   | ---      | ---         | --- | --- |
| install | ✔ | ✔ |   | 2.3s | 626ms |
| install |   | ✔ |   | 9s | 3.4s |

<img alt="Graph comparing pnpm versions on the alotta-files fixture" src="/img/benchmarks/alotta-files-pnpm.svg?v=aab00824" />