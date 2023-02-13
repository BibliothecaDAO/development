# VS Code with Dev Container (Recommended)



## 1. Install Visual Studio Code
https://code.visualstudio.com/



## 2. Install Docker
https://docs.docker.com/get-docker/



## 3. Checkout BibliothecaForAdventurers Repository
1. Select the Clone Git Repository option on the VS Code homescreen and enter the URL for the BlibiothecaForAdventurers repo
```
https://github.com/BibliothecaForAdventurers/realms-contracts.git
```
2. After the repo is downloaded, VS Code will ask if you want to open the cloned repository. Select Open.
3. After opening the repo, VS Code will ask if you trust the author of the files. Select Yes.
---

## 4. Open Project in Dev Container
1. VS Code will detect the presence of the .devcontainer config and ask if you want to open the project in the dev container. Select "Reopen in Container"
2. VS Code will reload and the project will now be open within a docker container. The container will automatically run a setup script which will walk you through importing an account from argentx or creating a new one using nile.
3. Once you complete the setup wizard, source in bashrc in your terminal (only neccessary first time but this is idempotent so no harm in running in more than once)
```bash
source ~/.bashrc
```
---


## 5. Setup Git

The development container loads settings and the repository information on your local computer but cannot read your GitHub login credentials from your local computer.

Instead, you can use the [Github CLI](https://cli.github.com/) to auth from your dev container:

1. Download the [Github CLI](https://github.com/cli/cli/blob/trunk/docs/install_linux.md#debian-ubuntu-linux-raspberry-pi-os-apt).
2. Visit the [Github Tokens page](https://github.com/settings/tokens) and click `Generate New Token` to create a new token that will be used in your dev container. Make sure to save it somewhere as the token is only visible upon creation.
3. With the container loaded, open the dev container terminal in vscode.
4. Run `gh auth login` and follow the steps, pasting in your new access token when asked.
---
---
## ⚠️ For those running OSX ARM chips
Docker performance on ARM chips is currently poor so we recommend running without a container until these perf issues are resolved:
1. Pull down the repository
2. Install homebrew: https://brew.sh/
3. Install gmp: `brew install gmp`
4. Install dependencies: `pip3 install -r ./requirements.txt`
5. Install realms cli: `pip3 install ./realms_cli`


If you have further questions about the development workflow, please ask in [#builders-chat in the Realms Discord](https://discord.gg/yP4BCbRjUs).