# Installation Guide

## Windows

Install via scoop <https://github.com/shemeshg/scoop-bucket>

remove winget install if exists [winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/):

```cmd
winget remove Shemeshg.MidiRouterClient
```

Install scoop

```
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
```

add bucket
```
scoop bucket add extras
scoop bucket add shemeshg https://github.com/shemeshg/scoop-bucket
```

install app

```
scoop install midi-router-client
```

keep updated with
```
scoop update *
```

Also see [Windows Service](installation_windows_service.md)

## macOS

Install via [Homebrew](https://brew.sh/):

```bash
brew remove --cask midi-router-client
brew install --cask shemeshg/homebrew-tap/midi-router-client
codesign --force --deep --sign - /Applications/midi-router-client.app/
xattr -c /Applications/midi-router-client.app/
```

> **Note:** macOS requires manual code signing and removal of extended attributes to ensure proper execution.

## Linux

Prebuilt `.zip` and `.deb` packages are available, targeting the oldest supported Ubuntu LTS at the time of release.

## ⚠️ Additional Notes

- Distributed binaries are **not code-signed**.

