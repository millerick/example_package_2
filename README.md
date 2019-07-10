Run the following:
```
npm i
npm ls
```
Observe the following output from `npm ls`:
```
example_package_2@1.0.0 /src/example_package_2
├─┬ async@2.6.1
│ └── lodash@4.17.11
└─┬ example_package_1@1.5.0 (git+ssh://git@github.com/millerick/example_package_1.git#903df064912d1ecb2d0e557379c0b0ff72509480)
  └─┬ async@2.6.2
    └── lodash@4.17.11 deduped
```
Run the following:
```
npm ci
npm ls
```
Observe the following output from `npm ls`:
```
example_package_2@1.0.0 /src/example_package_2
├─┬ async@2.6.1
│ └── lodash@4.17.11
└─┬ UNMET DEPENDENCY example_package_1@git+ssh://git@github.com/millerick/example_package_1.git#903df064912d1ecb2d0e557379c0b0ff72509480
  └─┬ UNMET DEPENDENCY async@2.6.2
    └── lodash@4.17.11 deduped

npm ERR! missing: example_package_1@git+ssh://git@github.com/millerick/example_package_1.git#v1.5.0, required by example_package_2@1.0.0
npm ERR! missing: async@2.6.2, required by example_package_1@git+ssh://git@github.com/millerick/example_package_1.git#903df064912d1ecb2d0e557379c0b0ff72509480
```
Note:
- The output differs.  After using `npm ci` with a git dependency, the dependency tree says that it is invalid, even though the proper packages are in fact installed.

Ramifications:
- Erroneous `npm ls` output after `npm ci` makes it difficult to programmatically enforce that `npm ls` does not report any violations.
