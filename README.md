# luneutic Contributor License Agreement
## Usage
To enable the CLA check for `myrepo`, follow these steps:

- Create personal access token (PAT): https://github.com/settings/personal-access-tokens/new
  - Repository access: `luneutic/cla`
  - Repository permissions
    - Contents: `read-write`
- _myrepo_: Add the PAT to Action secrets https://github.com/luneutic/myrepo/settings/secrets/actions/new
  - Name: `CLA_REPO_TOKEN`
- _myrepo_: Create `.github/workflows/cla.yml` with the content
  ```yml
  name: Call CLA Assistant

  on:
    issue_comment:
      types: [created]
    pull_request:
      types: [opened, closed, synchronize]

  jobs:
    call-shared:
      uses: luneutic/cla/.github/workflows/cla.yml@main
      permissions:
        actions: write
        contents: read
        pull-requests: write
        statuses: write
      secrets:
        CLA_REPO_TOKEN: ${{ secrets.CLA_REPO_TOKEN }}
  ```


## Acknowledgements
The CLA was adapted from [Signal Messenger][signal-cla] and [intuitem][intuitem-cla].

The GitHub Action workflow primarily uses the [CLA Assistant GitHub Action][cla-gh-action].


<!-- links -->
[signal-cla]: https://signal.org/cla/
[intuitem-cla]: https://github.com/intuitem/ciso-assistant-community/blob/main/Contributor%20License%20Agreement.md
[cla-gh-action]: https://github.com/contributor-assistant/github-action
