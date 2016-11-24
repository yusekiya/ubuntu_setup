Ansible Role: dev_env
=========

Establish development environment.
This role includes following tasks.

- Add user to docker group (tags: docker, need_root)
- Create directories (tags: basic_dirs)
- Install newer version of Git (tags: need_root)
- Clone user's dotfiles (tags: dotfiles, git)
- Install anaconda/miniconda (tags: python)
- Install packages through apt-get (tags: apt, need_root)
- Clone git repos (tags: git)
- Install and build fzf (tags: fzf, apt, git, need_root)
- Install and build tmux (tags: tmux, apt, git, need_root)
- Install and build tig (tags: tig, apt, git, need_root)
- Install nodebrew (tags: nodebrew)

The need_root tag is added to tasks which requires root privilege.

Requirements
------------

- git

Role Variables
--------------

Available variables are listed below.

[REQUIRED] User account name for development environement which has been created already.

``` yaml
dev_env_user: 'username'
```

List of directories preferred to be made in advance.

``` yaml
dev_env_basic_dirs:
  - {path: '~/Downloads'}
  - {path: '~/.nodebrew/src'}
  - {path: '~/bin'}
  - {path: '~/repos'}
  - {path: '~/scratch'}
  - {path: '~/share'}
  - {path: '~/usr/bin'}
  - {path: '~/usr/include'}
  - {path: '~/usr/lib'}
  - {path: '~/usr/lib/python3/site-packages'}
  - {path: '~/usr/share'}
  - {path: '~/usr/src'}
```

Information about your dotfiles.

``` yaml
dev_env_dotfiles:
  repository: 'https://github.com/USER/dotfiles.git'
  dest: '~/dotfiles'
  symlink_script: 'bash setup.sh -f'
```

`symlink_script` will be executed in the directory `dest` after the task changed.

Information for anaconda.

``` yaml
dev_env_anaconda:
  prefix: '~/anaconda3'
  src: 'https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh'
  dest: '~/Downloads/Ananconda_installer.sh'
```

List of packages to be installed through apt command.

``` yaml
dev_env_packages:
  - {name: git}
  - {name: build-essential}
  - {name: htop}
  - {name: pkg-config}
  - {name: tree}
  - {name: autoconf}
  - {name: automake}
  - {name: bash-completion}
  - {name: cmake}
  - {name: colordiff}
  - {name: exuberant-ctags}
  - {name: direnv}
  - {name: nkf}
  - {name: pandoc}
  - {name: clang}
  - {name: libncursesw5}
  - {name: libncursesw5-dev}
  - {name: libncurses5-dev}
  - {name: libevent-dev}
```

List of git repositories to be cloned.

``` yaml
dev_env_git_repos:
  - {name: tpm,
     repo: "https://github.com/tmux-plugins/tpm.git",
     dest: "~/.tmux/plugins/tpm" }
  # - {name: solarized,
  #    repo: "https://github.com/altercation/solarized.git",
  #    dest: "~/repos/solarized" }
  - {name: dircolors-solarized,
     repo: "https://github.com/seebi/dircolors-solarized.git",
     dest: "~/repos/dircolors-solarized" }
  - {name: enhancd,
     repo: "https://github.com/b4b4r07/enhancd.git",
     dest: "~/repos/enhancd" }
```

Information for nodebrew.

``` yaml
dev_env_nodebrew:
  executable_path: '~/.nodebrew/nodebrew'
  src: 'https://raw.githubusercontent.com/hokaccha/nodebrew/master/nodebrew'
  dest: '~/Downloads/nodebrew'
```


Dependencies
------------

None.

Example Playbook
----------------

``` yaml
- hosts: all
  vars_files:
    - vars/main.yml
  roles:
    - {role: dev_env, when: dev_env_user is defined, become: yes, become_user: '{{dev_env_user}}'}
```


License
-------

MIT

