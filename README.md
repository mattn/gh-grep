# gh-grep

Print lines matching a pattern in repositories using GitHub API

## Usage

``` console
$ gh grep func.*schema.Schema --include=**/*.go --owner k1LoW --repo tbls
k1LoW/tbls:cmd/doc.go:func withDot(s *schema.Schema, c *config.Config, force bool) (e error) {
k1LoW/tbls:cmd/doc.go:func outputErExists(s *schema.Schema, path string) bool {
k1LoW/tbls:config/config.go:func (c *Config) ModifySchema(s *schema.Schema) error {
k1LoW/tbls:config/config.go:func (c *Config) MergeAdditionalData(s *schema.Schema) error {
k1LoW/tbls:config/config.go:func (c *Config) FilterTables(s *schema.Schema) error {
k1LoW/tbls:config/config.go:func (c *Config) mergeDictFromSchema(s *schema.Schema) {
k1LoW/tbls:config/config.go:func excludeTableFromSchema(name string, s *schema.Schema) error {
[...]
```

( Do grep the codes (`**/*.go`) of [k1LoW/tbls](https://github.com/k1LoW/tbls) with the pattern `func.*schema.Schema` )

#### :warning: Notice :warning:

**`gh-grep` is very slow because it does all its scanning through the GitHub API.**

**It is recommended to specify the `--include` option to get the results in a realistic time.**

## Examples

### List Actions you are using

``` console
$ gh grep uses: --include=.github/workflows/* --owner k1LoW | sed -e 's/.*uses:\s*//g' | sort | uniq -c
   9 ./
   1 EndBug/add-and-commit@v7
   2 actions/checkout@master
  10 actions/checkout@v1
  50 actions/checkout@v2
  18 actions/setup-go@v1
  21 actions/setup-go@v2
   4 aquasecurity/trivy-action@master
[...]
```

### List base Docker images used in the Dockerfile of the project root

``` console
$ gh grep ^FROM --include=Dockerfile --owner k1LoW
k1LoW/centve:Dockerfile:FROM centos:7
k1LoW/docker-alpine-pandoc-ja:Dockerfile:FROM frolvlad/alpine-glibc
k1LoW/docker-sshd:Dockerfile:FROM docker.io/alpine:3.9
k1LoW/gh-grep:Dockerfile:FROM debian:buster-slim
k1LoW/ghdag:Dockerfile:FROM debian:buster-slim
k1LoW/ghdag-action:Dockerfile:FROM ghcr.io/k1low/ghdag:v0.16.0
k1LoW/ghput:Dockerfile:FROM alpine:3.13
k1LoW/ghput-release-action:Dockerfile:FROM ghcr.io/k1low/ghput:v0.12.0
k1LoW/github-script-ruby:Dockerfile:FROM ghcr.io/k1low/github-script-ruby-base:v1.1.0
[...]
```

## Install

`gh-grep` can be installed as a standalone command or as [a GitHub CLI extension](https://cli.github.com/manual/gh_extension)

### Install as a GitHub CLI extension

``` console
$ gh extension install k1LoW/gh-grep
```

### Install as a standalone command

Run `gh-grep` instead of `gh grep`.

**deb:**

Use [dpkg-i-from-url](https://github.com/k1LoW/dpkg-i-from-url)

``` console
$ export GH-GREP_VERSION=X.X.X
$ curl -L https://git.io/dpkg-i-from-url | bash -s -- https://github.com/k1LoW/gh-grep/releases/download/v$GH-GREP_VERSION/gh-grep_$GH-GREP_VERSION-1_amd64.deb
```

**RPM:**

``` console
$ export GH-GREP_VERSION=X.X.X
$ yum install https://github.com/k1LoW/gh-grep/releases/download/v$GH-GREP_VERSION/gh-grep_$GH-GREP_VERSION-1_amd64.rpm
```

**apk:**

Use [apk-add-from-url](https://github.com/k1LoW/apk-add-from-url)

``` console
$ export GH-GREP_VERSION=X.X.X
$ curl -L https://git.io/apk-add-from-url | sh -s -- https://github.com/k1LoW/gh-grep/releases/download/v$GH-GREP_VERSION/gh-grep_$GH-GREP_VERSION-1_amd64.apk
```

**homebrew tap:**

```console
$ brew install k1LoW/tap/gh-grep
```

**manually:**

Download binary from [releases page](https://github.com/k1LoW/gh-grep/releases)

**go get:**

```console
$ go get github.com/k1LoW/gh-grep
```

**docker:**

```console
$ docker pull ghcr.io/k1low/gh-grep:latest
```
