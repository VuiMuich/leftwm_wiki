 # Developing Tips and Tricks 
Developing on a window manager can be a bit tricky. It is hard to see the output of the executable you are building, if you introduce a bug it can be hard to revert. This page is meant to capture some of the tips and tricks the LeftWM team uses so if you want to contribute you can use them too. 

## Running more than one Xorg session.
You can switch back and forth between a different xorg session that is running something else like gnome by using `Ctrl+Alt+F[1-12]` 
1) boot into gnome
2) `Ctrl+Alt+F[1-12]` to get back to a terminal session
3) login and change the DISPLAY ENV to something like `export DISPLAY=:2`
4) boot LeftWM
Now you can switch back and forth between LeftWM and gnome

## Using Xephyr instead of switching tty
if you prefer not to switch tty you can use a tool called Xephyr. This tool allows you to run an embedded X session, aka a wm in a window. To use it first run `Xephyr -br -ac -noreset -screen 1920x1200 :1`. replace the value after `-screen` with the resolution you want the session to run in, if you are using a resolution bigger then the window it is contained it it will crop of anything that doesnt fit. If you want it to close after you exit out of the window manager running in it, remove the `-noreset`. To run leftwm in this X session run `DISPLAY=:1 leftwm` in a termial. if you changed the `:1` in the `Xephyr` command also replace it in the other command.

## Environment Functions  
To make your life easier once your done coding, adding this function
```
checkleft() {
        if cargo fmt ; then
          if cargo test; then
            if cargo clippy --all-targets --all-features ; then
                if git add -A $1 ; then
                    if git status ; then
                        git commit -S -m "$2"
                    else
                        echo "Status failed"
                     fi
                 else
                     echo "Add failed"
                fi
            else
                echo "Clippy failed"
            fi
          else
            echo "Test failed"
          fi
         else
                echo "FMT failed"
          fi
}
```
to your ```~/.bashrc``` and running it will automatically run all the cargo checks and commit the specified files to git. It assumes you have a gpg-key, remove ```-S ``` flag from git commit if not.
Example usage:
```
# Example, adds all of src/, Cargo.toml, and Cargo.lock to be committed.
# You can pass anything that would go to git add -A 
checkleft 'src/ Cargo.toml Cargo.lock' 'Commit message'
```

Note for extended clippy lints use:
```
cargo clippy -- -W clippy::pedantic -A clippy::must_use_candidate -A clippy::cast_precision_loss -A clippy::cast_possible_truncation -A clippy::cast_possible_wrap -A clippy::cast_sign_loss -A clippy::mut_mut

```