# Custom SSH keys buildpack
This buildpack allows you to set multiple ssh keys **per repository**.

It is useful e.g. for GitHub deploy keys, which have to be unique per repository.

You have to set a comment for each private key with a repository name - `repo_owner/repo_name.git`.

You can change an existing key comment with this command:
```
ssh-keygen -c -C "repo_owner/repo_name.git" -f /path/to/private/key
```

## Installation

Put your private keys as Heroku environment variables with variable name in the following format:
```
GITHUB_DEPLOY_KEY_#
```
where `#` is index of a given key (e.g. 0, 1, 2...):

```
heroku config:set GITHUB_DEPLOY_KEY_0="-----BEGIN RSA PRIVATE KEY-----...."
heroku config:set GITHUB_DEPLOY_KEY_1="-----BEGIN RSA PRIVATE KEY-----...."
...
```

Then add the buildpack to your Heroku app. It should be set as the first (default) one:

```
heroku buildpacks:add https://github.com/baronapp/represent-custom-ssh-keys-buildpack.git -i 1
```
