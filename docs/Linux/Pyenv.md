---
tags: pyenv python setup
---
# Pyenv
## Installation
Install [pyenv](https://github.com/pyenv/pyenv) for managing multiple python versions
```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

Then, add the commands to `~/.bashrc`:
```bash
# pyenv installation
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
# end of pyenv installation
```

Add to `~/.profile`:
```bash
# pyenv installation
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
# end of pyenv installation
```

Restart the shell, for the `PATH` changes to take effect
```path
exec "$SHELL"
```

## Python installation
Install Python for both 3.x and 2.x
```bash
pyenv install 3.10.5
pyenv install 2.7.18
```

You can verify that both installations have been successful with
```bash
pyenv global
python3 --version # Check your associated python3 version
python2 --version # Check your associated python2 version
```