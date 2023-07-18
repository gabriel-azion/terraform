
---
title: Edge Node first steps
description: 
meta_tags:
namespace: 
permalink:
---


## Installing

1. Generate a credential to run the actions;

   > To generate the credential required to authenticate your edge nodes, follow the steps in the [credentials documentation](/en/documentation/products/credentials/).
2. Install the **Edge Orchestrator** agent on the devices.
3. Authenticate the device after installation.

To begin the **Edge Node** installation process, you must download the **Edge Orchestrator** installation binary of your choice.

> **Note**: The commands executed in the edge-orchestrator agent, must be executed with root user privileges.

The root user is the one who has unrestricted access to all system components, whether files or processes. If you do not have these privileges you may experience installation failures when attempting to manage some operating system requirements that demand such privileges.

Check the list of compatible platforms for Azion Edge Node and download the one of your preference:

| Operating System | Architecture | File                                                         |
| :--------------- | :----------: | ------------------------------------------------------------ |
| FreeBSD          |    x86_64    | [edge-orchestrator](https://downloads.azion.com/freebsd/x86_64/edge-orchestrator) |
| FreeBSD          |    ARM64     | [edge-orchestrator](https://downloads.azion.com/freebsd/arm64/edge-orchestrator) |
| Linux            |    x86_32    | [edge-orchestrator](https://downloads.azion.com/linux/x86_32/edge-orchestrator) |
| Linux            |    x86_64    | [edge-orchestrator](https://downloads.azion.com/linux/x86_64/edge-orchestrator) |
| Linux            |    ARM32     | [edge-orchestrator](https://downloads.azion.com/linux/arm32/edge-orchestrator) |
| Linux            |    ARM64     | [edge-orchestrator](https://downloads.azion.com/linux/arm64/edge-orchestrator) |
| MacOS            |    x86_64    | [edge-orchestrator](https://downloads.azion.com/darwin/x86_64/edge-orchestrator) |

Alternatively, you can download it using the Command line. In the example, the download link refers to the Linux/x86_64 agent. If you want to download another version, just change the url for the required operating system or architecture:

`curl -O http://downloads.azion.com/linux/x86_64/edge-orchestrator`

After downloading, you must follow the steps below, in order to install the **Edge Orchestrator** agent to your device:

1. Install the **Edge Orchestrator** agent:<br />
   `chmod +x edge-orchestrator`<br />
   `./edge-orchestrator install`
2. Enter the **token** for the Edge Orchestrator agent;
3. Confirm the next steps;
4. Start the **Edge Orchestrator** agent after installing it:<br />
   `edge-orchestrator start`<br />
   **Note**: if your operating system does not have a service manager (systemd, for example), you must run it in the foreground.<br />
   `edge-orchestrator start --foreground`

   > The *logs* to run the Edge Orchestrator agent are stored in:  <br />`/var/log/azion/edge-orchestrator.log`

---

## Viewing your nodes

Whenever the installation code is run for any device and it has been authenticated by the Token, the edge nodes will be listed in [Real-Time Manager](https://manager.azion.com/).

To view the list of edge nodes created for your account, follow the steps below:

1. Go to [Real-Time Manager](https://manager.azion.com/);
2. Open the **Edge Orchestration** item on the top left menu and select the **Edge Node** page;

> You can verify the listed items by checking the HashId column, as it contains the hash used to create and authenticate the edge node.

---

## Authorizing 

You must authorize your edge nodes to begin orchestrating them. To authorize an edge node, follow the steps below:

1. Open the list of **Edge Nodes** in [Real-Time Manager](https://manager.azion.com/).
2. Click on the **icon** (key) and accept the confirmation window.

> After the authorization, the **Edge Node** can take up to *10 seconds* before services can be orchestrated.

You can also authorize all the edge nodes you want at once. To start using  this option, follow the steps below:

1. Open the list of Edge Nodes in [Real-Time Manager](https://manager.azion.com/).
2. Select the items you want to authorize or, if you prefer, select all items by checking the first check box on the left.
3. On the top right corner, click the **Actions** button and select **Authorize**.
4. A message to confirm your action will be shown, click the **Confirm** button to save your selection.
5. You'll see the following confirmation message: "*X nodes were successfully authorized!*"

---

## Services

You can provision the services registered in your library by following steps:

1. Open the list of **Edge Nodes** in [Real-Time Manager](https://manager.azion.com/);
2. Select the **Edge Node** that you want to configure;
3. Open the **Services** tab and click the **Add Service** button;
4. Link it to the service you want and, if necessary, you can configure the variables required by the service.

> Services that are due to be orchestrated via Edge Node, must be registered in **Edge Libraries** > **Edge Services** and marked as active.

Once the service is provided, Edge Node can begin orchestrating it based on resource priorities. You can monitor the service installation process via logs in the Edge Orchestrator agent.

> The service installation logs are stored in <br/>`/var/log/azion/edge-services.log`
