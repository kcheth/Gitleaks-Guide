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

 1. **Verifying Secrets in the Git Source Code [Repository](https://github.com/kcheth/Shopping-cart)**
    1. Open the terminal and navigate to the source code repository you want to detect secrets from using the `cd <path-to-your-source-code-repository>` command.
    2. Run the `gitleaks detect .` command, and it will provide you with the count of leaks in your Git repository.
    3. Run the `gitleaks detect -v` command to find the details of secrets committed in your git repository.
```
[ec2-user@ip-172-31-17-43 ~]$ ls
LICENSE  README.md  Shopping-cart  calcwebapp  gitleaks_8.18.2_linux_x64.tar.gz  simple-webapp-flask
[ec2-user@ip-172-31-17-43 ~]$ cd Shopping-cart/
[ec2-user@ip-172-31-17-43 Shopping-cart]$ gitleaks detect

    ○
    │╲
    │ ○
    ○ ░
    ░    gitleaks

11:30AM INF 25 commits scanned.
11:30AM INF scan completed in 69ms
11:30AM WRN leaks found: 3
[ec2-user@ip-172-31-17-43 Shopping-cart]$ gitleaks detect -v

    ○
    │╲
    │ ○
    ○ ░
    ░    gitleaks

Finding:     -- password in plaintext: "password"
INSERT INTO USER (u...
Secret:      "password"
RuleID:      hashicorp-tf-password
Entropy:     2.921928
File:        src/main/resources/sql/import-h2.sql
Line:        1
Commit:      0553a75ebeb005e15f47f674400b0177d00af278
Author:      Jaiswal
Email:       adijaiswal@deloitte.com
Date:        2023-05-06T18:51:52Z
Fingerprint: 0553a75ebeb005e15f47f674400b0177d00af278:src/main/resources/sql/import-h2.sql:hashicorp-tf-password:1

Finding:     -- password in plaintext: "password"
INSERT INTO USER (u...
Secret:      "password"
RuleID:      hashicorp-tf-password
Entropy:     2.921928
File:        src/main/resources/sql/import-h2.sql
Line:        6
Commit:      0553a75ebeb005e15f47f674400b0177d00af278
Author:      Jaiswal
Email:       adijaiswal@deloitte.com
Date:        2023-05-06T18:51:52Z
Fingerprint: 0553a75ebeb005e15f47f674400b0177d00af278:src/main/resources/sql/import-h2.sql:hashicorp-tf-password:6

Finding:     -- password in plaintext: "password"
INSERT INTO USER (u...
Secret:      "password"
RuleID:      hashicorp-tf-password
Entropy:     2.921928
File:        src/main/resources/sql/import-h2.sql
Line:        10
Commit:      0553a75ebeb005e15f47f674400b0177d00af278
Author:      Jaiswal
Email:       adijaiswal@deloitte.com
Date:        2023-05-06T18:51:52Z
Fingerprint: 0553a75ebeb005e15f47f674400b0177d00af278:src/main/resources/sql/import-h2.sql:hashicorp-tf-password:10

11:31AM INF 25 commits scanned.
11:31AM INF scan completed in 71.2ms
11:31AM WRN leaks found: 3
```
We seem to have a hard-coded secret in our code. Additionally, you can export the relevant data to a file using the `--report-path` flag. The complete command would be: 

`gitleaks detect --report-path /path/to/your/report.txt`

```
[ec2-user@ip-172-31-17-43 Shopping-cart]$ gitleaks detect --report-path /home/ec2-user/Shopping-cart/report.txt

    ○
    │╲
    │ ○
    ○ ░
    ░    gitleaks

11:44AM INF 25 commits scanned.
11:44AM INF scan completed in 69.3ms
11:44AM WRN leaks found: 3
[ec2-user@ip-172-31-17-43 Shopping-cart]$ ls
Dockerfile  Jenkinsfile  LICENSE  README.md report.txt deploymentservice.yml  docker  pom.xml  scripts  src
```
You can use a `cat` command to see the contents of `report.txt` file

![image](https://github.com/kcheth/Gitleaks-Guide/assets/106922418/3e0cfd15-e5ff-4a26-860d-9e3ac74efe4b)

In the output, you'll find the secret content, commit ID, and other relevant information.

2. **Preventing Accidental Secret Commits in Your Git Source Code Repository**
   1. Preventing accidental leaks in your repository is more effective than cleaning up later.
   2. Execute the command `gitleaks protect .` to identify any secrets in your code repository changes.
   3. Execute the command `gitleaks protect -v` to view detailed information about secrets committed in your Git repository.
   4. Remove any detected secrets.
   5. Use the command `gitleaks protect --staged` to identify secrets in the staging area of your Git repository.
   6. For detailed information on staging area secrets, execute `gitleaks protect --staged -v`

3. **Creating a baseline**
   
When scanning large repositories or repositories with a long history, it can be convenient to use a baseline. When using a baseline, gitleaks will ignore any old findings that are present in the baseline. A baseline can be any gitleaks report. To create a gitleaks report, run gitleaks with the `--report-path` parameter.

`gitleaks detect --report-path gitleaks-report.json` # This will save the report in a file called gitleaks-report.json

Once as baseline is created it can be applied when running the detect command again:

`gitleaks detect --baseline-path gitleaks-report.json --report-path findings.json`

After running the detect command with the `--baseline-path` parameter, report output (findings.json) will only contain new issues.

5. **Verify Findings**
You can verify a finding found by gitleaks using a `git log` command. Example output:
```
{
  "Description": "Identified a HashiCorp Terraform password field, risking unauthorized infrastructure configuration and security breaches.",
  "StartLine": 10,
  "EndLine": 11,
  "StartColumn": 5,
  "EndColumn": 1,
  "Match": "password in plaintext: \"password\"",
  "Secret": "\"password\"",
  "File": "src/main/resources/sql/import-h2.sql",
  "SymlinkFile": "",
  "Commit": "0553a75ebeb005e15f47f674400b0177d00af278",
  "Entropy": 2.9219282,
  "Author": "Jaiswal",
  "Email": "adijaiswal@deloitte.com",
  "Date": "2023-05-06T18:51:52Z",
  "Message": "Added source code",
  "Tags": [],
  "RuleID": "hashicorp-tf-password",
  "Fingerprint": "0553a75ebeb005e15f47f674400b0177d00af278:src/main/resources/sql/import-h2.sql:hashicorp-tf-password:10"
 }
```
We can use the following format to verify the leak:

`git log -L {StartLine,EndLine}:{File} {Commit}`

So in this example it would look like:

`git log -L 10,11:src/main/resources/sql/import-h2.sql 0553a75ebeb005e15f47f674400b0177d00af278`
















