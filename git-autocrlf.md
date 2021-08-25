# Rule of thumb:

If you’re on a **Windows** machine, set it to `true` — this converts LF endings into CRLF when you check out code.

```
git config --global core.autocrlf true
```

If you’re on a **Linux** or **macOS** system that uses LF line endings, then you don’t want Git to automatically convert them when you check out files; however, if a file with CRLF endings accidentally gets introduced, then you may want Git to fix it. You can tell Git to convert CRLF to LF on commit but not the other way around by setting core.autocrlf to `input`.

```
git config --global core.autocrlf input
```

If you’re a Windows programmer doing a **Windows-only** project, then you can turn off this functionality, recording the carriage returns in the repository by setting the config value to false:

```
git config --global core.autocrlf false
```

([source](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration) and (source)[https://stackoverflow.com/questions/1967370/git-replacing-lf-with-crlf/20653073#20653073])

PS: If you config VS Code to handle LF, just disable this thing
