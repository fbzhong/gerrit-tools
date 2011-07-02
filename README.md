# gerrit Tools

A few scripts to make code review via [Gerrit Code Review](http://gerrit.googlecode.com) easier for developers.
They are improved and maintained to fit the needs of the [TYPO3](http://typo3.org) review workflow.

## gerrit-cherry-pick

This is a script that allows you to cherry-pick a particular patch from Gerrit, so that it can be reviewed easily. It comes with Gerrit, but is included here because Gerrit 2.1.1.1 does not yet contain support for the `--latest` option.

## gerrit-setup

Gerrit-setup will attempt to convert a repository cloned from github to use Gerrit as the origin instead.

## git-review

Git-review is a wrapper script to make creating, reviewing, and approving Gerrit changes very simple. In the simplest case, you can have an entire Git workflow that looks like this for people creating a new changeset:

    git review push

And looks like this for people reviewing someone else's changeset:

    git review 123
    rake && git review approve
    git review reset

You may find it helpful to alias `gr` to `git review`.

## Installation

You can either install it locally for your user only or you can install it globally for all users.

First cd into the downloaded directoy into the subdir bin:

	cd gerrit-tools/bin/

### Local install

If the directory ~/bin does not exist, create it in your in your home path:

	if [[ ! -d $HOME/bin ]]; then mkdir $HOME/bin; fi

Now check if your $PATH variable already contains that path or add it do ~/.bashrc:

	if [[ ! $PATH =~ $HOME/bin ]]; then echo -e "\nexport PATH=\$PATH:\$HOME/bin" >> $HOME/.bashrc; source $HOME/.bashrc; fi

Finally symlink all files (you need to be in gerrit-tools/bin/) and make them executable:

	for i in *; do ln -s `pwd`/$i $HOME/bin/$i; chmod +x $i; done

Check if all worked by running:

	cd ; git review

It will print "git-review can only be run from a git repository." in red (unless your home directory is already a git repository ;) )

### Global install

First become root:

	sudo su

Then you can either create the symlinks like above (make sure to be in gerrit-tools bin) or you can cp the files:

    for i in *; do ln -s `pwd`/$i /bin/$i; chmod +x $i; done

or

	for i in *; do cp -u $i /bin/; chmod +x /bin/$i; done

Now quit root:

	exit

Finally check if it worked by running:

	cd ; git review

It will print "git-review can only be run from a git repository." in red (unless your home directory is already a git   repository ;) )

## Contributing

Feel free to fork and send a pull request if you think you've improved anything.
