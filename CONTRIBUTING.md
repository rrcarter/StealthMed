# Table of Contents

- [Prereqs](#prerequisites)
- [Access Tokens](#setup-your-personal-access-token-pat-for-github)
- [Getting ready to develop locally](#setup-your-personal-access-token-pat-for-github)
- [Contribution workflow](#contributing-to-stealthmed)
- [TLDR](#tldr)

# Prerequisites
### OS options
- MacOSx
- If you have windows, install Linux with WSL2
- If you still want to use Windows, please don't and set up WSL2 :)

#### macOS

1. From the terminal, install Xcode Command Line Tools: `xcode-select --install`
	- Confirm installation with `xcode-select -p`
	- You should see: /Library/Developer/CommandLineTools
2. Install the package manager Homebrew: [Homebrew installation instructions](https://brew.sh/)
3. Install UV. It handles everything for you Python related.
	- `brew install uv`
	- Tip: If brew wants to do a massive update for itself and its not the first time you're using it, you can skip this by running `HOMEBREW_NO_AUTO_UPDATE=1 brew install uv`
4. Install Python with uv
- You can get the exact version you want `uv python 3.12` or request the latest version with:  `uv python install --preview`

#### Windows 10 & WSL2 
1. CRITICAL:  Make sure virtualization is enabled first
	- Go to task manager
	- Check the processor (CPU) and you should see "Virtualization: enabled"
	- You  may need to bypass your BIOS and change the Intel VT-d in the options as available for virtualization (See steps: [WSL2 on Windows 10](https://kennisbank.meemoo.be/toolbox/installeer-wsl2-windows-subsystem-for-linux-2-op-windows-10)
2. Download [Windows Subsystem for Linux 2](https://learn.microsoft.com/en-us/windows/wsl/install)
3. Open command prompt / terminal or powershell as an Administrator
4. Paste in the command prompt terminal, `wsl --install` and press enter
5. Restart your computer (mandatory!)
6. Ubuntu will be installed by default. To access, type in the command prompt terminal
    `wsl -d ubuntu`
7. Verify with `wsl --list --verbose`

# Setup your Personal Access Token (PAT) for Github
You have to use a Personal Access Token (PAT) instead of a password. If you skip this step you will get error "Password authentication is not supported for Git operations" and can't send anything to the repository.

1. Go to your GitHub account settings: https://github.com/settings/profile
2. Developer Settings → Personal Access Tokens → Fine Grained Personal Access Tokens
	- Developer Settings are waaaaaaaaaaaaaaaay at the bottom of the list on the leftmost side with this icon: <>
	- Personal Access Tokens have a key icon
	
	**Why do you need this token?**
	These are repository-scoped tokens for using Git over HTTPS
	This slices and dices access permissions as opposed to a broad brush "access all the things"
	This is a standard zero trust approach and avoids giving too many privileges widely. 
3. Set up permissions
	- Select one repository: Stealthmed
4. Generate a new token and copy it
	-  The token starts with `ghp_`)
	- Save in a secure password manager. I recommend Bitwarden :)
	- Tip: If its your first time doing this, keep the window open. The token won't disappear. But then close it when you've successfully saved it somewhere secure AND successfully pushed to Github
	- If you lose it you will have to regenerate a new token.  Its not the end of the world but its annoying.
    
5. Next time Git asks for a password, use your GitHub username and paste the PAT in place of the password.
- Tip: If its your first time setting up Git and pushing to github, you need to configure your email and user name that are associated with your Github account
	- git config --global user.email "you@example.com" 
	- git config --global user.name "Your Name"

# Getting ready to develop Stealthmed locally
## 1. Fork the repository into your Github if you haven't already
- Tip: Look for the blue button that says Code <> for the URL
- You only need to do this the first time :)
## 2. Make sure git is initialized in this folder 
- You only need to do this the first time :)

# Contributing to Stealthmed
## Step 1. Your code must be up to date before you start
You must run the `git pull` command every time.
1. From the terminal, open the folder
	- `cd StealthMed`
2. Make sure you're up to date: SUPER CRITICAL
	- `git pull origin main`
- You will likely get this message:
	*branch            main       -> FETCH_HEAD*
    *Already up to date.*
## Step 2. You must check out a branch first
1. git checkout -b _branchname_ 
	- git checkout -b _fix_deprecation_ 
	- Tip: Give it a relevant name
	- Tip: Don't skip this step
## Step 3. Sync your python packages and check the build
Before you stage your changes (Step 4) you must sync/update your Python packages, then check your work by running the app locally

1. Update the python packages contained in the Stealthmed folder 
	`uv sync` 
2. Run streamlit with uv 
	`uv run streamlit run app.py`
	Hosted URL: https://stealthmedeye.streamlit.app/
	Paste this address in your local machine: http://localhost:8501/ 
    
## Step 4. Upload to Github
git add _specificfilename.filetype_
- git add _poc/app.py pyproject.toml uv.lock_

git commit -m "What I did"
- git commit -m "Made changes and stuff"

git remote set-url upstream https://YOURGITHUBNAME:YOURGITHUBTOKEN@github.com/YOURGITHUBNAME/StealthMed.git
- This part is really finicky but its why you needed to fork the repo as a contributor

git push upstream your-feature-branch
- git push upstream _uvmigration_ 

## Step 5. Log into Github.com to finish PR Request for approval
You're not done after you push to Github, one more step with writing the Pull request 
- Add "Fixes" at the top of the description box (not the title) of the Pull Request
- When you type "Fixes" you will see a drop-down menu with the issues numbered.  Select the relevant one.
- Then it should be automatically linked to the issue
- After submitting PR will be reviewed!

# TLDR
1. git pull origin main
2. git checkout -b _descriptive name_
3. `uv sync` → edit →  `uv run streamlit run app.py`
4. `git add` _filename_.filetype
   `git commit -m "whatidid_keepitshort"`
5. git push **upstream** _descriptive name_
6. GitHub Pull Request → in the top of the description link the Issue with "Fixes #..."
