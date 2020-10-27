# Conventions and Best Practices

## Branches

The `master` and `develop` [approach](https://nvie.com/posts/a-successful-git-branching-model/).

+ `master`: only __production__ code
+ `fix`: branches from `master` and into `master` and `develop` and bump version number(patch)
+ `release`: branches from `develop` for bugfixes until it's ready for `master`
+ `develop`: main development branch, receives bugfixes and new features
+ `feature`: where things are actually done, branches from and into `develop`
+ `manage`: where notes files are changed

#### Naming:

`master` is master, `develop` is develop, and `manage` is manage.

Fixes `fix-nextpatch`, e.g., if version 2.3.1 has a bug, the fix is named `fix-2.3.2`.

Releases are `release-x.y.z`

Features are `whatever_you-like`, just keep it meaningful and don't use slashes.

## Commits

Format: `<branch>:[<scope>:] <verb> <object>`

- `<branch>` is the name or code of the branch. This makes it easier to keep track of branches when looking at the log.

- `<scope>` is optional and informs which part of the code was worked on.

- `<verb>` is what the commit will do. Key verbs are add, remove, fix, and change.

- `<object>` what the verb did.

- Whenever possible, keep the message under 80 characters. If need more space to describe what you did, maybe you should've made more commits.

Examples:
- `manage:conventions: change the pattern commit messages should follow`
- `react: add state to Select Components`

## Versions

[Semver approach](https://semver.org/). Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make incompatible API changes,
2. MINOR version when you add functionality in a backwards-compatible manner, and
3. PATCH version when you make backwards-compatible bug fixes.

Adicional labels: `a` for alpha, `b` for beta, `rc` for release candidate. They can receive incremental numbers too, eg. 0.0.1rc1

## Changelogs

[Keep A Change Log approach](https://keepachangelog.com/). Keep a CHANGELOG.md file with every release change in the following format:

```
## 0.0.1 (2019-06-10)

### Added
- For new features

### Changed
- For changes in existing functionality

### Deprecated
- For once-stable features removed in upcoming releases

### Removed
- For deprecated features removed in this release

### Fixed
- For any bug fixes
```

Resulting in:
## 0.0.1 (2019-06-10)

### Added
- For new features

### Changed
- For changes in existing functionality

### Deprecated
- For once-stable features removed in upcoming releases

### Removed
- For deprecated features removed in this release

### Fixed
- For any bug fixes

## Git Best Practices

- Commit related changes: fixing two different bugs should produce two diferent commits
- Commit oftern: keeping them small helps keeping changes related and makes it easier to solve conflicts
- Don't commit half-done work and test befor you commit: the commited logical chunk should make sense and work
- After choosing a workflow, stick to it: don't change patterns