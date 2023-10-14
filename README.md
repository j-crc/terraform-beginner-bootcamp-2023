# Terraform Beginner Bootcamp 2023

### Semantic versioning :mage:
This project is going to utilize semantic versioning for its branching. See more at the  [Semantic Versioning 2.0.0](https://semver.org/) website.

The general format will be MAJOR.MINOR.PATCH. Eg.: `1.0.1`.

- MAJOR version when you make **incompatible API changes**
- MINOR version when you **add functionality in a backward compatible manner**
- PATCH version when you **make backward compatible bug fixes**

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Install Terraform CLI :surfing_woman:

### Considerations about the Terraform CLI changes

The Terraform CLI installation instructions have changed due to gpg kering changes, therefore we needed to refer to the latest install CLI instructions via Terraform documentations and change the scripting for install.

[Terraform CLI Install tutorial](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)


### Refactoring into bash scripting

While addressing the Terraform CLI GPG deprecation problems, we observed that the bash script steps contained significantly more code so we decided to create a bash script to install the TF CLI.

This bash script is located here: 

Benefits:
- this will keep the Gitpod task file ([.gitpod.yml](./gitpod.yml))tidy;
- this allows us an easier time to debug and  manually execute the installation of the CLI;
- this will allow better portability for other projects that need to install the CLI.


### Considerations for Linux distribution

This project is build against Ubuntu. Please consider checking your Linux distribution and change accordingly to distribution needs.

[How to check OS version in Linux](https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/)

Example of checking OS version:
```
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```


### Shebang

A Shebang (pronounced sha-bang) tells the bash script what program will interpret the script. Eg. `#!/bin/bash`

Chat GPT recommended this format for bash: `#!/usr/bin/env bash`

- for portability (used in different distributions);
- will search the user's PATH for the bash executable.

[Wikipedia page](https://en.wikipedia.org/wiki/Shebang_(Unix))


#### Execution considerations

When executing the bash script, we can use the `./` shorthand notation to execute the bash script. Eg. `./bin/install_terraform_cli`.

If we are using a script in .gitpod.yml we need to point the script to a program to interpret it. Eg. `source ./bin/install_terraform_cli`.


##### Linux permissions considerations

In order to make our bash scripts executable we need to change the Linux permissions for the file to be executable at the user mode.

```sh
chmod u+x .bin/install_terraform_cli
```

Alternatively, we can use numeric notation:
```sh
chmod 744 .bin/install_terraform_cli
```
[Chmod - Wikipedia](https://en.wikipedia.org/wiki/Chmod)


### Gitpod lifecycle (before, init, command)

We need to be careful when using the `init` command because it will not return if we restart an existing workspace.

[Gitpod Workspaces Tasks Doc](https://www.gitpod.io/docs/configure/workspaces/tasks)
