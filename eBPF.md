---
title: eBPF
description: 
published: true
date: 2020-12-17T16:29:12.041Z
tags: 
editor: markdown
dateCreated: 2020-12-17T15:36:22.454Z
---

# eBPF

[ebpf.io](http://ebpf.io/)
[Linux doc: BPF ring buffer](https://www.kernel.org/doc/html/latest/bpf/ringbuf.html)
[LWN.net: Kernel operations structures in BPF](https://lwn.net/Articles/811631/)

## Usage Question

[StackOverflow: What is not allowed in restricted C for ebpf?](https://stackoverflow.com/questions/57688344/what-is-not-allowed-in-restricted-c-for-ebpf)
  - [cilium: BPF and XDP Reference Guide](https://docs.cilium.io/en/latest/bpf/)
  
## History

2014.09 [`99c55f7`](https://github.com/torvalds/linux/commit/99c55f7d47c0dc6fc64729f37bf435abf43f4c60) bpf: introduce BPF syscall and maps 
  - [LWN.net: BPF syscall, maps, verifier, samples](https://lwn.net/Articles/603816/)
  
2014.11 [`d0003ec`](https://github.com/torvalds/linux/commit/d0003ec01c667b731c139e23de3306a8b328ccf5) bpf: allow eBPF programs to use maps
2014.11 [`0f8e4bd`](https://github.com/torvalds/linux/commit/0f8e4bd8a1fc8c4185f1630061d0a1f2d197a475#diff-44bbf34e69b69ec779122b4b90cd8f00437d4aa974ee9b6bbcf2d88b8b12ec6f) bpf: add hashtable type of eBPF maps

2014.12 [`89aa075`](https://github.com/torvalds/linux/commit/89aa075832b0da4402acebd698d0411dcc82d03e) net: sock: allow eBPF programs to be attached to sockets
