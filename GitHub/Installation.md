# Git Installation Guide

## Installation

### Windows

1. Visit the official Git website for Windows: [Click Here](https://gitforwindows.org/)

2. Download the latest version of Git for Windows by clicking the "Download" button.

3. Run the downloaded installer file (`Git-XX.XX.X.X-64-bit.exe`, where `XX.XX.X.X` is the version number).

4. Follow the installation wizard, leaving the default options selected in most cases.

5. During installation, you'll have the option to choose an editor for Git. The default editor is usually "Vim," but you can select another editor if you prefer, such as "Nano" or "Notepad++."

6. When prompted, choose the default settings for adjusting your PATH environment and configuring line endings. Select "Use Git from the Windows Command Prompt" to have Git available in the Command Prompt.

7. Complete the installation.

8. To verify that Git is installed, open the Command Prompt and run the following command:
   
   ```bash
   git --version

### macOS

1. On macOS, you can install Git using the built-in package manager, Homebrew. If you don't have Homebrew installed, you can install it by following the instructions on the Homebrew [website](https://brew.sh/.) 

2. Once Homebrew is installed, open the Terminal.

3. To install Git, run the following command:
    
    ```bash
    brew install git

4. After the installation is complete, verify that Git is installed by running:

    ```bash
    git --version

### Linux (Redhat/Fedora)

1. Open a terminal.

2. Install Git using the package manager:

    ```bash
    sudo dnf install git 

3. After the installation is complete, verify that Git is installed by running:
    
    ```bash
    git --version


### Linux (Debian/Ubuntu)

1. Open a terminal.

2. Update your package lists to ensure you have the latest information about available packages:
    
    ```bash
    sudo apt update

3. Install Git with the following command:

    ```bash
    sudo apt install git

4. After the installation is complete, verify that Git is installed by running:

    ```bash
    git --version

Once Git is successfully installed on your system, you're ready to start using it for version control and collaboration on software projects. You can configure Git with your name and email using the git config command to associate your identity with your Git commits.

## Configuration

After installation, open a terminal (Command Prompt on Windows, or Terminal on macOS and Linux) and configure your Git identity:    
    
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"

Replace "Your Name" with your name and "your.email@example.com" with your email address. This information will be associated with your Git commits.