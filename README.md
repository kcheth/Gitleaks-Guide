# Gitleaks
As DevOps engineers, we recognize the significance of maintaining the security and integrity of our code repositories. A crucial aspect of securing a codebase involves ensuring that sensitive information, including passwords, API keys, tokens, private keys, or any suspicious file names, is not inadvertently committed.

## What is Gitleaks?
Gitleaks is an open-source tool designed to detect and prevent secret passwords, API keys, tokens, private keys, and more in your code repository. It scans your code repository for sensitive information that may have been accidentally committed. These secrets could include passwords, API keys, tokens, private keys, suspicious file names, or file extensions like id_rsa, .pem, and htpasswd.

## How does Gitleaks Work?
Gitleaks functions by inspecting your code repository for files that conform to predefined patterns. These patterns are crafted to identify different types of sensitive information like passwords, secrets, key files, and more. Upon discovering a match, Gitleaks issues an alert, enabling you to take necessary measures to eliminate the identified sensitive information.

## Getting Started
### To install Gitleaks on a Linux machine, you can follow these steps:
1. Download Gitleaks:
   1. Obtain the Gitleaks binary for Linux from its GitHub [releases page](https://github.com/gitleaks/gitleaks/releases)
   2. Ensure to select the version that matches your architecture (e.g., Linux x64).
`wget <https://github.com/gitleaks/gitleaks/releases/download/v8.18.2/gitleaks_8.18.2_linux_x64.tar.gz>`
   3. At the time of documenting this installation, the Gitleaks version was V8.18.2.
2. Extract the Tarball:
   1. After completing the download, extract the contents of the tarball.
`tar xvf gitleaks_8.18.2_linux_x64.tar.gz`
3. Grant Executable Permission:
   1. Provide executable permission to the extracted file.
`chmod +x gitleaks`
4. Move the Binary:
   1. Move the extracted Gitleaks binary to a directory in your system's PATH for global accessibility.
`sudo mv gitleaks /usr/local/bin/`
5. Verify Installation:
   1. Gitleaks doesn't support the --version flag for displaying the version. You can confirm a successful Gitleaks installation by running:
`gitleaks version`
You should see the version number displayed, confirming that Gitleaks is installed.

![image](https://github.com/kcheth/Gitleaks-Guide/assets/106922418/fa250eba-6835-4650-98ea-31f21cd81536)

Use the below command to know more about Gitleaks

That's it! Gitleaks should now be installed on your Linux machine. You can start using it to scan Git repositories for sensitive information and credentials by running the  `gitleaks` command followed by the desired options and repository path.

There are two main commands that you need to be familiar with when working with Gitleaks: `detect` and `protect`

`detect` : This command scans code repositories for sensitive information like passwords and API keys, enabling early detection of vulnerabilities in both developer machines and CI environments.

 `protect` : This command helps undo the last commit, aiding in the removal of detected sensitive data from the commit history, ensuring a secure codebase by addressing vulnerabilities early in development.

 ### Scenarios

 1. Verifying Secrets in the Git Source Code [Repository](https://github.com/kcheth/Shopping-cart)
    a. Open the terminal and navigate to the source code repository you want to detect secrets from using the `cd <path-to-your-source-code-repository>` command.
    b. Run the `gitleaks detect .` command, and it will provide you with the count of leaks in your Git repository.
    c. Run the `gitleaks detect -v` command to find the details of secrets committed in your git repository.




