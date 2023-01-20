---
title: "Service Manager for Linux operating systems - systemctl"
date: 2023-01-20T16:12:51+05:30
description: Service Manager for Linux operating systems - systemctl
authorbox: true
sidebar: false
thumbnail: "img/ubuntu_service.jpeg"
pager: true
categories:
  - "Development"
  - "Automation"
tags:
  - "LINUX"
  - "CODE"
  - "DEV-OPS"
---

`systemd` is a system and service manager for Linux operating systems. It provides a standard way to manage services, and it is the default init system for many popular Linux distributions, including Ubuntu. One of the tools that is provided with systemd is systemctl, which is a command-line utility that allows you to control the state of systemd and the services it manages.

In this blog post, we will discuss the basics of systemctl and how it can be used to manage services on an Ubuntu system.

### Basic Usage

The `systemctl` command allows you to view the status of services, start and stop services, and enable or disable services. Here are some basic examples of how you can use `systemctl`:

- To view the status of a service, you can use the `status` command:

```
sudo systemctl status apache2
```

This will show you the current status of the Apache web server, including whether it is running or stopped, and any relevant error messages.

- To start a service, you can use the `start` command:

```
sudo systemctl start apache2
```
This will start the Apache web server if it is not already running.

- To stop a service, you can use the `stop` command:

```
sudo systemctl stop apache2
```

This will stop the Apache web server if it is running.

- To enable a service to start automatically at boot time, you can use the `enable` command:

```
sudo systemctl enable apache2
```

This will create a symbolic link from the Apache service file to the `/etc/systemd/system/multi-user.target.wants` directory, which tells systemd to start the service when the system boots up.

- To disable a service from starting automatically at boot time, you can use the disable command:

```
sudo systemctl disable apache2
```

This will remove the symbolic link that was created by the enable command, preventing the service from starting at boot time.

--- 

### Service Management

In addition to controlling the state of services, systemctl also provides some useful tools for managing services.

- To list all of the services that are currently registered with systemd, you can use the `list-units` command:

```
sudo systemctl list-units --type=service
```

This will show you a list of all of the services on the system, along with their current state and whether they are enabled or disabled.

- To view the details of a service, you can use the `show` command:

```
sudo systemctl show apache2
```

This will display a detailed list of properties for the Apache service, including its dependencies, file paths, and resource limits.

- To view the log messages for a service, you can use the `journalctl` command:

```
sudo journalctl -u apache2
```

This will show you the log messages for the Apache service, which can be helpful for debugging issues with the service.

---

### Creating Custom Services

In addition to managing the services that are included with your Linux distribution, `systemctl` also allows you to create and manage your own custom services. To create a custom service, you will need to create a service file in the `/etc/systemd/system` directory.

A service file is a configuration file that tells systemd how to manage a service. The file should have a.service extension, and it should contain a[Unit]section, a[Service]section, and a[Install] section. Here is an example of a simple service file for a custom service called "my-service":

```
[Unit]
Description=My Custom Service

[Service]
ExecStart=/usr/local/bin/my-service

[Install]
WantedBy=multi-user.target
```

In the `[Unit]` section, you can specify a description for the service, as well as any dependencies that the service has. In the `[Service]` section, you can specify the command that should be run to start the service, as well as any additional options or settings that you want to apply. In the `[Install]` section, you can specify which target the service should be started under.

Once you have created your service file, you can use `systemctl` to manage your custom service just like any other service. For example, to start your custom service, you can use the `start` command:

```
sudo systemctl start my-service
```

To enable your custom service to start automatically at boot time, you can use the enable command:

```
sudo systemctl enable my-service
```

And to disable your custom service from starting automatically at boot time, you can use the disable command:

```
sudo systemctl disable my-service
```
---

### Conclusion
In this blog post, we have discussed the basics of `systemctl` and how it can be used to manage services on an Ubuntu system. We have covered the basic commands for controlling the state of services, as well as some useful tools for managing and troubleshooting services. We have also discussed how to create and manage custom services using `systemctl`.

I hope that this has given you a good understanding of how `systemctl` works and how you can use it to manage services on your Ubuntu system. If you have any questions or comments, please feel free to leave them in the comments section below.