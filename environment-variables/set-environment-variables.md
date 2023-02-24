

Bash

export VAR="value"

Powershell

[Environment]::SetEnvironmentVariable("YOUR_ENV_VAR", "value", '[User | Machine]')

e.g. [Environment]::SetEnvironmentVariable("FOO", "bar", 'User')
