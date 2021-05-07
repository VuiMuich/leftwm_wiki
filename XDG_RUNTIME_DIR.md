LeftWM requires that `$XDG_RUNTIME_DIR` is set in the environment as it uses this directory.

`$XDG_RUNTIME_DIR` is the standard directory for a user's runtime files.<br>
Most users will more than likely not need this page as they use systemd or elogind.<br>
However, some people (myself included) don't want that software anywhere near their machines.

So to get around that, you can set it yourself:

```bash
export XDG_RUNTIME_DIR=/tmp/${UID}-runtime-dir
mkdir "${XDG_RUNTIME_DIR}"
chmod 0700 "${XDG_RUNTIME_DIR}"
```

Explanations:
- `${UID}` is replaced with the ID of your user
- `chmod 0700` means that the user can read, write, and execute things in that directory

And to automatically have it set, place this in your `$HOME/.bash_profile`:

```bash
if test -z "${XDG_RUNTIME_DIR}"; then
    export XDG_RUNTIME_DIR=/tmp/${UID}-runtime-dir
    if ! test -d "${XDG_RUNTIME_DIR}"; then
        mkdir "${XDG_RUNTIME_DIR}"
        chmod 0700 "${XDG_RUNTIME_DIR}"
    fi
fi
```

Explanations:
- `$HOME/.bash_profile`

The reason for this, is that `.bash_profile` is the first file read by bash in an interactive login shell<br>
meaning that once you've logged in from a tty it will be evaluated. This is why it's the best place to stick<br>
environmental variables as all shells spawned after it will inherit the environmental variables.

- `test -z` checks if the file does not exist
- `! test -d` checks if the file is not a directory

References: 
- https://wiki.gentoo.org/wiki/Sway#Executing_sway
- https://www.baeldung.com/linux/bashrc-vs-bash-profile-vs-profile
- https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html