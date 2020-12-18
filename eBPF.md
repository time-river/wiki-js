---
title: eBPF
description: 
published: true
date: 2020-12-18T14:32:37.182Z
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
  - [LWN.net: allow eBPF programs to be attached to sockets](https://lwn.net/Articles/623370/)
  
2015.03 [`03e69b5`](https://github.com/torvalds/linux/commit/03e69b508b6f7c51743055c9f61d1dfeadf4b635) ebpf: add prandom helper for packet sampling
2015.03 [`c04167c`](https://github.com/torvalds/linux/commit/c04167ce2ca0ecaeaafef006cb0d65cf01b68e42) ebpf: add helper for obtaining current processor id

2015.03 [`9bac3d6`](https://github.com/torvalds/linux/commit/9bac3d6d548e5cc925570b263f35b70a00a00ffd) bpf: allow extended BPF programs access skb fields
  - [LWN.net: bpf: allow extended BPF programs access skb fields](https://lwn.net/Articles/636647/)

2015.04 [`2541517`](https://github.com/torvalds/linux/commit/2541517c32be2531e0da59dfd7efc1ce844644f5) tracing, perf: Implement BPF programs attached to kprobes

2015.06 [`ffeedaf`](https://github.com/torvalds/linux/commit/ffeedafbf0236f03aeb2e8db273b3e5ae5f5bc89) bpf: introduce current->pid, tgid, uid, gid, comm accessors