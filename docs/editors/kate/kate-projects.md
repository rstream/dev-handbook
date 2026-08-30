# Kate projects

[← back](index.md)

Basic setup for Kate `Project` plugin.

Official docs: [Kate Project Plugin](https://docs.kde.org/trunk_kf6/en/kate/kate/kate-application-plugin-projects.html)

## 1. Enable Project plugin

Navigate to:  
`Settings > Configure Kate > Plugins`

Enable the `Project` plugin.

After that Kate loads projects automatically:
* create a `.kateproject` file in the root folder
* open any file from this folder or any nested folder
* or open the folder itself with `kate /path/to/folder`

## 2. Minimal `.kateproject`

Create `.kateproject` in the folder that should become the project root:

```json
{
  "name": "My project",
  "files": [
    {
      "directory": ".",
      "recursive": 1
    }
  ]
}
```

Meaning:
* `"directory": "."` - use the folder where `.kateproject` is located
* `"recursive": 1` - include files from nested folders too
* no `"filters"` - do not limit the project to specific file masks

## 3. Include hidden files

To show hidden files and folders in the left `Projects` tree, add `"hidden": 1`:

```json
{
  "name": "My project",
  "files": [
    {
      "directory": ".",
      "recursive": 1,
      "hidden": 1
    }
  ]
}
```

This is the important flag for files like `.env`, `.gitignore`, `.editorconfig`, `.github/`, etc.

## 4. Optional excludes

If the project becomes too noisy, exclude folders with `exclude_patterns`:

```json
{
  "name": "My project",
  "files": [
    {
      "directory": ".",
      "recursive": 1,
      "hidden": 1
    }
  ],
  "exclude_patterns": [
    "^node_modules/.*",
    "^build/.*",
    "^dist/.*"
  ]
}
```

`exclude_patterns` uses regular expressions relative to the project root.

## Notes

* The file must be named exactly `.kateproject`.
* The content is JSON, so no comments and no trailing commas.
* Kate may also auto-load Git/SVN/Hg projects, but explicit `.kateproject` is more predictable when you need all files, including hidden or untracked files.
