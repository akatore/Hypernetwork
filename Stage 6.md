# Description
## Like containers and images, you can delete networks and volumes. In this stage, you need to delete them. But beware, don't delete any volume with essential data. Follow the objectives below to finish your job.

# Objectives
- Delete the hyper-network network;
- Delete the hyper-volume volume.

```PowerShell
(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1>  docker network list
NETWORK ID     NAME            DRIVER    SCOPE
c8aad952ac5c   bridge          bridge    local
3b2c8d1649c5   host            host      local
814301c3bf72   hyper-network   bridge    local
cb2f959712a2   none            null      local
(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1> docker network rm hyper-network
hyper-network
(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1> docker volume list
DRIVER    VOLUME NAME
local     hyper-volume
(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1> docker volume rm hyper-volume
hyper-volume
(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1>
```
