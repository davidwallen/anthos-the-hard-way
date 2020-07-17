# Prerequisites

## Local Linux Workstation

This tutorial is intended to demonstrate local installation of Kubernetes for integration into Anthos. As such, it presumes a sufficiently configured local workstation. In my case, the local workstation looks like this:

Processor: AMD Ryzen Threadripper 3960X 24-Core Processor
Memory: 128 GB
Machine Type: Desktop
Operating System: Pop!_OS 20.04 LTS
Disks:
  Phison Electronics Corporation E16 PCIe4 NVMe Controller @ 1 TB (solid-state disk)
  Phison Electronics Corporation E16 PCIe4 NVMe Controller @ 1 TB (solid-state disk)
  Phison Electronics Corporation E16 PCIe4 NVMe Controller @ 500 GB (solid-state disk)
  RAID 0
    ATA WDC WD2003FZEX-0 @ 2 TB (spinning disk)
    ATA WDC WD20EADS-00R @ 2 TB (spinning disk)

RAID 0 is brittle - we are not creating a robust or resilient instance here so I am not concerned about rebuilding this infrastructure. In fact, my goal is to practice so dealing with a disk failure mid way through this exercise, while annoying, would not be catastrophic. Thererfore I am not shy about using the 4 TB array for my VM store.

I have an embarassment of riches on this machine. I have seen evidence of similar setups on NUCs with an i7, 1 TB of disk, and 32 GB of RAM. As a test, I will try this set up on a VC66 I have in storage.

## Google Cloud Platform

This tutorial leverages the [Google Cloud Platform](https://cloud.google.com/) to streamline provisioning of the compute infrastructure required to bootstrap a Kubernetes cluster from the ground up. [Sign up](https://cloud.google.com/free/) for $300 in free credits.

[Estimated cost](https://cloud.google.com/products/calculator/#id=55663256-c384-449c-9306-e39893e23afb) to run this tutorial: $0.23 per hour ($5.46 per day).

> The compute resources required for this tutorial exceed the Google Cloud Platform free tier.

### Google Cloud Platform SDK

#### Install the Google Cloud SDK

Follow the Google Cloud SDK [documentation](https://cloud.google.com/sdk/) to install and configure the `gcloud` command line utility.

Verify the Google Cloud SDK version is 262.0.0 or higher:

```
gcloud version
```

#### Set a Default Compute Region and Zone

This tutorial assumes a default compute region and zone have been configured.

If you are using the `gcloud` command-line tool for the first time `init` is the easiest way to do this:

```
gcloud init
```

Then be sure to authorize gcloud to access the Cloud Platform with your Google user credentials:

```
gcloud auth login
```

Next set a default compute region and compute zone:

```
gcloud config set compute/region us-west1
```

Set a default compute zone:

```
gcloud config set compute/zone us-west1-c
```

> Use the `gcloud compute zones list` command to view additional regions and zones.

## Running Commands in Parallel with tmux

[tmux](https://github.com/tmux/tmux/wiki) can be used to run commands on multiple compute instances at the same time. Labs in this tutorial may require running the same commands across multiple compute instances, in those cases consider using tmux and splitting a window into multiple panes with synchronize-panes enabled to speed up the provisioning process.

> The use of tmux is optional and not required to complete this tutorial.

![tmux screenshot](images/tmux-screenshot.png)

> Enable synchronize-panes by pressing `ctrl+b` followed by `shift+:`. Next type `set synchronize-panes on` at the prompt. To disable synchronization: `set synchronize-panes off`.

Next: [Installing the Client Tools](02-client-tools.md)
