# Setting up SSH keys

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/cb-geo/git-course/blob/master/Licence.md)

Tired of typing your password? ... Set up an SSH key.

First, check for existing SSH keys.

```bash
ls -al ~/.ssh                  # Check for existing SSH keys
```

You may see some defaults, such as:

* id_dsa.pub
* id_ecdsa.pub
* id_ed25519.pub
* id_rsa.pub

Second, decide if you want to _use an existing key_ or _generate a new SSH key_.

If you already have a key you wish to use (i.e., you created one already for
this purpose) you can skip ahead.

To generate a new key.

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@email.com"   # Generates a new key
```

Enter a file in which to save the key.

Enter a passphrase.

_Note: A passphrase is an additional level of security, such that if your system
is compromised you will still have this passphrase protecting your remotes. You
will need to enter this passphrase once per system login to authenticate before
using git._

Add the key to the ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/<newkeyname>
```

Add key to GitHub account by [this](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account) explainer.

You may also need to _switch from HTTPS to SSH_ for this to work, by doing the
following.

```bash
git remote -v                                                # Baseline
# You will see HTTPS or SSH
  # HTTPS looks like this https://github.com/<USER>/<REPO>.git
  # SSH looks like this git@github.com:<USER>/<REPO>.git
git remote set-url origin git@github.com:<USER>/<REPO>.git   # Switch to SSH
git remote -v                                                # Note the change
```

## Multiple SSH keys

When you have multiple SSH keys on the same machine, you can specify which SSH key to use for a given repo. In the local repo:

```bash
git config --add --local core.sshCommand 'ssh -i <<<PATH_TO_SSH_KEY>>>'
```
This will use the specified ssh key to fetch/pull/push. Note: This applies to your _local repository only_.
## Sources

[Why is Git always asking for my password?](https://help.github.com/en/articles/why-is-git-always-asking-for-my-password)
