# repomd

[![build status](https://api.cirrus-ci.com/github/carlwgeorge/repomd.svg)](https://cirrus-ci.com/github/carlwgeorge/repomd/master)
[![pypi](https://img.shields.io/pypi/v/repomd.svg)](https://pypi.org/project/repomd/)
[![fedora](https://img.shields.io/badge/RPM-Fedora-blue.svg)](https://src.fedoraproject.org/rpms/python-repomd)

This library provides an object-oriented interface to get information out of dnf/yum repositories.

## Update 2023-07-04

This copy of the code contains updates from the following unmerged PRs

- [#16 Add checksum properties (@sy-base)](https://github.com/carlwgeorge/repomd/pull/16)
- [#13 Add package weight (size) properties](https://github.com/carlwgeorge/repomd/pull/13)

## Usage

```python
>>> import repomd

>>> repo = repomd.load('https://mirror.rackspace.com/centos/7/updates/x86_64/')

>>> repo
<Repo: "https://mirror.rackspace.com/centos/7/updates/x86_64/">
```

The length of the `Repo` object indicates the number of packages in the repository.

```python
>>> len(repo)
1602
```

Find a package by name.

```python
>>> repo.find('systemd')
<Package: "systemd-219-57.el7_5.3.x86_64">
```

Find all packages of a given name.

```python
>>> repo.findall('systemd')
[<Package: "systemd-219-57.el7_5.1.x86_64">, <Package: "systemd-219-57.el7_5.3.x86_64">]
```

A `Package` instance has many useful properties.

```python
>>> package = repo.find('systemd')

>>> package.name
'systemd'

>>> package.version
'219'

>>> package.build_time
datetime.datetime(2018, 9, 26, 14, 11, 37)

>>> package.nevr
'systemd-219-57.el7_5.3'
```

Iterate through packages in the repository.

```python
>>> for package in repo:
...     print(package.nvr)
389-ds-base-1.3.7.5-19.el7_5
389-ds-base-1.3.7.5-21.el7_5
389-ds-base-1.3.7.5-24.el7_5
(and so on)
```
