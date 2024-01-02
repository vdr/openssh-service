openssh-service
===============

Service definition for Brew installed OpenSSH.

For Apple Silicon Macs, Sonoma (14+)

Although the default ssh-agent in macOS Sonoma supports FIDO2 somewhat, it needs a Security Provider
(like [Yubico libfido2](https://github.com/Yubico/libfido2)) Unfortunately [it is not working out of the box](https://github.com/Yubico/libfido2/issues/464) and require "too" clever rebuild.

Instead, enable the vanilla OpenSSH agent, with necessary tooling to make it work.

Homebrew generates the plist for us directly.

However you can use the `openssh-service` command for some extra features:
* `eval $(openssh-service eval)` - set up environment variables for ssh-agent in the current session

* `openssh-service check` - Check if things are setup correctly

* `openssh-service run` - Run the ssh-agent in the foreground, if the service is not enabled

* `openssh-service logpath` - Get the log path if the service is running through launchd
  eg:

  ```shell
  cat $(openssh-service logpath)
  ```

  

## Installation

`brew install vdr/tap/openssh-service`

Then just follow the instructions options from the caveats.

### [Recommended] Using Launchd

1. Start the service: `brew services start openssh-service`
2. Add the following to your `~/.ssh/config`:
```
Include /opt/homebrew/etc/ssh_config.d/openssh-service.conf
```

### Manual

1. Run in a terminal: `openssh-service run`
2. Run in each terminal you want to use ssh-agent: `eval $(openssh-service eval)`
Alternative:
3. Add the content of `openssh-service.conf` to the top of `~/.ssh/config`:
