---
tags: setup, environment, bash, kids
languages: ruby
---

## Environment Setup for Students Using Mac Computers
Let's go ahead and get your environment setup. Don't worry too much about the how's and why's of all of this. Our goal is to get you up and running as fast as possible!

##1. Download and Install Google Chrome

https://www.google.com/intl/en/chrome/browser/

##2. Make Sure You Have Xcode

Type `xcode-select --install` into your terminal. If a window pops up telling you to install Xcode agree to the terms and follow the instructions.

##3. Download Homebrew 

[Homebrew](http://brew.sh/.). is an awesome package manager, and makes downloading lots of software really easy. Download Homebrew by entering 
```
  ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Once downloading is complete, you'll want to enter `brew doctor` to make sure you don't have any conflicts.

##4. Get the Most Updated Version of Git.

Update your version of git by entering `brew install git`

If you have issues with Homebrew, You can try reinstalling it with this command:
```
\curl -L https://gist.github.com/mxcl/1173223/raw/a833ba44e7be8428d877e58640720ff43c59dbad/uninstall_homebrew.sh | bash
```

##5. Set Up a Sublime Sym Link

This means that instead of typing `open` to open files, you can type `subl` and it will open that file in Sublime Text. Programmers love shortcuts and this one is super helpful.

#### For Sublime Text 2
```
ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" /usr/local/bin
```

#### For Sublime Text 3
```
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin
```

##6. Set Up Your `.bash_profile`.

We'll spend a lot more time in terminal today, but it's helpful if your `.bash_profile` looks just like mine. We're going to open terminal and enter the following commands:

`cd ~`

`ls -lah`

This command should bring up a list of all the files on your computer, including secret hidden files that begin with a `.`. We're looking for a file called `.bash_profile`. 
If it's there go ahead and enter `open .bash_profile`. 
It it's not there, enter `touch .bash_profile` followed by `open .bash_profile`.

We're going to use the standard for ours. Copy and paste this code below into your `.bash_profile` and save it. 

```bash
# Configuring Our Prompt
# ======================

  # This function is called in your prompt to output your active git branch.
  function parse_git_branch {
    git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
  }

  # This function builds your prompt. It is called below
  function prompt {
    # Define some local colors
    local         RED="\[\033[0;31m\]" # This syntax is some weird bash color thing I never
    local   LIGHT_RED="\[\033[1;31m\]" # really understood
    local        CHAR="♥"

    # Here is where we actually export the PS1 Variable which stores the text for your prompt
    export PS1="\[\e]2;\u@\h\a[\[\e[37;44;1m\]\t\[\e[0m\]]$RED\$(parse_git_branch) \[\e[32m\]\W\[\e[0m\]\n\[\e[0;31m\]$CHAR \[\e[0m\]"
      PS2='> '
      PS4='+ '
    }

# Environment Variables
# =====================
  # Library Paths
  # These variables tell your shell where they can find certain
  # required libraries so other programs can reliably call the variable name
  # instead of a hardcoded path.

    # NODE_PATH
    export NODE_PATH="/usr/local/lib/node_modules:$NODE_PATH"

    # This NODE path won't break anything even if you don't have NODE installed. 

  # Configurations

    # GIT_MERGE_AUTO_EDIT
    # This variable configures git to not require a message when you merge.
    export GIT_MERGE_AUTOEDIT='no'

    # Editors
    # Tells your shell that when a program requires various editors, use sublime.
    # The -w flag tells your shell to wait until sublime exits
    export VISUAL="subl -w"
    export SVN_EDITOR="subl -w"
    export GIT_EDITOR="subl -w"
    export EDITOR="subl -w"

  # Paths

    # The USR_PATHS variable will store all relevant /usr paths for easier usage
    # Each path is seperate via a : and we always use absolute paths.
    export USR_PATHS="/usr/local:/usr/local/bin:/usr/local/sbin:/usr/bin"

    # Hint: You can interpolate a variable into a string by using the $VARIABLE notation as below.

    # Our PATH variable is special and very important. Whenever we type a command into our shell,
    # it will try to find that command within a directory that is defined in our PATH.
    export PATH="$USR_PATHS:$PATH"

    # If you go into your shell and type: $PATH you will see the output of your current path.

# Helpful Functions
# =====================

# A function to easily grep for a matching process
# USE: psg postgres
function psg {
  FIRST=`echo $1 | sed -e 's/^\(.\).*/\1/'`
  REST=`echo $1 | sed -e 's/^.\(.*\)/\1/'`
  ps aux | grep "[$FIRST]$REST"
}

# A function to extract correctly any archive based on extension
# USE: extract imazip.zip
#      extract imatar.tar
function extract () {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)  tar xjf $1      ;;
            *.tar.gz)   tar xzf $1      ;;
            *.bz2)      bunzip2 $1      ;;
            *.rar)      rar x $1        ;;
            *.gz)       gunzip $1       ;;
            *.tar)      tar xf $1       ;;
            *.tbz2)     tar xjf $1      ;;
            *.tgz)      tar xzf $1      ;;
            *.zip)      unzip $1        ;;
            *.Z)        uncompress $1   ;;
            *)          echo "'$1' cannot be extracted via extract()" ;;
        esac
    else
        echo "'$1' is not a valid file"
    fi
}

# Aliases
# =====================
  # LS
  alias l='ls -lah'

# Case-Insensitive Auto Completion
  bind "set completion-ignore-case on" 

# Final Configurations and Plugins
# =====================
  # Git Bash Completion
  # Will activate bash git completion if installed
  # via homebrew
  if [ -f `brew --prefix`/etc/bash_completion ]; then
    . `brew --prefix`/etc/bash_completion
  fi

  # RVM
  # Mandatory loading of RVM into the shell
  # This must be the last line of your bash_profile always
  [[ -s "/Users/$USER/.rvm/scripts/rvm" ]] && source "/Users/$USER/.rvm/scripts/rvm"  # This loads RVM into a shell session.
```

## Congrats! 

Phew! That was a lot of work, but now you are all set.





