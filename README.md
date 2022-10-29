# setup-golang (GitHub action)

![GitHub](https://img.shields.io/github/license/hashicorp/setup-golang)

A composite GitHub action for setting up Go compiler and module cache
- configures Go compiler using `actions/setup-go`
- configures Go modules cache using `actions/cache`
- configures GOBIN environment variable to be on `$PATH`
- compatible with `Linux`, `Darwin`, and `Windows` runners

## Inputs

- `version-file` - Either `.go-version` (default) or `go.mod`. Used to determine the version of Go compiler to configure.
- `cache-key` - Key used to share (or not share) module cache across later actions.

## Environment

- `GOBIN` - Sets `$GOBIN` to a value on `$PATH`
  - currently uses `$(go env GOROOT)/bin`

## Cache Limit

Note that GitHub limits repositories to have up to 10GiB of caches. Once the limit
is exceeded, older caches will be evicted on an LRU basis.

## Usage

#### minimal example

This example uses the default values (uses `.go-version` for the Go version
and `default` as the cache key).

```yaml
steps:
  - uses: hashicorp/setup-golang@v1
```

This example uses custom values (uses `go.mod` for the Go version and
`mykey` as the cache key).

#### complete example

```yaml
steps:
  - uses: actions/checkout@v3
  - uses: hashicorp/setup-golang@v1
    with:
      version-file: go.mod
      cache-key: mykey
```

## Cross Platform

The cache automatically keys on operating system. The cache is not shared between
Linux, Darwin, and Windows runners.

