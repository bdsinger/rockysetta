# rockysetta
Single command that runs Rocky Linux amd64 on Apple Silicon using Rosetta2 under Lima.

# Requirements
- Apple Silicon based Mac
- macOS 13 Ventura or higher
- [Lima](https://github.com/lima-vm/lima) installed via, say, [Homebrew](https://brew.sh)

# Details
It does this by running arm64 Rocky 9 VM under VZ and then running an amd64 Rocky 9 docker
container on it using [containerd](https://github.com/containerd/containerd)

# Usage
```
Usage: rockysetta 
   [-n|--name instance_name(default)]
   [-t|--template template_name(custom)]
   [-c|--container container_name(rockylinux:9.3)]

On first run with no arguments, this script:

1) creates a lima "Rocky 9 using VZ" template
2) saves it to the template directory as "custom.yaml"
3) uses it to run Intel based Linux on Apple Silicon via Rosetta2

You can overwrite any existing custom template with the same one
it creates on first run, by supplying the args "-t newcustom"

Continue running it with no arguments to reuse this initial config,
unless you have a reason to play with Lima and make your own templates
or multiple instances with different names. If you prefer a different
distro you can supply its dockerhub name via the -c option.

If the command runs successfully, the end result will be a
root prompt (#) in rockylinux:9.3 for intel (x86_64)

If you want to build containers for intel-based linux you can
install apptainer at the prompt, via:

dnf install -y epel-release
dnf install -y apptainer
```
# Purpose
This script's main purpose is building Apptainer/Singularity
containers for an Intel-based Rocky 9 Linux HPC cluster.
Once built with Apptainer, the resulting SIF image is scp'd
to the server and run there.

Since building containers is most easily done as root, it is
convenient to build images on your own PC or laptop and transfer
the image over. Since an Apple Silicon based Mac is a popular
laptop choice, this complicates things slightly over the days of
Intel-based Macs. Getting a good working solution took longer
than expected so am publishing the result here for others to use.

# Warning
Anything you install or change in the Intel-based Linux environment
is not saved upon exiting! This includes installing apptainer every
time. You are running in a Docker container, that's why. It's good
to have a predictable and working environment but with enough use
I'm sure this situation will need to be remedied somehow.

# Support
As-is but might update it if anyone cares.
