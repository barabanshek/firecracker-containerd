# Firecracker-containerd for Sabre

Implementation of Sabre plugin for Firecracker described in the paper ["Sabre: Improving Memory Prefetching in Serverless MicroVMs with Near-Memory Hardware-Accelerated Compression"]().

This reposirtory is fork of [Firecracker-containerd](https://github.com/firecracker-microvm/firecracker-containerd) which allows to run regular docker containers in firecracker. To try it, run the following:

```
pushd sabre/

# Prepare machine to run containerd
./install_contrainerd.sh

# Setup env to run containerd (if fails - run one more time)
./configure_node_for_containerd.sh <path to firecracker folder>

# Try it out; first run on a node will take time when activating devmapper device;
# wait until the output stabilizes before moving on
sudo firecracker-containerd --config /etc/firecracker-containerd/config.toml

# In another window
sudo firecracker-ctr --address /run/firecracker-containerd/containerd.sock image pull --snapshotter devmapper docker.io/library/hello-world:latest
sudo firecracker-ctr --address /run/firecracker-containerd/containerd.sock run --snapshotter devmapper --runtime aws.firecracker --rm --tty --net-host docker.io/library/hello-world:latest test
```
