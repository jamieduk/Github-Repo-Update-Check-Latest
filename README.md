# GitHub Version Checker

**GitHub Version Checker By (c) J~Net 2026**

A lightweight Bash script that checks the version of a GitHub repository against the version used locally and tells you when a newer version is available.

The script can read the local version from a `package.json` file and checks GitHub for the latest available release, tag, or repository `package.json` version.

## Repository

[GitHub Repository](https://github.com/jamieduk/Github-Repo-Update-Check-Latest?utm_source=chatgpt.com)

**Website:** [jnetai.com](https://jnetai.com?utm_source=chatgpt.com)

## Features

* Checks the local version from `package.json`
* Supports a fallback version using `CURRENT_VERSION`
* Checks the latest GitHub release
* Falls back to the latest GitHub tag
* Falls back to the `package.json` version on the repository's default branch
* Supports GitHub repositories with or without a `.git` suffix
* Supports `v1.2.3` and `1.2.3` version formats
* Compares numeric semantic-style versions
* Uses the GitHub API
* Supports an optional `GITHUB_TOKEN` for authenticated GitHub API requests
* Offers to open the GitHub repository when an update is available
* Works with `xdg-open` on Linux
* Works with `open` on macOS
* Falls back to displaying the repository URL if no browser opener is available
* Does not modify or automatically replace any files

## Requirements

The script requires:

* Bash
* `curl`
* `sed`
* A working internet connection for GitHub checks

On Ubuntu/Debian:

```bash
# (c) J~Net 2026
sudo apt update && sudo apt install -y curl sed
```

## Installation

Clone the repository:

```bash
# (c) J~Net 2026
git clone https://github.com/jamieduk/Github-Repo-Update-Check-Latest.git
cd Github-Repo-Update-Check-Latest
chmod +x update-check.sh
./update-check.sh
```
## How it works
The check script
update-check.sh

Usage Example:
'''bash
sudo chmod +x *.sh

./update-check.sh
'''

Uses a local file package.json and compares to the github hosted version to check if version is current or out of date!

## Configuration

The repository to check is configured near the top of `update-check.sh`:

```bash
repo_to_check="https://github.com/jamieduk/Python_Cheat_Sheet"
```

Change this to the GitHub repository you want to monitor.

For example:

```bash
repo_to_check="https://github.com/username/my-project"
```

You can also pass a repository directly when running the script:

```bash
# (c) J~Net 2026
./update-check.sh https://github.com/username/my-project
```

The command-line repository takes priority over the default `repo_to_check` value.

## Local Version

If a `package.json` exists in the same directory as `update-check.sh`, the script reads its `version` value.

Example:

```json
{
  "name": "my-project",
  "version": "1.0.0"
}
```

The script will use:

```text
Current version : 1.0.0
```

If `package.json` does not exist, the script uses:

```bash
CURRENT_VERSION="${CURRENT_VERSION:-1.0.0}"
```

You can therefore override the local version without modifying the script:

```bash
# (c) J~Net 2026
CURRENT_VERSION=1.5.0 ./update-check.sh
```

## How Version Detection Works

The script checks GitHub in this order:

1. **Latest GitHub release**
2. **Latest GitHub tag**
3. **`package.json` on the repository's default branch**

This allows the checker to work with different types of GitHub projects.

### Release

If the repository has a GitHub release, its release tag is used.

For example:

```text
v2.0.0
```

### Git Tag

If no GitHub release is available, the script checks the repository tags.

### package.json

If neither a release nor tag is available, the script checks:

```text
https://raw.githubusercontent.com/OWNER/REPOSITORY/BRANCH/package.json
```

The version is read from the repository's `package.json`.

If no version information can be found, the script reports that a `package.json` should be added to the root of the repository.

## Update Detection

The script compares the current version against the latest GitHub version.

For example:

```text
Current version : 1.0.0
Latest version  : 1.2.0
An update is available (1.0.0 -> 1.2.0).
Do you want to visit the repository link? [y/N]
```

Press `y` to open the GitHub repository in your default browser.

If an update is not available:

```text
Current version : 1.2.0
Latest version  : 1.2.0
No update version is available
```

## GitHub Authentication

Unauthenticated GitHub API requests are rate limited.

For projects that make frequent checks, you can provide a GitHub token using the `GITHUB_TOKEN` environment variable.

```bash
# (c) J~Net 2026
export GITHUB_TOKEN="YOUR_GITHUB_TOKEN"
./update-check.sh
```

The script automatically sends the token to GitHub when it is available.

**Do not place your GitHub token directly inside `update-check.sh` or commit it to Git.**

## Example

With:

```bash
repo_to_check="https://github.com/jamieduk/Python_Cheat_Sheet"
```

and a local version of:

```text
1.0.0
```

the script may return:

```text
Current version : 1.0.0
Latest version  : 1.1.0
An update is available (1.0.0 -> 1.1.0).
Do you want to visit the repository link? [y/N]
```

Selecting `y` opens:

[https://github.com/jamieduk/Python_Cheat_Sheet](https://github.com/jamieduk/Python_Cheat_Sheet?utm_source=chatgpt.com)

## Running the Script

Run it using the configured repository:

```bash
# (c) J~Net 2026
./update-check.sh
```

Or specify another repository:

```bash
# (c) J~Net 2026
./update-check.sh https://github.com/jamieduk/Python_Cheat_Sheet
```

GitHub URLs can also be supplied with `.git`:

```bash
# (c) J~Net 2026
./update-check.sh https://github.com/username/project.git
```

The script normalises the repository URL before querying GitHub.

## Safety

The script is designed to **check and report updates only**.

It does not:

* Download updates automatically
* Replace project files
* Run code from the remote repository
* Modify Git repositories
* Delete existing files
* Automatically perform a Git pull
* Automatically install anything

When an update is found, it simply provides the GitHub repository link and optionally opens it in the default browser.

## File Structure

```text
Github-Repo-Update-Check-Latest/
├── update-check.sh
├── package.json
└── README.md
```

`package.json` is optional. If present, it provides the local version number.

## Licence

Copyright © J~Net 2026.

Created by **J~Net**.

[jnetai.com](https://jnetai.com?utm_source=chatgpt.com)
