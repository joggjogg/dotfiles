# Dotfiles
## Steps to bootstrap a new Mac
1. Install Apple's command line tools, which are prerequisites for Git and Homebrew.

    ```
    $ xcode-select -- install
    ```

2. Generate and add a new SSH key
    - First generate a new key with the Github generated email adress.

        ```
        $ ssh-keygen -t ed25519 -C "45901428+joggjogg@users.noreply.github.com"
        ```
    - Start the ssh-agent
        ```
        $ eval "$(ssh-agent -s)"
        ```
    - Open your ~/.ssh/config file, then modify the file to contain the following lines. If your SSH key file has a different name or path than the example code, modify the filename or path to match your current setup.
        ```
        Host *
            AddKeysToAgent yes
            UseKeychain yes
            IdentityFile ~/.ssh/id_ed25519
        ```
    - Add your SSH private key to the ssh-agent and store your passphrase in the keychain. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_ed25519 in the command with the name of your private key file.
        ```
        $ ssh-add -K ~/.ssh/id_ed25519
        ```
    - Authenticate to the GitHub CLI.
        ```
        $ gh auth login
        ```
    - Add the SSH key to the GitHub account.
        ```
        $ gh ssh-key add ~/.ssh/id_ed25519.pub --title "MacBook Pro"
        ```
3. Clone repo into hidden directory.
    ```
    $ git clone git@github.com:joggjogg/dotfiles.git ~/.dotfiles
    ```
4. Create symlinks to Home directory
    ```
    $ ln -s ~/.dotfiles/.zshrc ~/.zshrc
    $ ln -s ~/.dotfiles/.gitconfig ~/.gitconfig
    ```
5. Install Homebrew and Homebrew packages
    ```
    $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    $ brew bundle --file ~/.dotfiles/Brewfile
    ```