#git #line-endings #crlf #wsl

When editing a Windows-hosted project from WSL (or otherwise mixing line-ending expectations), force CRLF line endings on checkout instead of Git's default LF-on-Linux behavior:

```
git config core.autocrlf true
```

Run from the project root. See the [WSL line-endings issue discussion](https://github.com/Microsoft/WSL/issues/184) for why this matters when a Windows tool (e.g. Visual Studio) expects CRLF but the repo is being edited from the Linux side.
