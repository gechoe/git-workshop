= Setting up an SSH key for Github

In 2020, Github changed their policies to [require token-based authentication](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/).

== Generate the token

First, if you do not have a `~/.ssh` directory, do

```
$ mkdir .ssh
$ chmod 600
```

Then run ssh-keygen.

```
$ cd .ssh
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

Specify a name for your key and (optionally) a password.
This will produce a private key and a public key (ends in `.pub`). 

On your Github account, under Settings/SSH and GPG keys, create a new SSH key and copy and paste the contents of the public key.

NOTES:
* Make sure that your keys are in the `~/.ssh` directory
* Make sure the `~/.ssh` directory has permissions TODO
* Make sure the private key has permissions TODO

== Clone the respository

Make sure that you clone the repository using the SSH url. 

== Local account setup

You may need to also set up the ssh-agent for you keys to work. Add the following lines to ~/.bashrc

```
# .bashrc
eval `ssh-agent -s`
ssh-add ~/.ssh/<private_keyname>
```
To test that your `.bashrc` works, run

```
$ source .bashrc
```

Check the hidden files in your home directory using `ls -a`. If you do not have a `.bash_profile`, add one with the following contents

```
# .bash_profile

# If .bash_profile exists, bash doesn't read .profile
if [[ -f ~/.profile ]]; then
  . ~/.profile
fi

# If the shell is interactive and .bashrc exists, get the aliases and functions
if [[ $- == *i* && -f ~/.bashrc ]]; then
    . ~/.bashrc
fi
```

References:

* https://docs.github.com/en/authentication/connecting-to-github-with-ssh
