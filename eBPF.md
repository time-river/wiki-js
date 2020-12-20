---
title: eBPF
description: 
published: true
date: 2020-12-20T11:41:35.505Z
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
  * 1. Prominent features
    - [1.6. Allow BPF programs to attach to tracepoints](https://kernelnewbies.org/Linux_4.7#Allow_BPF_programs_to_attach_to_tracepoints)
      * [LWN.net: Tracepoints with BPF](https://lwn.net/Articles/683504/)
  * [7. Tracing, perf, BPF](https://kernelnewbies.org/Linux_4.7#Tracing.2C_perf.2C_BPF)
    - perf bpf: Automagically create a 'bpf-output' event, easing the setup of BPF C "scripts" that produce output via the perf ring buffer. Now it is just a matter of calling any perf tool, such as 'trace', with a C source file that references the `__bpf_stdout__` output channel and that channel will be created and connected to the script
    - (FEATURED) perf bpf: allow bpf programs attach to tracepoints
    - BPF
      * Add support for further security hardening of JIT generated images through generic support for blinding constants. A new `/proc/sys/net/core/bpf_jit_harden` file is provided that admins can tweak along with `/proc/sys/net/core/bpf_jit_enable`, so that for cases where JIT should be enabled for performance reasons, the generated image can be further hardened with blinding constants for unpriviledged users (`bpf_jit_harden` == 1), with trading off performance for these, but not for privileged ones. `bpf_hit_harden` enables blinding for all users. This functionality provides a generic eBPF byte-code level based blinding implementation, which is then just transparently JITed. JIT compilers need to make only a few changes to integrate this facility
      * Extended BPF carried over two instructions from classic to access network packet data: `LD_ABS` and `LD_IND`. They're highly optimized in JITs, but due to their design they have to do length check for every access. This releases incorporates direct packet access, which eliminates the overhead
      * Add event output helper for notifications/sampling/logging
      
- KernelNewbies: Linux_4.8
  * 1. Prominent features
    - [1.2. Support for eXpress Data Path](https://kernelnewbies.org/Linux_4.8#Support_for_eXpress_Data_Path)
      * [Early packet drop — and more — with BPF](https://lwn.net/Articles/682538/)
  * [7. Tracing and perf tool](https://kernelnewbies.org/Linux_4.8#Tracing_and_perf_tool)
    - Support eBPF program attach to tracepoints
    - Allows BPF programs to manipulate user memory during the course of tracing
    - Add `BPF_MAP_TYPE_CGROUP_ARRAY`. It is used to implement a bpf-way to check the cgroup2 membership of a skb
    - Allow dumping the object files generated by llvm when processing eBPF scriptlet events
  * [11. Architectures](https://kernelnewbies.org/Linux_4.8#Architectures)
    - PowerPC
      * Implement JIT compiler for extended BPF
  
- KernelNewbies: Linux_4.9
  * 1. Prominent features
    - [1.3. Efficient BPF-based profiler](https://kernelnewbies.org/Linux_4.9#Efficient_BPF-based_profiler)
  * [6. Tracing and perf tool](https://kernelnewbies.org/Linux_4.9#Tracing_and_perf_tool)
    - perf: Allow attaching `BPF_PROG_TYPE_PERF_EVENT` programs to sw and hw perf events
  * [9. Networking](https://kernelnewbies.org/Linux_4.9#Networking)
    - sched
      * cls_bpf: add support for hardware offload
  * [10. Architectures](https://kernelnewbies.org/Linux_4.9#Architectures)
    - PPC
      * bpf: Add support for bpf constant blinding, implement support for tail calls
      
- KernelNewbies: Linux_4.10
  * 1. Prominent features
    - [1.7. Allow attaching eBPF programs to cgroups](https://kernelnewbies.org/Linux_4.10#Allow_attaching_eBPF_programs_to_cgroups)
      * [LWN.net: Network filtering for control groups](https://lwn.net/Articles/698073/)
  * [6. Tracing and perf tool](https://kernelnewbies.org/Linux_4.10#Tracing_and_perf_tool)
    - Add initial support for tooling hooks, they allow hooking user code at perf events and can be used for manipulation of BPF maps, taking snapshot and reporting results. In this release two perf hook points are introduced: record_start and record_end
  * [10. Networking](https://kernelnewbies.org/Linux_4.10#Networking)
    - Add eBPF hooks for cgroups (FEATURED)
    - BPF for lightweight tunnel encapsulation
    - Netfilter
      * xt_bpf: Add support for attaching an eBPF object by file descriptor. The iptables binary can be called with a path to an elf object or a pinned bpf object
    - BPF
      * Add the LRU versions of the existing `BPF_MAP_TYPE_HASH` and `BPF_MAP_TYPE_PERCPU_HASH` maps: `BPF_MAP_TYPE_LRU_HASH` and `BPF_MAP_TYPE_LRU_PERCPU_HASH`
      * Add support for symlinks and fix mtime/ctime
      * Allow for mount options to specify permissions
      * Allow head adjustment in XDP prog
      
- KernelNewbies: Linux_4.11
  * [2. Core (various)](https://kernelnewbies.org/Linux_4.11#Core_.28various.29)
    - BPF
      * Add new bpf MAP, implementing a longest prefix match trie. This trie implements a longest prefix match algorithm that can be used to match IP addresses to a stored set of ranges
      * Make jited programs visible in traces
      * Add initial bpf tracepoints
      * Enable load bytes helper for filter/reuseport progs
      * Allow adjusted map element values to spill
      * Allow helpers access to variable memory
      * Allow helpers access to map element values
      * Allow b/h/w/dw access for bpf's cb in ctx
      
- KernelNewbies: Linux_4.12
  * [6. Tracing and perf tool](https://kernelnewbies.org/Linux_4.12#Tracing_and_perf_tool)
    - BPF
      * Add array of maps support (`BPF_MAP_TYPE_HASH_OF_MAPS`
      * Add hash of maps support `BPF_MAP_TYPE_ARRAY_OF_MAPS`
      * Introduce `BPF_PROG_TEST_RUN` command to test and performance benchmark bpf programs
      * tools: bpf_jit_disasm: Add option to dump JIT image to a file
  * [10. Networking](https://kernelnewbies.org/Linux_4.12#Networking)
    - eBPF: Add a helper function to retrieve socket uid. This is useful to perform per-UID accounting of network traffic or per-UID packet filtering
    - eBPF: Add a helper function to get socket cookie in eBPF
  * [11. Architectures](https://kernelnewbies.org/Linux_4.12#Architectures)
    - ARM64
      * bpf: implement jiting of `BPF_XADD`
    - MIPS
      * BPF: Add JIT support for `SKF_AD_HATYPE`
    - SPARC
      * Add eBPF JIT
      
- KernelNewbies: Linux_4.13
  * [6. Tracing and perf tool](https://kernelnewbies.org/Linux_4.13#Tracing_and_perf_tool)
    - bpf
      * Add new `SOCKET_OPS` program type and a corresponding struct that allows BPF programs of this type to access some of the socket's fields (such as IP addresses, ports, etc.) and setting connection parameters such as buffer sizes, initial window, SYN/SYN-ACK RTOs, etc
      * Add BPF support to all perf_event types
      * Introduce bpf IDs for both bpf_prog and bpf_map. bpf commands are added to: iterate the prog IDs and map IDs, get a prog/map fd from an ID, get prog/map info from a fd
      * Add syscall lookup support for fd array and htab
      * Allow CGROUP_SKB eBPF program to access sk_buff
      * Expose prog id for cls_bpf and act_bpf
  * [10. Networking](https://kernelnewbies.org/Linux_4.13#Networking)
    - bpf: xdp: Report bpf_prog ID in IFLA_XDP
  * [11. Architectures](https://kernelnewbies.org/Linux_4.13#Architectures)
    - MIPS
      * Add support for eBPF JIT
  * 12. Drivers
    - [12.4. Networking](https://kernelnewbies.org/Linux_4.13#Networking-1)
      * nfp
        - bpf: add support for XDP_FLAGS_HW_MODE
        
- KernelNewbies: Linux_4.14
  * [6. Tracing, perf and BPF](https://kernelnewbies.org/Linux_4.14#Tracing.2C_perf_and_BPF)
    - BPF
      * Add support for `sys_enter_*` and `sys_exit_*` tracepoints
      * Allow selecting numa node during map creation
      * Add new jump instructions (`BPF_J{LT,LE,SLT,SLE`) to eBPF in order to reduce register pressure by avoiding `BPF_J{GT,GE,SGT,SGE`} rewrites and result in shorter BPF programs, less stack usage and less verification complexity
      * Add bpf device maps and XDP_REDIRECT, which can be used to build arbitrary switching frameworks using XDP
      * Implements a sockmap and socket redirect helper using a model similar to XDP netdev redirect. A sockmap is a BPF map type that holds references to sock structs. Then with a new sk redirect bpf helper BPF programs can use the map to redirect skbs between sockets. To use this infrastructure a new BPF program `BPF_PROG_TYPE_SK_SKB` is added that allows users to reference sock details, such as port and ip address fields, to build useful socket layer program
      * Add option to set mark and priority in addition to bound device for newly created sockets. Also, allow the bpf programs to use the `get_current_uid_gid` helper meaning socket marks, priority and device can be set based on the uid/gid of the running process
  * [10. Architectures](https://kernelnewbies.org/Linux_4.14#Architectures)
    - ARM
      * eBPF JIT compiler
    - MIPS
      * bpf: Implement JLT, JLE, JSLT and JSLE ops in the eBPF JIT
      
- KernelNewbies: Linux_4.15
  * [9. Security](https://kernelnewbies.org/Linux_4.15#Security)
    - Add eBPF LSM hooks (see bpf section in networking)
  * [10. Networking](https://kernelnewbies.org/Linux_4.15#Networking)
    - BPF
      * spectre v2 prevention: prevent out-of-bounds speculation, introduce BPF_JIT_ALWAYS_ON config
      * Add 'bpftool' utility, to help with the inspection and simple manipulation of eBPF maps (documentation tools/bpf/bpftool
      * Allow BPF programs to get the base RTT of the connection
      * New bpf cpumap type for XDP_REDIRECT
      * eBPF-based device cgroup controller: cgroup v2 lacks the device controller, provided by cgroup v1; this release adds a new eBPF program type, which in combination of previously added ability to attach multiple eBPF programs to a cgroup, will provide a similar functionality, but with some additional flexibility
      * New file mode and LSM hooks for eBPF object permission control: eBPF objects are accessed, controlled, and shared via a file descriptor, but unlike file descriptors for files and sockets, the existing mechanisms for eBPF object access control are very limited: grant access to all processes, or only `CAP_SYS_ADMIN` processes. This release adds LSM hooks to eBPF so that security systems such as selinux can do a more fine grained control
      * Extend bpf_{prog,map}_info
      * Permit multiple bpf attachments for a single perf tracepoint event
      * Enable generic transfer of metadata from XDP into skb, meaning the packet has a flexible and programmable room for meta data, which can later be used by BPF to set various skb members when passing up the stack
      * Add support for attaching multiple programs per cgroup
      * Add offload as a first class citizen
  * 12. Drivers
    - [12.4. Networking](https://kernelnewbies.org/Linux_4.15#Networking-1)
      * netronome nfp
        - bpf: stack support in offload
        - bpf: support direct packet access
        - bpf ABIv2 and multi port
        - bpf: support `[BPF_ALU | BPF_ALU64] | BPF_NEG`
        
- KernelNewbies: Linux_4.16
  * [10. Networking](https://kernelnewbies.org/Linux_4.16#Networking)
    - BFP
      * Add support for creating maps on networking devices. BPF is programs+maps, the pure program offload has been around for quite some time, this adds the map part of the equation
      * Allow arbitrary function calls from bpf function to another bpf function
      * Add the ability to do BPF directed error injection. A lot of our error paths are not well tested because there is no good way of injecting errors generically. Some subystems have ways to inject errors, but they are random so it's hard to get reproduceable results. With this mechanism it is possible to add determinism to our error injection
      * Implement syscall command `BPF_MAP_GET_NEXT_KEY` for stacktrace map
      * Implements `MAP_GET_NEXT_KEY` command for `LPM_TRIE` map. This command is really useful for key enumeration, and for key deletion if what keys in the trie are unknown
      * Implement `MAP_GET_NEXT_KEY` command for LPM_TRIE map
      * Adds support for several sock_ops callbacks
      * Add a UID to use for ULP socket assignment
      * Allow user space to query prog array on the same tracepoint
      * Allow for correlation of maps and helpers in dump
      * Restrict access to core bpf sysctls
      * tun: allow to attach ebpf socket filter
      * Add eBPF based queue selection to tun
      * bpftool: Add basic cgroup bpf operations to bpftool
    - tools: bpftool: create "uninstall", "doc-uninstall" make targets
  * [11. Architectures](https://kernelnewbies.org/Linux_4.16#Architectures)
    - SPARC
      * bpf: Add JIT support for multi-function programs
  * 12. Drivers
    - [12.4. Networking](https://kernelnewbies.org/Linux_4.16#Networking-1)
      * nfp
        - bpf: adjust head support

- KernelNewbies: Linux_4.17
  * [10. Networking](https://kernelnewbies.org/Linux_4.17#Networking)
    - BPF
      * Add sock_ops R/W access to ipv4 tos
      * Introduce cgroup-bpf bind, connect, post-bind hooks
      * Add support for bpf program to read perf event sample address
      * Adds a BPF hook for sendmsg and senfile by using the ULP infrastructure and sockmap
      * Introduce bpf raw tracepoints. It is a different way to address the pressing need to access task_struct pointers in sched tracepoints from bpf programs
      * Add the BPF_F_INGRESS flag support to the reidrect APIs, bringing the sockmap API in-line with the cls_bpf redirect APIs
      * Whitelist all syscalls for error injection
      * bpftool: improve batch mode
      * Visualization support for eBPF program
  * 12. Drivers
    - [12.4. Networking](https://kernelnewbies.org/Linux_4.17#Networking-1)
      * nfp
        - bpf: add basic support for atomic adds
        - bpf: add support for atomic add of unknown values

- KernelNewbies: Linux_4.18
  * 1. Prominent features
    - [1.3. bpfilter, BPF based networking filtering](https://kernelnewbies.org/Linux_4.18#bpfilter.2C_BPF_based_networking_filtering)
      * [LWN.net: BPF comes to firewalls](https://lwn.net/Articles/747551/)
  * [6. Tracing and perf](https://kernelnewbies.org/Linux_4.18#Tracing_and_perf)
    - Add infrastructure to help in writing eBPF C programs to be used with '-e name.c' type events in tools such as 'record' and 'trace', with headers for common constructs and an examples directory that will get populated as we add more such helpers and the 'perf bpf'
  * [10. Networking](https://kernelnewbies.org/Linux_4.18#Networking)
    - BPF
      * (FEATURED) Add skeleton of bpfilter kernel module: it builds experimental bpfilter framework that is aiming to provide netfilter compatible functionality via BPF
      * Introduce BTF: BPF Type Format. It is the meta data format which describes the data types of BPF program/map. Hence, it basically focus on the C programming language which the modern BPF is primary using. The first use case is to provide a generic pretty print capability for a BPF map
      * Introduce BTF ID - an ID for each loaded BTF program
      * Enhancements for multi-function programs
      * Introduce seg6local End.BPF action with the corresponding new BPF program type BPF_PROG_TYPE_LWT_SEG6LOCAL
      * Hooks for sys_sendmsg similar to existing hooks for sys_bind and sys_connect
      * Allows the BPF loader to figure out the btf_key_id and btf_value_id from a map's name by using BPF_ANNOTATE_KV_PAIR
      * Allow map helpers access to map values directly
      * Hash support for sock
      * Introduce bpf subcommand `BPF_TASK_FD_QUERY` to show which bpf program is attached to which tracepoint/kprobe/uprobe
      * Support offload of bpf_event_output()
  * [11. Architectures](https://kernelnewbies.org/Linux_4.18#Architectures)
    - X86
      * bpf: add eBPF JIT compiler for ia32
  * 12. Drivers
    - [12.4. Networking](https://kernelnewbies.org/Linux_4.18#Networking-1)
      * nfp
        - bpf: complete shift supports on NFP JIT
        - bpf: add programmable RSS support
    - 12.7. TV tuners, webcams, video capturers
      * rc: IR decoding using BPF

- KernelNewbies: Linux_4.19
  * [10. Networking](https://kernelnewbies.org/Linux_4.19#Networking)
    - BPF
      * Implement cgroup local storage for bpf programs. The main idea is to provide a fast accessible memory for storing various per-cgroup data, e.g. number of transmitted packets. Cgroup local storage looks as a special type of map for userspace, and is accessible using generic bpf maps API for reading and updating of the data. The (cgroup inode id, attachment type) pair is used as a map key. A user can't create new entries or destroy existing entries; it happens automatically when a user attaches/detaches a bpf program to a cgroup
      * Introduce `BPF_MAP_TYPE_REUSEPORT_SOCKARRAY` and `BPF_PROG_TYPE_SK_REUSEPORT` to allow userspace to be capable of directly setting up a bpf map which can then be consumed by the bpf prog to make decision. In this case, decide which `SO_REUSEPORT` sk to serve the incoming request. By adding `BPF_MAP_TYPE_REUSEPORT_SOCKARRAY`, the userspace has total control and visibility on where a `SO_REUSEPORT` sk should be located in a bpf map. `BPF_PROG_TYPE_SK_REUSEPORT` allows the bpf prog to directly select a sk from the bpf map
      * Introduce a new bpftool command: cgroup tree. The idea is to iterate over the whole cgroup tree and print all attached programs
      * Add support to call `bpf_get_socket_cookie()` helper from two more program types: `BPF_PROG_TYPE_CGROUP_SOCK_ADDR` and `BPF_PROG_TYPE_SOCK_OPS`
      * Add TCP-BPF callback for listening sockets
      * Print bpftool map data with btf
      * Add support for sharing BPF objects within one ASIC. This will allow us to reuse of the same program on multiple ports of a device leading to better code store utilization. It also enables sharing maps between programs attached to different ports of a device
      * Extend the abilities of bpftool prog load beyond the simple cgroup use cases. Three new parameters are added: type - allows specifying program type; map - allows reusing existing maps; dev - offload/binding to a device
  * 12. Drivers
    - [12.4. Networking](https://kernelnewbies.org/Linux_4.19#Networking-1)
      * nfp
        - bpf: support u16 and u32 multiplications
        - bpf: support u32 divide
        - bpf: xdp_adjust_tail support

- KernelNewbies: Linux_4.20
  * [6. Tracing, perf and BPF](https://kernelnewbies.org/Linux_4.20#Tracing.2C_perf_and_BPF)
    - BPF
      * Implement queue/stack maps. This patchset implements two new kind of eBPF maps: queue and stack. Those maps provide to eBPF programs the peek, push and pop operations, and for userspace applications a new
      * bpf_map_lookup_and_delete_elem() is added
      * Add socket lookup support
      * Adding supprot for two new bpf's tcp sockopts: `TCP_SAVE_SYN` (set) and `TCP_SAVED_SYN` (get)
      * bpftool support for sockmap use cases
      * per-cpu cgroup local storage. It implements per-cpu cgroup local storage and provides an example how per-cpu and shared cgroup local storage can be used for efficient accounting of network traffic
      * bpftool: add support for `BPF_MAP_TYPE_REUSEPORT_SOCKARRAY` maps
      * bpftool: add net support. The functionality to dump network driver and tc related bpf programs are added
    - bpftool: add map create command
  * [10. Networking](https://kernelnewbies.org/Linux_4.20#Networking)
    - Introduce eBPF flow dissector, a more secure flow dissector
      * [LWN.net: Writing network flow dissectors in BPF](https://lwn.net/Articles/764200/)
    - TLS
      * sockmap integration for ktls. It allows for introspection or filtering of L7 data with the help of BPF programs operating on a common input context
  * 12. Drivers
    - [12.4. Networking](https://kernelnewbies.org/Linux_4.20#Networking-1)
      * nfp
        - bpf: add support for BPF-to-BPF function calls

- KernelNewbies: Linux_5.0
  * [6. Tracing, perf and BPF](https://kernelnewbies.org/Linux_5.0#Tracing.2C_perf_and_BPF)
    - BPF
      * Support raw tracepoints in modules
      * Add perf-based event notification for sock_ops. The eBPF kernel module can thus be designed to apply any desired filters to the bpf_sock_ops and trigger a perf-event notification based on the verdict from the filter. The uspace component can use these perf-event notifications to either read any state managed by the eBPF kernel module, or issue a TCP_INFO netlink call if desired
      * Add support for mapinmap in libbpf, a helper for libbpf which would allow it to load map-in-map(`BPF_MAP_TYPE_ARRAY_OF_MAPS` and `BPF_MAP_TYPE_HASH_OF_MAPS`)
      * Introduce bpf_line_info. It will be useful for introspection purpose
      * Add func info support to the kernel so we can get better ksym's for bpf function calls. Basically, function call types are passed to kernel and the kernel extract function names from these types in order to contruct ksym for these functions
      * Add `BPF_F_ANY_ALIGNMENT`, an "any alignment" flags to tell the verifier to forcefully disable it's alignment checks completely. It's needed by SPARC
      * Support socket lookup in `CGROUP_SOCK_ADDR` progs
      * Support of `BPF_ALU | BPF_ARSH`
      * Add skb->tstamp r/w access from tc clsact and cg skb progs
      * sockmap, metadata support for reporting size of msg
      * Allow BPF read access to qdisc pkt_len
      * bpftool
        - Add loadall command
        - Add pinmaps argument to the load/loadall
        - Support loading flow dissector
        - Add a command to dump the trace pipe
        - Add an option to prevent auto-mount of bpffs, tracefs
        - Add owner_prog_type and owner_jited to bpftool output
        - Add `BPF_MAP_TYPE_QUEUE` and `BPF_MAP_TYPE_STACK` to bpftool-map

- KernelNewbies: Linux_5.1
  * [6. Tracing and perf](https://kernelnewbies.org/Linux_5.1#Tracing_and_perf)
    - BPF
      * Add Host Bandwidth Manager. Host Bandwidth Manager is a framework for limiting the bandwidth used by v2 cgroups. It consists of 1 BPF helper, a sample BPF program to limit egress bandwdith as well as a sample user program and script to simplify HBM testing
      * Implements `BPF_LWT_ENCAP_IP` mode in `bpf_lwt_push_encap` BPF helper. It enables BPF programs (specifically, `BPF_PROG_TYPE_LWT_IN` and `BPF_PROG_TYPE_LWT_XMIT` prog types) to add IP encapsulation headers to packets (e.g. IP/GRE, GUE, IPIP)
      * Add new jmp32 instructions. Current eBPF ISA has 32-bit sub-register and has defined a set of ALU32 instructions. However, there is no JMP32 instructions, the consequence is code-gen for 32-bit sub-registers is not efficient. For example, explicit sign-extension from 32-bit to 64-bit is needed for signed comparison
      * Add `__sk_buff->sk`, `struct bpf_tcp_sock`, `BPF_FUNC_sk_fullsock` and `BPF_FUNC_tcp_sock`. Together, they provide a common way to expose the members of struct tcp_sock and struct bpf_sock for the bpf_prog to access
      * Add a new command to bpftool in order to dump a list of eBPF-related parameters for the system (or for a specific network device) to the console
      * Allow BPF programs access `skb_shared_info->gso_segs` field
      * Support `__int128`. Previous maximum supported integer bit width is 64. But the __int128 type has been supported by most (if not all) 64bit architectures including bpf for both gcc and clang
      * Introduce per program stats to monitor the usage BPF
      * Many algorithms need to read and modify several variables atomically. Until now it was hard to impossible to implement such algorithms in BPF. Hence introduce support for bpf_spin_lock
      * Add support for queue/stack manipulations
      * Avoid unloading xdp prog not attached by sample
      * Add `AF_XDP` support to libbpf. The main reason for this is to facilitate writing applications that use `AF_XDP` by offering higher-level APIs that hide many of the details of the `AF_XDP` uapi
      * Add btf documentation
      * Reveal invisible bpf programs. This set catches symbol for all bpf programs loaded/unloaded before/during/after perf-record run `PERF_RECORD_KSYMBOL` and `PERF_RECORD_BPF_EVENT`
      * tracing: Add some useful new functions to the hist trigger code: a snapshot action and an onchange handler
    - perf
      * perf bpf: Automatically add BTF ELF markers to 'perf trace' BPF programs, so that tools such as 'bpftool map dump' can pretty print map keys and values
      * Add support for annotating BPF programs, using the `PERF_RECORD_BPF_EVENT` and `PERF_RECORD_KSYMBOL` recently added to the kernel and plugging binutils's libopcodes disassembly of BPF programs with the existing annotation interfaces in 'perf annotate', 'perf report' and 'perf top' various output formats (--stdio, --stdio2, --tui)
      * Add initial BPF map dumper, initially just for the current, minimal needs of the augmented_raw_syscalls BPF example used to collect pointer args payloads that uses BPF maps for pid and syscall filtering, but will in time have features similar to 'perf stat' `--interval-print`, `--interval-clear`, ways to signal from a BPF event that a specific map (or range of that map) should be printed, optionally as a histogram, etc
  * 9. Architectures
    - [9.8. RISCV](https://kernelnewbies.org/Linux_5.1#RISCV)
      * Add BPF JIT for RV64G
  * 10. Drivers
    - [10.4. Networking](https://kernelnewbies.org/Linux_5.1#Networking-1)
      * nfp: bpf: dead code elimination

- KernelNewbies: Linux_5.2
  * [6. Tracing, perf and BPF](https://kernelnewbies.org/Linux_5.2#Tracing.2C_perf_and_BPF)
    - BPF
      * kbuild: add ability to generate BTF type info for vmlinux and kernel modules. The intent is to record compact type information of all types used inside kernel, in order to enables BPF's compile-once-run-everywhere approach, in which tracing programs that are inspecting kernel's internal data can be compiled on a system running some kernel version, but would be possible to run on other kernel versions (and configurations) without recompilation, even if the layout of structs changed and/or some of the fields were added, removed, or renamed
      * Add global data support for BPF. The kernel has been extended to add proper infrastructure that allows for full .bss/.data/.rodata sections on BPF loader
      * Add a new program type `BPF_PROG_TYPE_CGROUP_SYSCTL` and attach type `BPF_CGROUP_SYSCTL`. `BPF_CGROUP_SYSCTL` hook is placed before calling to sysctl's proc_handler so that accesses (read/write) to sysctl can be controlled for specific cgroup and either allowed or denied, or traced
      * New set of arguments to bpf_attr for BPF_PROG_TEST_RUN: `ctx_in/ctx_size_in` - input context and `ctx_out/ctx_size_out` - output context
      * Add BPF sk local storage. It attempts to make bpf's network programming more intuitive to do (together with memory and performance benefit)
      * Support variable offset stack access from helpers
      * BPF tc tunneling: it allows for dynamic tunneling, choosing the tunnel destination and features on-demand
      * Allow checking SYN cookies from XDP and tc cls act
      * Extend bpf_skb_adjust_room growth to mark inner MAC header so that L2 encapsulation can be used for tc tunnels
      * Improve verifier scalability
      * Add an opt-in interface for tracepoints to expose a writable context to `BPF_PROG_TYPE_RAW_TRACEPOINT_WRITABLE` programs that are attached, while supporting read-only access from existing `BPF_PROG_TYPE_RAW_TRACEPOINT` programs, as well as from non-BPF-based tracepoints
      * Make bpf_skb_ecn_set_ce callable from `BPF_PROG_TYPE_SCHED_ACT`
      * Support `BPF_PROG_QUERY` for `BPF_FLOW_DISSECTOR` attach_type
      * bpftool: Support sysctl hook
      * Add btf dumping to bpftool
  * 11. Architectures
    - [11.5. MIPS](https://kernelnewbies.org/Linux_5.2#MIPS)
      * eBPF: Provide support for MIPS64R6
      * eBPF: Initial support for MIPS32 architecture

- KernelNewbies: Linux_5.3
  * [6. Tracing, perf and BPF](https://kernelnewbies.org/Linux_5.3#Tracing.2C_perf_and_BPF)
    - BPF
      * libbpf: Add BTF-to-C dumping support, allowing to output a subset of BTF types as a compilable C type definitions. This is useful by itself, as raw BTF output is not easy to inspect and comprehend. But it's also a big part of BPF CO-RE (compile once - run everywhere) initiative aimed at allowing to write relocatable BPF programs, that won't require on-the-host kernel headers (and would be able to inspect internal kernel structures, not exposed through kernel headers)
      * Implements initial version (as discussed at LSF/MM2019 conference) of a new way to specify BPF maps, relying on BTF type information, which allows for easy extensibility, preserving forward and backward compatibility
      * Adds support for propagating congestion notifications to TCP from cgroup inet skb egress BPF programs
      * Add `SO_DETACH_REUSEPORT_BPF` to detach BPF prog from reuseport sk
      * Add a sock_ops callback that can be selectively enabled on a socket by socket basis and is executed for every RTT. BPF program frequency can be further controlled by calling bpf_ktime_get_ns and bailing out early
      * Allow CGROUP_SKB programs to use `bpf_skb_cgroup_id()` helper
      * Eliminate zero extensions for sub-register writes
      * Export bpf_sock for `BPF_PROG_TYPE_CGROUP_SOCK_ADDR` prog type and for `BPF_PROG_TYPE_SOCK_OPS` prog type
      * allow wide (u64) aligned stores for some fields of bpf_sock_addr
      * Adds support for fq's Earliest Departure Time to HBM (Host Bandwidth Manager)
      * Introduces verifier support for bounded loops and other improvements
      * bpf: getsockopt and setsockopt hooks
      * libbpf: add bpf_link and tracing attach APIs
  - perf
    * perf tools: Display eBPF code in intel_pt trace
    * perf trace: Auto bump rlimit(MEMLOCK) for eBPF maps sake

- KernelNewbies: Linux_5.4
  * [6. Tracing, perf and BPF](https://kernelnewbies.org/Linux_5.4#Tracing.2C_perf_and_BPF)
    - BPF
      * flow_dissector: pass input flags to BPF flow dissector program, so it can customize parsing by either stopping early or trying to parse as deep as possible
      * xdp: Add devmap_hash map type for looking up devices by hashed index
      * Add BTF ids in procfs for file descriptors to BTF objects
      * Add a new command `BPF_BTF_GET_NEXT_ID` to the bpf() system call, and uses it in bpftool as to list all BTF objects (`bpftool btf list`) loaded on the system (and to dump the ids of maps and programs associated with them, if any)
      * Introduce `BPF_F_TEST_STATE_FREQ` flag to stress test parentage chain and state pruning
      * Expose BTF info through /sys/kernel/btf. It contains all the BTFs present inside kernel. Currently there is only kernel's main BTF, represented as /sys/kernel/btf/vmlinux file. Once kernel modules' BTFs are supported, each module will expose its BTF as /sys/kernel/btf/<module\-name> file
      * **Implement the central part of CO-RE (Compile Once - Run Everywhere, an strategy to allow redistributable BPF binaries, see [this](http://vger.kernel.org/bpfconf2019.html#session-2) and [this](http://vger.kernel.org/lpc-bpf2018.html#session-2))**
      * Introduce a BPF helper to generate SYN cookies
      * bpftool: add net attach/detach command to attach XDP prog
      * bpftool: work with frozen maps
      * bpftool: add support for reporting the effective cgroup progs
  * 12. Architectures
    - [12.4. S390](https://kernelnewbies.org/Linux_5.4#S390)
      * bpf: add JIT support for bpf line info

- KernelNewbies: Linux_5.5
  * 1. Coolest features
    - [BPF improvements: type checking and BPF Trampoline](https://kernelnewbies.org/Linux_5.5#BPF_improvements:_type_checking_and_BPF_Trampoline)
      - [LWN.net: Type checking for BPF tracing](https://lwn.net/Articles/803258/)
  * [6. Tracing, perf and BPF](https://kernelnewbies.org/Linux_5.5#Tracing.2C_perf_and_BPF)
    - BPF
      * **(FEATURED) Revolutionize BPF tracing and BPF C programming: With introduction of Compile Once Run Everywhere technology in libbpf and in LLVM and BPF Type Format (BTF) the verifier is finally ready for the next step in program verification. Now it can use in-kernel BTF to type check bpf assembly code. The end result is safer and faster bpf tracing.**
      * (FEATURED) Introduce BPF trampoline to allow kernel code to call into BPF programs with practically zero overhead
      * Add support for memory-mapping BPF array maps
      * Optimize BPF tail calls for direct jumps
      * Add `probe_read_user`, `probe_read_kernel` and `probe_read_user_str`, `probe_read_kernel_str` helpers
      * bpftool: Allow to read btf as raw data commit
      * flow_dissector: add mode to enforce global BPF flow dissector
    - libbpf
      * Make bpf_helpers.h and bpf_endian.h a part of libbpf itself for consumption by user BPF programs, and add BPF_CORE_READ macros
      * Add `bpf_object__open_file()` and `bpf_object__open_mem()` APIs that use a new approach to providing future-proof non-ABI-breaking API changes
      * Bitfield and size relocations support
      * **Generalize libbpf's CO-RE relocation support. In addition to existing field's byte offset relocation, libbpf now supports field existence relocations, which are emitted by Clang**
      * Teach `bpf_object__open()` (and its variants) to automatically derive BPF program type/expected attach type from section names, similarly to how bpf_prog_load() was doing it
      * Add support for reading 'pinning' settings from BTF-based map definitions. It introduces a new open option which can set the pinning path; if no path is set, /sys/fs/bpf is used as the default. Callers can customise the pinning between open and load by setting the pin path per map, and still get the automatic reuse feature
      * Extend libbpf to support shared umems and Rx|Tx-only sockets 
    - perf
      * tools: Allow to link with libbpf dynamicaly
  * 11. Architectures
    - [11.4. MIPS](https://kernelnewbies.org/Linux_5.5#MIPS)
      * BPF: Disable MIPS32 eBPF JIT
    - [11.9. UML](https://kernelnewbies.org/Linux_5.5#UML)
      * Loadable BPF "Firmware" for vector drivers

- KernelNewbies: Linux_5.6
  * [6. Tracing, perf and BPF](https://kernelnewbies.org/Linux_5.6#Tracing.2C_perf_and_BPF)
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