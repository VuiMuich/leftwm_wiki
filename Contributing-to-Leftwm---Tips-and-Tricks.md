 # Developing Tips and Tricks 
Developing on a window manager can be a bit tricky. It is hard to see the output of the executable you are building, if you introduce a bug it can be hard to revert. This page is meant to capture some of the tips and tricks the LeftWM team uses so if you want to contribute you can use them too. 

## Running more than one Xorg session.
You can switch back and forth between a different xorg session that is running something else like gnome by using `Ctrl+Alt+F[1-12]` 
1) boot into gnome
2) `Ctrl+Alt+F[1-12]` to get back to a terminal session
3) login and change the DISPLAY ENV to something like `export DISPLAY=:2`
4) boot LeftWM
Now you can switch back and forth between LeftWM and gnome

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