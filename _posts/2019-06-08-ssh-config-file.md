---
layout: post
title:  "SSH Config File"
date:   2019-06-08
categories: [note]
tags:   [ssh, configuration, automation]
---
In my daily work, I usually login and logout of a half dozen remote servers, either EC2 or local virtual machines.
And I hate remembering all those various username, hostname and command line options to specify a non-standard connection
port or forwarding to local ports to the remote machine.

## Shell Aliases

The first thing come to my mind and the most frequently used approach to simplifying the ssh process is to define a shell
alias. For example, if you have a remote host named `awesome-cloud-desktop.example.com` and you have set it up with
public/private authorization for password-less logins. This means a typical ssh login command line will look like this:

```bash
ssh shinthirty@awesome-cloud-desktop.example.com -p <your_defined_port>
# Assusming you keys are properly set up...
```

Not too bad. But to cut down the verbosity you can use alias to simplify the command line:

```bash
alias dev='ssh shinthirty@awesome-cloud-desktop.example.com -p <your_defined_port>'
dev # To connect
```

## ~/.ssh/config

However, there is a more elegant and flexible solution to this problem. For the same purpose above, enther the following ssh
config file:

```config
# Contents of ~/.ssh/config
Host dev
  HostName awesome-cloud-desktop.example.com
  Port <your_defined_port>
  User shinthirty
```

This means I could simply do `ssh dev` and the options will be read from the configuration file.

## Going Further

There are acutally a lot more than setting up the host profile in the SSH config file. You can use different private key for a
specific host or set up local port forwarding to access a blocked port on the remote server.

---

## Reference

* [Simplify Your Life With an SSH Config File, Joël Perras](https://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/)
