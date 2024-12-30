# Ultimate Home Server design goals

## Container based

Containers have taken over as a well known way to distribute applications, and provide some very powerful ways to manage
many disparate applications running on the same hardware.

## High availability

It should be as high availability as useful. While this is a home server and HA is usually not necessary, I do plan on
running some critical network services on this such as DNS for my network. One thing I've learned from running Pihole on
my TrueNAS server is that boot times on server hardware can be truly awful and having a complete network outage for that
time is at best annoying but there's been a few times where an update has gone bad and really caused problems for
multiple hours while I try to debug.

HA means some kind of clustering solution, but I don't want to completely blow the bank so I've decided to go with a
Raspberry Pi cluster using one of the carrier boards that are available. I'll be using six Raspberry Pi CM5s mounted on
a [DeskPi Super6C][deskpi-super6c].

[deskpi-super6c]: https://deskpi.com/collections/deskpi-super6c

## Remote access, from anywhere

There will be some local-only services running on the cluster to help run my home network, like Pihole, and these
services should only be available from my home network. However I also want to run services that I will need to access
remotely too, like Nextcloud. It's right there in the name - it's only useful if I can pretend it's my own little cloud
service.

Remote access will be handled via [Tailscale][tailscale]. Tailscale is a mesh VPN solution built on top of Wireguard
which sands off some of the rough edges and makes initiating connections painless. [It also deals with lots of networking
shenanigans][tailscale-new-internet] that can make life hard. The end result is a simple-to-use product that I can leave
connected even when I'm at home with very little overhead for connecting to other devices on my local network. The
local-to-local connections only traverse the LAN, meaning you can get close to line speed of the slowest physical link
between the two devices, no matter where they are. Tailscale isn't free for commercial usage, but they have a very
generous free personal plan which supports up to three users and 100 devices which will be more than enough for this
project.

Thus, only two modes of operation. Either a service is a local service and it is exposed out of Kubernetes using a local
ingress, or it is a remote-access service exposed through Tailscale. There is no need to try to expose the same service
in both ways.

[tailscale]: https://tailscale.com/
[tailscale-new-internet]: https://tailscale.com/blog/new-internet

## No local storage

Since I have a TrueNAS server, I've decided to use that for persistent storage as it already has backups and other
things like that setup. That means I can focus this project on just setting up new network services. I'll be using a mix
of iSCSI and NFS to share storage space over to the cluster.

The Super6C has an NVMe slot for each compute module, so if you wanted to go off script here then there's
definitely room for a local Ceph or similar cluster running across the cluster to use for persistent storage.

## Learning

There's an explicit goal for this project of learning and documenting my journey with some new hardware running a new
software stack. I'm going to be building a Kubernetes cluster on this hardware and this is my first experiences with
Kubernetes as well. This is going to be a learning cluster and while I'm planning on running this permanently myself, I
wouldn't recommend this approach in a production environment. We'll be building up our Kubernetes cluster from scratch
and I'm sure there's better distributions of Kubernetes available.

## Next

Next, we'll take a look at the [specific list of hardware and other prerequisites][prerequisites] we'll need to work on
this project.

[prerequisites]: ./01-prerequisites.md
