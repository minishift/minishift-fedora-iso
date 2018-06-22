<a name="creating-a-minishift-fedora-iso"></a>
# Minishift Fedora ISO

This repository contains all the instructions and code to build a Live ISO based on Fedora
which can be used by [minishift](https://github.com/minishift/minishift) as an alternative to
the CentOS ISO.

----

<!-- MarkdownTOC -->

- [Building the Fedora ISO](#building-the-fedora-iso)
	- [On Fedora](#on-fedora)
		- [Prerequisites](#prerequisites)
		- [Building the ISO](#building-the-iso)
	- [On hosts _other than Fedora_ \(OS X, Windows, CentOS ...\)](#non-fedora-hosts)
		- [Prerequisites](#prerequisites-1)
		- [Building the ISO](#building-the-iso-1)
  - [Manual release](#manual-release)
- [Further reading](#further-reading)
- [Community](#community)

<!-- /MarkdownTOC -->

----

<a name="building-the-fedora-iso"></a>
## Building the Fedora ISO

The following contains instructions on how to build the Fedora based ISO.
If you are able to install [livecd-tools](https://github.com/rhinstaller/livecd-tools)
directly on your machine, you can use the [Fedora](#on-fedora) instructions.

If you don't have _livecd-tools or using different linux distro other than Fedora_, follow the
[hosts other than Fedora](#non-fedora-hosts) instructions.

<a name="on-fedora"></a>
### On Fedora

<a name="prerequisites"></a>
#### Prerequisites
* Update your system before start and if there is kernel update then reboot your system to activate latest kernel.

        $ dnf update -y

* [Install livecd-tools](https://github.com/rhinstaller/livecd-tools)

  Note: We use to have docker installed on system to get selinux context, [check bugzilla](https://bugzilla.redhat.com/show_bug.cgi?id=1303565)

        $ dnf install -y livecd-tools docker


<a name="building-the-iso"></a>
#### Building the ISO

```
$ git clone https://github.com/minishift/minishift-fedora-iso.git
$ cd minishift-fedora-iso
$ make
```

<a name="non-fedora-hosts"></a>
### On hosts _other than Fedora_ (macOS, Windows, CentOS ...)

<a name="prerequisites-1"></a>
#### Prerequisites

* [Vagrant](https://www.vagrantup.com/)
* [vagrant-sshfs](https://github.com/dustymabe/vagrant-sshfs)

        $ vagrant plugin install vagrant-sshfs

<a name="building-the-iso-1"></a>
#### Building the ISO

```
$ git clone https://github.com/minishift/minishift-fedora-iso.git
$ cd minishift-fedora-iso
$ vagrant up
$ vagrant ssh
$ cd <path to minishift-fedora-iso directory on the VM>/minishift-fedora-iso
$ make
```

<a name="manual-release"></a>
### Manual release

The manual release includes following steps:

- Assemble all the meaningful changes since the last release to create release notes.
- Bump the `VERSION` variable in the Makefile.
- Before you execute below command be sure to have a [Github personal access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use) defined in your environment as `GITHUB_ACCESS_TOKEN`.
- Run following command to perform release:

  ```shell
  $ make release
  ```

#### Build ISO

Setup your build environment by following the instructions provided in [Building the Fedora ISO](#building-the-fedora-iso) section as per your preferred OS.

Note: Building ISO might require you to have Vagrant environment if you are not using host other than Fedora.

#### Run the tests

Once the ISO is built from above step, use following command to run tests:

```
$ make test
```

Note: If you are using the Vagrant environment, you need to exit from it and come back to host to run the above command.

This command will fetch the latest [minishift](http://github/minishift/minishift) binary and run the [tests](tests/test.sh).

<a name="further-reading"></a>
## Further reading

Once you are able to build the ISO, you are most likely interested to modify the
image itself. To do so you have to get familiar with
[pykickstart](https://github.com/rhinstaller/pykickstart/blob/master/docs/kickstart-docs.rst).

<a name="community"></a>
## Community

You can reach the Minishift community by:

- Signing up to our [mailing list](https://lists.minishift.io/admin/lists/minishift.lists.minishift.io)

- Joining the `#minishift` channel on [Freenode IRC](https://freenode.net/)
