# Sharing your theme
1. [Add your theme to a github repository](https://docs.github.com/en/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line)
2. Fork the leftwm-community-themes repository
3. Clone your version of the leftwm-community-themes repository. Replace USERNAME

```BASH
git clone https://github.com/USERNAME/leftwm-community-themes.git
```
4. Enter the directory and add your theme repository as a sub-module. Replace USERNAME, NAME_OF_REPO, and NAME_OF_FOLDER (NAME_OF_FOLDER cannot have spaces)

```BASH
cd leftwm-community-themes
git submodule add -- https://github.com/USERNAME/NAME_OF_REPO NAME_OF_FOLDER
```

5. Modify known.toml adding your theme. Replace USERNAME, NAME_OF_REPO, and NAME_OF_THEME

```
[[theme]]
name = "NAME_OF_THEME"
repository = "https://github.com/USERNAME/NAME_OF_REPO/"
commit = "*"
version = "0.0.1"
leftwm_versions = "*"
```

6. Add, commit, and push the changes

```BASH
git add . && git commit -m "Adding my theme" && git push -u origin master
```

7. Create a pull request on github
8. Once your theme has been added you can delete your fork of leftwm-community-themes, this helps to keep the forks clean. (optional)