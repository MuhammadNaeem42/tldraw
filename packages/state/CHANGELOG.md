# v2.1.2 (Thu Apr 25 2024)

### Release Notes

#### Revert "[signia] Smart dirty checking of active computeds (#3516)" ([#3611](https://github.com/tldraw/tldraw/pull/3611))

This performance optimisation introduced a regression where sometimes computed caches wouldn't get invalidated at the correct time, leading to stale data causing crashes. We're reverting the change for now.

---

#### 🐛 Bug Fix

- Revert "[signia] Smart dirty checking of active computeds (#3516)" [#3611](https://github.com/tldraw/tldraw/pull/3611) ([@SomeHats](https://github.com/SomeHats))

#### Authors: 1

- alex ([@SomeHats](https://github.com/SomeHats))

---

# v2.1.0 (Tue Apr 23 2024)

### Release Notes

#### [perf] faster signia capture (again) ([#3487](https://github.com/tldraw/tldraw/pull/3487))

- Add a brief release note for your PR here.

#### [perf] faster signia capture ([#3471](https://github.com/tldraw/tldraw/pull/3471))

- Slight performance improvement to reactivity bookkeeping.

#### New migrations again ([#3220](https://github.com/tldraw/tldraw/pull/3220))

#### BREAKING CHANGES

- The `Migrations` type is now called `LegacyMigrations`.
- The serialized schema format (e.g. returned by `StoreSchema.serialize()` and `Store.getSnapshot()`) has changed. You don't need to do anything about it unless you were reading data directly from the schema for some reason. In which case it'd be best to avoid that in the future! We have no plans to change the schema format again (this time was traumatic enough) but you never know.
- `compareRecordVersions` and the `RecordVersion` type have both disappeared. There is no replacement. These were public by mistake anyway, so hopefully nobody had been using it.
- `compareSchemas` is gone. Comparing the schemas directly is no longer really possible since we introduced some fuzziness. The best thing to do now to check compatibility is to call `schema.getMigraitonsSince(prevSchema)` and it will return an error if the schemas are not compatible, an empty array if there are no migrations to apply since the prev schema, and a nonempty array otherwise.

   Generally speaking, the best way to check schema compatibility now is to call `store.schema.getMigrationsSince(persistedSchema)`. This will throw an error if there is no upgrade path from the `persistedSchema` to the current version.

- `defineMigrations` has been deprecated and will be removed in a future release. For upgrade instructions see https://tldraw.dev/docs/persistence#Updating-legacy-shape-migrations-defineMigrations

- `migrate` has been removed. Nobody should have been using this but if you were you'll need to find an alternative. For migrating tldraw data, you should stick to using `schema.migrateStoreSnapshot` and, if you are building a nuanced sync engine that supports some amount of backwards compatibility, also feel free to use `schema.migratePersistedRecord`.
- the `Migration` type has changed. If you need the old one for some reason it has been renamed to `LegacyMigration`. It will be removed in a future release.
- the `Migrations` type has been renamed to `LegacyMigrations` and will be removed in a future release.
- the `SerializedSchema` type has been augmented. If you need the old version specifically you can use `SerializedSchemaV1`

#### [perf] Reinstate render throttling ([#3160](https://github.com/tldraw/tldraw/pull/3160))

- Add a brief release note for your PR here.

#### Performance improvements ([#2977](https://github.com/tldraw/tldraw/pull/2977))

- Improves the performance of rendering.

#### Fix typo in useValue comment ([#3088](https://github.com/tldraw/tldraw/pull/3088))

- Fix typo in useValue comment.

---

#### 💥 Breaking Change

- Performance improvements [#2977](https://github.com/tldraw/tldraw/pull/2977) ([@MitjaBezensek](https://github.com/MitjaBezensek) [@steveruizok](https://github.com/steveruizok))

#### 📚 SDK Changes

- [signia] Smart dirty checking of active computeds [#3516](https://github.com/tldraw/tldraw/pull/3516) ([@ds300](https://github.com/ds300))
- [perf] faster signia capture (again) [#3487](https://github.com/tldraw/tldraw/pull/3487) ([@ds300](https://github.com/ds300))
- [perf] faster signia capture [#3471](https://github.com/tldraw/tldraw/pull/3471) ([@ds300](https://github.com/ds300))
- New migrations again [#3220](https://github.com/tldraw/tldraw/pull/3220) ([@ds300](https://github.com/ds300) [@steveruizok](https://github.com/steveruizok))
- Add white migration [#3334](https://github.com/tldraw/tldraw/pull/3334) ([@steveruizok](https://github.com/steveruizok))
- Fix blur bug in editable text [#3343](https://github.com/tldraw/tldraw/pull/3343) ([@steveruizok](https://github.com/steveruizok))
- [perf] Reinstate render throttling [#3160](https://github.com/tldraw/tldraw/pull/3160) ([@ds300](https://github.com/ds300))

#### 📖 Documentation changes

- Fix typo in useValue comment [#3088](https://github.com/tldraw/tldraw/pull/3088) ([@Slowhand0309](https://github.com/Slowhand0309))

#### 🏠 Internal

- Revert "[perf] faster signia capture (#3471)" [#3480](https://github.com/tldraw/tldraw/pull/3480) ([@ds300](https://github.com/ds300))
- Revert perf changes [#3217](https://github.com/tldraw/tldraw/pull/3217) ([@MitjaBezensek](https://github.com/MitjaBezensek))

#### 🐛 Bug Fixes

- Revert throttling of useValue and useStateTracking. [#3129](https://github.com/tldraw/tldraw/pull/3129) ([@MitjaBezensek](https://github.com/MitjaBezensek))

#### Authors: 4

- David Sheldrick ([@ds300](https://github.com/ds300))
- Mitja Bezenšek ([@MitjaBezensek](https://github.com/MitjaBezensek))
- Slowhand ([@Slowhand0309](https://github.com/Slowhand0309))
- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-beta.5 (Thu Feb 29 2024)

#### 🔩 Dependency Updates

- bump typescript / api-extractor [#2949](https://github.com/tldraw/tldraw/pull/2949) ([@steveruizok](https://github.com/steveruizok))

#### Authors: 1

- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-beta.4 (Wed Feb 21 2024)

### Release Notes

#### Improve signia error handling ([#2835](https://github.com/tldraw/tldraw/pull/2835))

- Add a brief release note for your PR here.

---

#### 🐛 Bug Fix

- Improve signia error handling [#2835](https://github.com/tldraw/tldraw/pull/2835) ([@ds300](https://github.com/ds300))

#### 🏠 Internal

- Check tsconfig "references" arrays [#2891](https://github.com/tldraw/tldraw/pull/2891) ([@ds300](https://github.com/ds300))
- dev: swap yarn test and test-dev for better dx [#2773](https://github.com/tldraw/tldraw/pull/2773) ([@mimecuvalo](https://github.com/mimecuvalo))

#### Authors: 2

- David Sheldrick ([@ds300](https://github.com/ds300))
- Mime Čuvalo ([@mimecuvalo](https://github.com/mimecuvalo))

---

# v2.0.0-beta.3 (Tue Feb 13 2024)

### Release Notes

#### dev: add test-dev command for easier testing of packages ([#2627](https://github.com/tldraw/tldraw/pull/2627))

- Adds easier testing command for individual packages.

---

#### 🚀 Enhancement

- [dx] use Biome instead of Prettier, part 2 [#2731](https://github.com/tldraw/tldraw/pull/2731) ([@si14](https://github.com/si14))

#### 🏠 Internal

- Unbiome [#2776](https://github.com/tldraw/tldraw/pull/2776) ([@si14](https://github.com/si14))
- Update the project to Node 20 [#2691](https://github.com/tldraw/tldraw/pull/2691) ([@si14](https://github.com/si14))
- dev: add test-dev command for easier testing of packages [#2627](https://github.com/tldraw/tldraw/pull/2627) ([@mimecuvalo](https://github.com/mimecuvalo))
- unbrivate, dot com in [#2475](https://github.com/tldraw/tldraw/pull/2475) ([@steveruizok](https://github.com/steveruizok) [@si14](https://github.com/si14) [@SomeHats](https://github.com/SomeHats))
- Add docs [#2470](https://github.com/tldraw/tldraw/pull/2470) ([@steveruizok](https://github.com/steveruizok))

#### 🔩 Dependency Updates

- Bump Yarn to 4.0.2 and add version constraints [#2481](https://github.com/tldraw/tldraw/pull/2481) ([@si14](https://github.com/si14))

#### Authors: 4

- alex ([@SomeHats](https://github.com/SomeHats))
- Dan Groshev ([@si14](https://github.com/si14))
- Mime Čuvalo ([@mimecuvalo](https://github.com/mimecuvalo))
- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-beta.1 (Wed Dec 20 2023)

### Release Notes

#### Remove deprecated getters ([#2333](https://github.com/tldraw/tldraw/pull/2333))

- (Breaking) Removed deprecated getters.

#### Use a global singleton for tlstate ([#2322](https://github.com/tldraw/tldraw/pull/2322))

- Make a global singleton for tlstate.

---

#### 💥 Breaking Change

- bump to beta [#2364](https://github.com/tldraw/tldraw/pull/2364) ([@steveruizok](https://github.com/steveruizok))
- Change licenses to tldraw [#2167](https://github.com/tldraw/tldraw/pull/2167) ([@steveruizok](https://github.com/steveruizok))
- Remove deprecated getters [#2333](https://github.com/tldraw/tldraw/pull/2333) ([@ds300](https://github.com/ds300))

#### 🐛 Bug Fix

- Fix TSDoc for @tldraw/state [#2327](https://github.com/tldraw/tldraw/pull/2327) ([@ds300](https://github.com/ds300))
- Use a global singleton for tlstate [#2322](https://github.com/tldraw/tldraw/pull/2322) ([@ds300](https://github.com/ds300))

#### Authors: 2

- David Sheldrick ([@ds300](https://github.com/ds300))
- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-alpha.19 (Tue Dec 12 2023)

#### 💥 Breaking Change

- No impure getters pt 1 [#2189](https://github.com/tldraw/tldraw/pull/2189) ([@steveruizok](https://github.com/steveruizok) [@ds300](https://github.com/ds300))

#### 🐛 Bug Fix

- no impure getters pt 11 [#2236](https://github.com/tldraw/tldraw/pull/2236) ([@ds300](https://github.com/ds300))
- No impure getters pt10 [#2235](https://github.com/tldraw/tldraw/pull/2235) ([@ds300](https://github.com/ds300))

#### 📝 Documentation

- Replace getters in examples [#2261](https://github.com/tldraw/tldraw/pull/2261) ([@ds300](https://github.com/ds300))

#### Authors: 2

- David Sheldrick ([@ds300](https://github.com/ds300))
- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-alpha.18 (Fri Nov 10 2023)

### Release Notes

#### Remove (optional) from jsdocs ([#2109](https://github.com/tldraw/tldraw/pull/2109))

- dev: Removed duplicate/inconsistent `(optional)`s from docs

---

#### 🏠 Internal

- Revert "bump prerelease from alpha to beta" [#2192](https://github.com/tldraw/tldraw/pull/2192) ([@ds300](https://github.com/ds300))
- bump prerelease from alpha to beta [#2148](https://github.com/tldraw/tldraw/pull/2148) ([@ds300](https://github.com/ds300))

#### 📝 Documentation

- Remove (optional) from jsdocs [#2109](https://github.com/tldraw/tldraw/pull/2109) ([@TodePond](https://github.com/TodePond))

#### Authors: 2

- David Sheldrick ([@ds300](https://github.com/ds300))
- Lu Wilson ([@TodePond](https://github.com/TodePond))

---

# v2.0.0-alpha.16 (Wed Oct 11 2023)

#### 🏠 Internal

- Publish api.json [#2034](https://github.com/tldraw/tldraw/pull/2034) ([@steveruizok](https://github.com/steveruizok))

#### Authors: 1

- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-alpha.15 (Fri Oct 06 2023)

### Release Notes

#### Editor commands API / effects ([#1778](https://github.com/tldraw/tldraw/pull/1778))

- tbd

#### tldraw zero - package shuffle ([#1710](https://github.com/tldraw/tldraw/pull/1710))

- [@tldraw/editor] lots, wip
- [@tldraw/ui] gone, merged to tldraw/tldraw
- [@tldraw/polyfills] gone, merged to tldraw/editor
- [@tldraw/primitives] gone, merged to tldraw/editor / tldraw/tldraw
- [@tldraw/indices] gone, merged to tldraw/editor
- [@tldraw/file-format] gone, merged to tldraw/tldraw

---

#### 💥 Breaking Change

- Revert "Editor commands API / effects" [#1783](https://github.com/tldraw/tldraw/pull/1783) ([@steveruizok](https://github.com/steveruizok))
- Editor commands API / effects [#1778](https://github.com/tldraw/tldraw/pull/1778) ([@steveruizok](https://github.com/steveruizok))
- tldraw zero - package shuffle [#1710](https://github.com/tldraw/tldraw/pull/1710) ([@steveruizok](https://github.com/steveruizok) [@SomeHats](https://github.com/SomeHats))

#### 🚀 Enhancement

- [improvement] More selection logic [#1806](https://github.com/tldraw/tldraw/pull/1806) ([@steveruizok](https://github.com/steveruizok))

#### Authors: 2

- alex ([@SomeHats](https://github.com/SomeHats))
- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-alpha.14 (Tue Jul 04 2023)

#### 🐛 Bug Fix

- [fix] rename `global` in @tldraw/state to avoid collissions [#1672](https://github.com/tldraw/tldraw/pull/1672) ([@steveruizok](https://github.com/steveruizok))

#### Authors: 1

- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-alpha.13 (Wed Jun 28 2023)

#### 🔩 Dependency Updates

- Incorporate signia as @tldraw/state [#1620](https://github.com/tldraw/tldraw/pull/1620) ([@steveruizok](https://github.com/steveruizok) [@ds300](https://github.com/ds300))

#### Authors: 2

- David Sheldrick ([@ds300](https://github.com/ds300))
- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# v2.0.0-alpha.12 (Mon Apr 03 2023)

#### 🐛 Bug Fix

- Make sure all types and build stuff get run in CI [#1548](https://github.com/tldraw/tldraw-lite/pull/1548) ([@SomeHats](https://github.com/SomeHats))
- add pre-commit api report generation [#1517](https://github.com/tldraw/tldraw-lite/pull/1517) ([@SomeHats](https://github.com/SomeHats))
- [chore] restore api extractor [#1500](https://github.com/tldraw/tldraw-lite/pull/1500) ([@steveruizok](https://github.com/steveruizok))
- Asset loading overhaul [#1457](https://github.com/tldraw/tldraw-lite/pull/1457) ([@SomeHats](https://github.com/SomeHats))
- David/publish good [#1488](https://github.com/tldraw/tldraw-lite/pull/1488) ([@ds300](https://github.com/ds300))
- [chore] alpha 10 [#1486](https://github.com/tldraw/tldraw-lite/pull/1486) ([@ds300](https://github.com/ds300))
- [chore] package build improvements [#1484](https://github.com/tldraw/tldraw-lite/pull/1484) ([@ds300](https://github.com/ds300))
- [chore] bump for alpha 8 [#1485](https://github.com/tldraw/tldraw-lite/pull/1485) ([@steveruizok](https://github.com/steveruizok))
- [fix] page point offset [#1483](https://github.com/tldraw/tldraw-lite/pull/1483) ([@steveruizok](https://github.com/steveruizok))
- stop using broken-af turbo for publishing [#1476](https://github.com/tldraw/tldraw-lite/pull/1476) ([@ds300](https://github.com/ds300))
- [chore] add canary release script [#1423](https://github.com/tldraw/tldraw-lite/pull/1423) ([@ds300](https://github.com/ds300) [@steveruizok](https://github.com/steveruizok))
- [chore] upgrade yarn [#1430](https://github.com/tldraw/tldraw-lite/pull/1430) ([@ds300](https://github.com/ds300))
- flush store on attach [#1449](https://github.com/tldraw/tldraw-lite/pull/1449) ([@ds300](https://github.com/ds300))
- [fix] dev version number for tldraw/tldraw [#1434](https://github.com/tldraw/tldraw-lite/pull/1434) ([@steveruizok](https://github.com/steveruizok))
- repo cleanup [#1426](https://github.com/tldraw/tldraw-lite/pull/1426) ([@steveruizok](https://github.com/steveruizok))
- [fix] use polyfill for `structuredClone` [#1408](https://github.com/tldraw/tldraw-lite/pull/1408) ([@TodePond](https://github.com/TodePond) [@steveruizok](https://github.com/steveruizok))
- Run all the tests. Fix linting for tests. [#1389](https://github.com/tldraw/tldraw-lite/pull/1389) ([@MitjaBezensek](https://github.com/MitjaBezensek))

#### Authors: 5

- alex ([@SomeHats](https://github.com/SomeHats))
- David Sheldrick ([@ds300](https://github.com/ds300))
- Lu[ke] Wilson ([@TodePond](https://github.com/TodePond))
- Mitja Bezenšek ([@MitjaBezensek](https://github.com/MitjaBezensek))
- Steve Ruiz ([@steveruizok](https://github.com/steveruizok))

---

# @tldraw/tlstore

## 2.0.0-alpha.11

### Patch Changes

- fix some package build scripting
- Updated dependencies
  - @tldraw/utils@2.0.0-alpha.10

## 2.0.0-alpha.10

### Patch Changes

- 4b4399b6e: redeploy with yarn to prevent package version issues
- Updated dependencies [4b4399b6e]
  - @tldraw/utils@2.0.0-alpha.9

## 2.0.0-alpha.9

### Patch Changes

- Release day!
- Updated dependencies
  - @tldraw/utils@2.0.0-alpha.8

## 2.0.0-alpha.8

### Patch Changes

- 23dd81cfe: Make signia a peer dependency

## 2.0.0-alpha.7

### Patch Changes

- Bug fixes.
- Updated dependencies
  - @tldraw/utils@2.0.0-alpha.7

## 2.0.0-alpha.6

### Patch Changes

- Add licenses.
- Updated dependencies
  - @tldraw/utils@2.0.0-alpha.6

## 2.0.0-alpha.5

### Patch Changes

- Add CSS files to tldraw/tldraw.
- Updated dependencies
  - @tldraw/utils@2.0.0-alpha.5

## 2.0.0-alpha.4

### Patch Changes

- Add children to tldraw/tldraw
- Updated dependencies
  - @tldraw/utils@2.0.0-alpha.4

## 2.0.0-alpha.3

### Patch Changes

- Change permissions.
- Updated dependencies
  - @tldraw/utils@2.0.0-alpha.3

## 2.0.0-alpha.2

### Patch Changes

- Add tldraw, editor
- Updated dependencies
  - @tldraw/utils@2.0.0-alpha.2

## 0.1.0-alpha.11

### Patch Changes

- Fix stale reactors.
- Updated dependencies
  - @tldraw/utils@0.1.0-alpha.11

## 0.1.0-alpha.10

### Patch Changes

- Fix type export bug.
- Updated dependencies
  - @tldraw/utils@0.1.0-alpha.10

## 0.1.0-alpha.9

### Patch Changes

- Fix import bugs.
- Updated dependencies
  - @tldraw/utils@0.1.0-alpha.9

## 0.1.0-alpha.8

### Patch Changes

- Changes validation requirements, exports validation helpers.
- Updated dependencies
  - @tldraw/utils@0.1.0-alpha.8

## 0.1.0-alpha.7

### Patch Changes

- - Pre-pre-release update
- Updated dependencies
  - @tldraw/utils@0.1.0-alpha.7

## 0.0.2-alpha.1

### Patch Changes

- Fix error with HMR
- Updated dependencies
  - @tldraw/utils@0.0.2-alpha.1

## 0.0.2-alpha.0

### Patch Changes

- Initial release
- Updated dependencies
  - @tldraw/utils@0.0.2-alpha.0
