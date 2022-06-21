# Ansible Lint for GitHub Actions

This action allows you to run `ansible-lint` with no additional options.

The following versions are available in the main branch:

```
ansible version: 5.5.0
ansible-lint version: 6.0.2
```

The following versions are available in the releases:

| Version | ansible-lint | ansible |
|---------|--------------|---------|
| v2.0.0  | 6.0.2        | 5.5.0   |
| v1.2.0  | 5.4.0        | 5.5.0   |
| v1.1.0  | 5.4.0        | 5.4.0   |
| v1.0.0  | 5.3.2        | 5.2.0   |

The versions of ansible and ansible-lint are updated regularly.

If there is a change of the major version at ansible-lint or ansible
then the major version is also incremented here.

If the major versions of ansible-lint and ansible both change at the
same time, our major version is only incremented once.

Examples:

* When ansible-lint jumps from 5.4.0 to 6.0.2 then our major version changes as well.
* When ansible-lint jumps from 5.3.2 to 5.4.0 then our major version does not change.
* When ansible jumps from 5.5.0 to 6.0.0 then our major version version changes as well.
* When ansible jumps from 5.4.0 to 5.5.0 then our major version does not change.

## Usage

To use the action simply create an `check-ansible-syntax.yml` file
(or choose custom `*.yml` name) in the `.github/workflows/` directory.

For example:

```yaml
name: Check ansible syntax  # feel free to pick your own name

on: [push, pull_request]

jobs:
  check-ansible-syntax:

    runs-on: ubuntu-latest

    steps:
    # Important: This sets up your GITHUB_WORKSPACE environment variable
    - uses: actions/checkout@v2

    - name: Lint Ansible Playbook
      # replace "main" with any valid ref
      uses: osism/ansible-lint-action@main
      with:
        # [required]
        # Paths to ansible files (i.e., playbooks, tasks, handlers etc..)
        # or valid Ansible directories according to the Ansible role
        # directory structure.
        # If you want to lint multiple ansible files, use the following syntax
        # targets: |
        #   playbook_1.yml
        #   playbook_2.yml
        targets: ""
        # [optional]
        # Arguments to override a package and its version to be set explicitly.
        # Must follow the example syntax.
        override-deps: |
          ansible==5.2.0
          ansible-lint==5.3.2
        # [optional]
        # Arguments to be passed to the ansible-lint

        # Options:
        #   -q                    quieter, although not silent output
        #   -p                    parseable output in the format of pep8
        #   --parseable-severity  parseable output including severity of rule
        #   -r RULESDIR           specify one or more rules directories using one or
        #                         more -r arguments. Any -r flags override the default
        #                         rules in ansiblelint/rules, unless -R is also used.
        #   -R                    Use default rules in ansiblelint/rules in addition to
        #                         any extra
        #                         rules directories specified with -r. There is no need
        #                         to specify this if no -r flags are used
        #   -t TAGS               only check rules whose id/tags match these values
        #   -x SKIP_LIST          only check rules whose id/tags do not match these
        #                         values
        #   --nocolor             disable colored output
        #   --exclude=EXCLUDE_PATHS
        #                         path to directories or files to skip. This option is
        #                         repeatable.
        #   -c C                  Specify configuration file to use. Defaults to ".ansible-lint"
        args: ""

```

## License

The Dockerfile and associated scripts and documentation in this project are released under
the [MIT](license).

## Credits

This fork is based on [ansible/ansible-lint-action](https://github.com/osism/ansible-lint-action).

The initial GitHub action has been created by [Stefan Stölzle](https://github.com/stoe) at
[stoe/actions](https://github.com/stoe/actions).
