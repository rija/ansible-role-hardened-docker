# How to contribute ?

* Start with our issue tracker[1] to check what are the open issues, and feel free to raise new issues if there isn't one yet for the subject you are looking for.
* Feel free to comment on existing open issues if you think it can help with the issue
* This is more like an integration project, make sure you understand what are the pieces and how they fit together
* When creating a Merge Request, **the only way we accept code/docs contributions**, keep it as small as possible and highly focused
* In a Pull Request, do mention which issue number it relates to
* When commenting on others' Merge Requests, use Conventional Comments[2]
* Reach out to the maintainer before trying to make complex changes

## Formatting your commits

* All commits should follow Conventional Commits[3] format
* commit messages should aim to answer the questions why?, and (for complex changes) how?
* Sometimes a one line commit message is enough to answer them, but when it's not, format your message as in the `.commit-template` document in this repository
* You can also configure `git` with that commit template: 

```
git config commit.template .commit-template
```

* if it took multiples trial-and-error kind of commits to implement a given unit of change, it's better to combine them together into one commit by squashing[4] them before making a pull request.
* Try to reference the issue number you are making changes to in your commit message, especially for the main commit that implements the issue, and the last commit before you are ready to make a pull request (see `.commit-template` on how to format that information, which is from Conventional Commits[3]).
* Whenever it makes sense, make use of "git trailers"[5].

## Testing your changes

If the change is a code change, make sure you are testing thoroughly: 

* Not just in your setup, but also on a fresh deployment of the project
* You should write automated tests for your code changes
* Make sure the existing automated tests still pass.

## Getting started

Ensure the tool dependencies are installed with Homebrew
```
brew bundle
```
You also need to create a python virtual env alongside the cloned repo:
```
python3 -m venv ../rhd_venv
source ../rhd_venv/bin/activate
```

Then, install python dependencies:
```
pip install -r requirements.txt
```
Next, install the Ansible dependencies
```
ansible-galaxy install -r requirements.yml
```

## Setting up the git hooks

Given that this project is YAML heavy, you should make sure you run `yamllint` and `ansible-lint` before committing any changes. That's what git hooks enables.

Additionally, in this project we use conventional commits as mentioned above.

So that nobody has to think about that every time, run the commands below to enable automated checks before a commit is made:
```
cd .git/hooks/
ln -s ../../.pre-commit pre-commit
ln -s ../../.commit-msg commit-msg
```

## Testing

This role uses `molecule` for integration testing. Run them as below:
```
molecule test
```


[1] https://gitlab.com/rmenage/ansible-role-hardened-docker/-/issues

[2] https://conventionalcomments.org/

[3] https://www.conventionalcommits.org/en/v1.0.0/

[4] https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History

[5] https://git-scm.com/docs/git-interpret-trailers 


