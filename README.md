# Dotfiles

Dotfiles provides a simple way to manage your most important application configuration files that live in your home directory. Dotfiles are stored under version control and then linked in to your home directory from the checked out repository.

### Installation
```bash
$ git clone git@github.com:hertzz/dotfiles.git ~/dotfiles
```

### Running
```bash
$ ~/dotfiles/bin/dotfiles
```

### Handlers
Handlers represent individual applications which you want to manage dot files for.  To control which handlers are processed at runtime, you can modify the `config.sh` file and simply add or remove handlers from the `HANDLERS_ENABLED` array.

By default, the enabled handlers array is as follows:
```bash
HANDLERS_ENABLED=(aliases curl git screen vim wget zsh)
```

You can explicitly define files that you wish to ignore being linked to your home directory. To do so, you can simply add a property to any handler's bootstrap file named `EXCLUDED_FILES`, and those files will be ignored when the handler links are processed. For example, the `vim` handler excludes the following files from the bootstrap script:
```bash
EXCLUDED_FILES=(.vitest)
```

### Application files
To add new dot files to be stored under version control and linked to your home directory, add new files under a specific handlers `files` directory, and the handler will automatically link this file at runtime.

### Configuration

#### Home Directory
If you wish to change the location of where your dot files are stored, you can change the `HOME_DIRECTORY` property in the `config.sh` configuration file:
```bash
HOME_DIRECTORY="${BASE_DIR}/home_sandbox"
```
By default, the home directory is based off the `$HOME` environment variable.

#### Logging
Dotfiles supports three different logging types:
```bash
stdout
file
both
```

By default, `stdout` logging output is used which writes messages directly to STDOUT. When `file` is used, it will write all messages to a date appended log file in the `log` directory at the root level of dotfiles. When `both` is used, you get the same logging functionality as both `stdout` and `file` logging combined.
