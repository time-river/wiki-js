---
title: eBPF
description: 
published: true
date: 2020-12-20T09:07:15.087Z
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

### kernel source

- KernelNewbies: Linux_3.18
  * 1. Prominent features
    - [1.3. bpf() syscall for eBFP virtual machine programs](https://kernelnewbies.org/Linux_3.18#bpf.28.29_syscall_for_eBFP_virtual_machine_programs)
      * [LWN.net: The BPF system call API, version 14](https://lwn.net/Articles/612878/)
      * 2014.09 [`99c55f7`](https://github.com/torvalds/linux/commit/99c55f7d47c0dc6fc64729f37bf435abf43f4c60) bpf: introduce BPF syscall and maps 

- KernelNewbies: Linux_3.19
  * [11. Networking](https://kernelnewbies.org/Linux_3.19#Networking)
    - Allow eBPF programs to be attached to sockets
      * [LWN.net: Attaching eBPF programs to sockets](https://lwn.net/Articles/625224/)
      * 2014.12 [`89aa075`](https://github.com/torvalds/linux/commit/89aa075832b0da4402acebd698d0411dcc82d03e) net: sock: allow eBPF programs to be attached to sockets
    - bpf: reduce verifier memory consumption
      * 2014.10 [`9c39976`](https://github.com/torvalds/linux/commit/9c3997601d51069ec08d7d06cf31a17884056cc2) bpf: reduce verifier memory consumption

- KernelNewbies: Linux_4.0
  * [11. Networking](https://kernelnewbies.org/Linux_4.0#Networking)
    - tc: add BPF-based action. This action provides a possibility to execute custom BPF code
      * 2015.01 [`d23b8ad`](https://github.com/torvalds/linux/commit/d23b8ad8ab23f5a18b91e2396fb63d10f66b08d6) tc: add BPF based action

- KernelNewbies: Linux_4.1
  * 1. Prominent features
    - [1.8. BPF programs can be attached to kprobes](https://kernelnewbies.org/Linux_4.1#BPF_programs_can_be_attached_to_kprobes)
      * 2015.04 [`2541517`](https://github.com/torvalds/linux/commit/2541517c32be2531e0da59dfd7efc1ce844644f5) tracing, perf: Implement BPF programs attached to kprobes
  * [11. Networking](https://kernelnewbies.org/Linux_4.1#Networking)
    - Extends the "classic" BPF programmable tc classifier by extending its scope also to native eBPF code, thus allowing userspace to implement own custom, 'safe' C like classifiers that can then be compiled with the LLVM eBPF backend to an eBPF elf file and loaded into the kernel via iproute2's tc, and be JITed in the kernel
      * 2015.03 [`9bac3d6`](https://github.com/torvalds/linux/commit/9bac3d6d548e5cc925570b263f35b70a00a00ffd) bpf: allow extended BPF programs access skb fields
  
- KernelNewbies: Linux_4.2
  * [9. Tracing and perf tool](https://kernelnewbies.org/Linux_4.2#Tracing_and_perf_tool)
    - BPF
      * BPF based latency tracing commit
      * Allow BPF programs access skb->skb_iif and skb->dev->ifindex fields commit
      * Allow bpf programs to tail-call other bpf programs commit
      * Allow programs to write to certain skb fields commit
      * Disallow bpf tc programs access current->pid,uid

- KernelNewbies: Linux_4.3
  * [8. Tracing and perf tool](https://kernelnewbies.org/Linux_4.3#Tracing_and_perf_tool)
    - Support BPF programs attached to uprobes and first steps for BPF tooling support
  * [10. Networking](https://kernelnewbies.org/Linux_4.3#Networking)
    - packet: Add fanout mode PACKET_FANOUT_CBPF that accepts a classic BPF program to select a socket
    - packet: Add fanout mode PACKET_FANOUT_EBPF that accepts an en extended BPF program to select a socket
    - tools/net/bpf_jit_disasm: support reading jit dump from file
  * [11. Architectures](https://kernelnewbies.org/Linux_4.3#Architectures)
    - ARM
      * Add support for ARM JIT generation of several BPF instructions
      
- KernelNewbies: Linux_4.4
  * 1. Prominent features
    - [1.6. Unprivileged eBPF + persistent eBPF programs](https://kernelnewbies.org/Linux_4.4#Unprivileged_eBPF_.2B-_persistent_eBPF_programs)
      * Unprivileged eBPF
        - [LWN.net: Unprivileged bpf()](https://lwn.net/Articles/660331/)
    - [1.7. perf + eBPF integration](https://kernelnewbies.org/Linux_4.4#perf__.2B-_eBPF_integration)
      * Persistent eBPF maps/progs
  * [9. Tracing and perf tool](https://kernelnewbies.org/Linux_4.4#Tracing_and_perf_tool)
    - Integration of perf with eBPF that, given an eBPF .c source file (or .o file built for the 'bpf' target with clang), will get it automatically built, validated and loaded into the kernel via the sys_bpf syscall, which can then be used and seen using 'perf trace' and other tools. Users can run commands like perf record --event bpf-file.c ls to try it

- KernelNewbies: Linux_4.5
  * 1. Prominent features
    - [1.9. Performance improvements for SO_REUSEPORT UDP sockets](https://kernelnewbies.org/Linux_4.5#Performance_improvements_for_SO_REUSEPORT_UDP_sockets)
      * 2016.01 [`538950a`](https://github.com/torvalds/linux/commit/538950a1b7527a0a52ccd9337e3fcd304f027f13) soreuseport: setsockopt SO_ATTACH_REUSEPORT_[CE]BPF
  * [9. Tracing and perf tool
](https://kernelnewbies.org/Linux_4.5#Tracing_and_perf_tool)
    - BPF programs can now to specify `perf probe` tunables via its section name, separating `key=val` values using semicolons. A `exec` key is used to specify an user executable which allows to attach BPF programs at uprobe events; a `module` key is used to allow users to attach BPF programs to symbols in modules, an `inline` key that allows to specify whether to probe at inline symbols or not and a `force` key to forcibly add events with existing name"
      * 2015.11 [`361f2b1`](https://github.com/torvalds/linux/commit/361f2b1d1d7231b8685d990b886f599378a4d5a5) perf bpf: Allow BPF program attach to uprobe events
    - Allow BPF scriptlets to specify arguments to be fetched using DWARF info, using a prologue generated at compile/build time. `perf probe` various options can be used to list functions, or see what variables can be collected at any given point
    - bpf: add show_fdinfo handler for maps
    
- KernelNewbies: Linux_4.6
  * [8. Tracing and perf tool](https://kernelnewbies.org/Linux_4.6#Tracing_and_perf_tool)
    - perf BPF
      * Print bpf-output events in `perf script`
      * Add API to set values of map entries in a BPF object, be it individual map slots or ranges
      * Support converting data from bpf events in 'perf data'
      * Introduce support for the `bpf-output` event. BPF programs can output data to a perf ring buffer through that new type of perf event, and perf can create events of that type, and a perf user can use the following cmdline to receive output data from BPF programs `perf record -a -e bpf-output/no-inherit,name=evt/ -e ./test_bpf_output.c map:channel.event=evt/ ls /`
        - 2016.02 [`03e0a7d`](https://github.com/torvalds/linux/commit/03e0a7df3efd959e40cd7ff40b1fabddc234ec5a) perf tools: Introduce bpf-output event
      * Print content of bpf-output event in `perf trace`
  * [10. Networking](https://kernelnewbies.org/Linux_4.6#Networking)
    - BPF
      * Add per-cpu maps, for hash (`BPF_MAP_TYPE_PERCPU_HASH`) and array maps (`BPF_MAP_TYPE_PERCPU_ARRAY`), for performance reasons. For per-cpu array maps, the primary use case is a histogram array of latency where bpf program computes the latency of block requests or other events and stores histogram of latency into array of 64 elements. All cpus are constantly running, so normal increment is not accurate, bpf_xadd causes cache ping-pong and this per-cpu approach allows fastest collision-free counters. For per-cpu hash maps, they are used to do accurate counters without need to use BPF_XADD instruction which turned out to be too costly for high-performance network monitoring
      * Add a new map type, `BPF_MAP_TYPE_STACK_TRACE`, to store stack traces. BPF programs already can walk the stack via unrolled loop of `bpf_probe_read()`s which is ok for simple analysis, but it's not efficient and limited to <30 frames. In this release the programs can collect up to `PERF_MAX_STACK_DEPTH` both user and kernel frames. Using stack traces as a key in a map turned out to be very useful for generating flame graphs, off-cpu graphs, waker and chain graphs
      * Support for access to tunnel options 
    - TCP
      * Faster SO_REUSEPORT for TCP. In the previous release, two performance improvements were done for the SO_REUSEPORT socket option for UDP sockets. In this release, these performance improvements are extended to TCP: faster lookup of a target socket when choosing a socket from the group of sockets, and also expose the ability to use a BPF program when selecting a socket from a reuseport group
      
- KernelNewbies: Linux_4.7
- KernelNewbies: Linux_4.8
- KernelNewbies: Linux_4.9
- KernelNewbies: Linux_4.10
- KernelNewbies: Linux_4.11
- KernelNewbies: Linux_4.12
- KernelNewbies: Linux_4.13
- KernelNewbies: Linux_4.14
- KernelNewbies: Linux_4.15
- KernelNewbies: Linux_4.16
- KernelNewbies: Linux_4.17
- KernelNewbies: Linux_4.18
- KernelNewbies: Linux_4.19
- KernelNewbies: Linux_4.20
- KernelNewbies: Linux_5.0
- KernelNewbies: Linux_5.1
- KernelNewbies: Linux_5.2
- KernelNewbies: Linux_5.3
- KernelNewbies: Linux_5.4
- KernelNewbies: Linux_5.5
- KernelNewbies: Linux_5.6
- KernelNewbies: Linux_5.7
- KernelNewbies: Linux_5.8
- KernelNewbies: Linux_5.9
- KernelNewbies: Linux_5.10

2015.10 [`ea317b2`](https://github.com/torvalds/linux/commit/ea317b267e9d03a8241893aa176fba7661d07579) bpf: Add new bpf map type to store the pointer to struct perf_event

2015.06 [`ffeedaf`](https://github.com/torvalds/linux/commit/ffeedafbf0236f03aeb2e8db273b3e5ae5f5bc89) bpf: introduce current->pid, tgid, uid, gid, comm accessors

2015.08 [`04a22fa`](https://github.com/torvalds/linux/commit/04a22fae4cbc1f7d3f7471e9b36359f98bd3f043) tracing, perf: Implement BPF programs attached to uprobes

2017.06 [`f91840a`](https://github.com/torvalds/linux/commit/f91840a32deef5cb1bf73338bc5010f843b01426) perf, bpf: Add BPF support to all perf_event types

### libbpf source

2019.06 [`abd29c9`](https://github.com/torvalds/linux/commit/abd29c9314595b1ee5ec6c61d7c49a497ffb30a3) libbpf: allow specifying map definitions using BTF