# macOS Installer for Jenkins LTS [](https://www.jenkins.io/download/lts/macos/#macos-installer-for-jenkins-lts)

[![homebrew](https://img.shields.io/homebrew/v/jenkins-lts)](https://formulae.brew.sh/formula/jenkins-lts)

Jenkins can be installed using the [Homebrew](https://brew.sh/) package manager. Homebrew formula: [jenkins-lts](https://formulae.brew.sh/formula/jenkins-lts)

This package is supported by a third party. It may not be as frequently updated as packages directly supported by the Jenkins project.

Sample commands:

- Install the latest LTS version: `brew install jenkins-lts`
- Start the Jenkins service: `brew services start jenkins-lts`
- Restart the Jenkins service: `brew services restart jenkins-lts`
- Update the Jenkins version: `brew upgrade jenkins-lts`

After starting the Jenkins service, browse to http://localhost:8080 and follow the instructions to complete the installation. Also see the external materials for installation guidelines. For example, [this blogpost](https://www.macminivault.com/installing-jenkins-on-macos/) describes the installation process.

## Post-installation setup wizard[](https://www.jenkins.io/doc/book/installing/macos/#setup-wizard)

After downloading, installing and running Jenkins using one of the procedures above (except for installation with Jenkins Operator), the post-installation setup wizard begins.

This setup wizard takes you through a few quick "one-off" steps to unlock Jenkins, customize it with plugins and create the first administrator user through which you can continue accessing Jenkins.

### [](https://www.jenkins.io/doc/book/installing/macos/#unlocking-jenkins)Unlocking Jenkins[](https://www.jenkins.io/doc/book/installing/macos/#unlocking-jenkins)

When you first access a new Jenkins controller, you are asked to unlock it using an automatically-generated password.

1. Browse to `http://localhost:8080` (or whichever port you configured for Jenkins when installing it) and wait until the **Unlock Jenkins** page appears.
    
    ![Unlock Jenkins page](https://www.jenkins.io/doc/book/resources/tutorials/setup-jenkins-01-unlock-jenkins-page.jpg)