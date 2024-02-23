# Create GitHub Release Action

This action creates a GitHub release for a repository.

It is expected to be run when on a tag, and it will use a file in the
repository to create the release notes. It can also upload assets to the
release.

The action follows [semver][], so if the tag looks like a pre-release, it will
be created as a pre-release in GitHub too.

Here is an example demonstrating how to use it in a workflow:

```yaml
jobs:
  build:
    name: Build
    runs-on: ubuntu-20.04
    permissions:
      # We need write permissions on contents to create GitHub releases
      contents: write

    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Create the GitHub release
        uses: frequenz-floss/gh-action-create-github-release@v0.x.x
```

## Inputs

* `release_notes_file`: The file name of the release notes file. Default:
  `RELEASE_NOTES.md`.

  It must exist in the repository. The contents of this file will be used as
  the release notes.

* `upload_files`: The files to be uploaded as release assets. Default: `""`.

  It will be passed directly using the shell, so it can be a glob pattern.

  If empty, nothing will be uploaded.

* `github_token`: The GitHub token to use for authentication. Default: `${{
  github.token }}`.

  This is required to create the release. It requires write permission, so you
  should add this to your job permissions:

  ```yaml
  permissions:
    contents: write
  ```

[semver]: https://semver.org
