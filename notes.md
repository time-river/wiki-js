---
title: Notes
description: 临时笔记
published: true
date: 2021-03-07T15:11:05.618Z
tags: 
editor: markdown
dateCreated: 2021-03-07T15:11:05.618Z
---

# Notes

# mode

- protected mode
- real-address mode
- system management mode(SMM)
- virtual-8086 mode

# register type / format

- generic register
- control register: CR0 - CR4, CR8 (p2869 for details, fig 2870)
  * CR0: Contains system control flags that control operating mode and states of the processor. (Lx cache policy)
   * CR1: reserved
   * CR2: Contains the page-fault linear address (the linear address that caused a page fault).
  * CR3 (base physical address of PML5/PML4, pgd) PML -- page map table
   * CR8: read-write access to the task priority register(TPR) used to control the priority classes of external interrupts
- extended control register(XCRs)
- debug register: DR0 - DR7
- FLAGS register (fig p80)
  * status
   * DF(direction flag) flag
  * system flags and filed
- extended feature enable register(IA32_EFER): controls activation of IA-32e mode and other IA-32e mode operations.
  • IA32_KERNEL_GS_BASE — Used by SWAPGS instruction.
  • IA32_LSTAR — Used by SYSCALL instruction.
  • IA32_FMASK — Used by SYSCALL instruction.
  • IA32_STAR — Used by SYSCALL and SYSRET instruction.
- model-specific registers (MSRs)
- segment selector: unique identifier for a segment
  * CS / DS / SS / ES / FS / GS
   * task-state segment (TSS) 
   * segment descriptor (pp. 46)
- memory-management registers (pp 2868)
  * system table register: GDTR / IDTR
  * system segment registers: TR(task register) / LDTR
     • Local descriptor-table (LDT) segment descriptor.
    • Task-state segment (TSS) descriptor.
    • Call-gate descriptor.
    • Interrupt-gate descriptor.
    • Trap-gate descriptor.
    • Task-gate descriptor.
  
The LGDT and SGDT instructions load and store the GDTR register, respectively. On power up or reset of the
processor, the base address is set to the default value of 0 and the limit is set to 0FFFFH. A new base address must
be loaded into the GDTR as part of the processor initialization process for protected-mode operation.

When a task switch occurs, the LDTR is automatically loaded with the segment selector and descriptor for the LDT
for the new task. The contents of the LDTR are not automatically saved prior to writing the new LDT information
into the register.
On power up or reset of the processor, the segment selector and base address are set to the default value of 0 and
the limit is set to 0FFFFH.

# memory management

PAE: translate 32-bit linear address to 52-bit physical address -- PDPTE registers refered to page directory pointer table

* model: segmentation, paging

code(CS) / data(DS) / stack(SS)

- segment
- linear address space
- logical address (alias far pointer, a segment selector + offset)
Each segment has a segment descriptor, which specifies the size of the segment, the access rights and
privilege level for the segment, the segment type, and the location of the first byte of the segment in the linear
address space (called the base address of the segment). 

- Segments
  * basic flat model
   * protected flat model
  * multi-segment model
  * IA32e: The processor treats the segment base of CS, DS, ES, SS as zero, creating a linear address that is equal to the effective address. The FS and GS segments are exceptions.
- Logical and Linear Addresses (in protected mode)
  * IA32e: the same as IA32

Q1: segmentation 与 logical address关系（在16-bits，32-bits，64-bits，怎么计算physical address的）？
Q2：64-bit model哪些segment selector用了哪些没用？（隐藏的用了啥，忽略了啥）

page-fault exception error code (pp. 2933)

# procedure

- call procedure
  * near
   * far
- interrupt procedure
  * priviledge changed
   * no priviledged changed
   
# Interrupt and Exception (trap / fault / aborts) 

描述符（descriptor）/ 描述符表（descriptor table） / 寄存器（register）/ segment, segment descriptor ：


- GD / GDT / GDTR
- LD / LDT / LDTR
- IDT (interrupt, trap, task gate descriptor)
- TSS（task-state segments）
  - Data
   - Code
    - System

Gate / Gate descriptor：(p2995) Code modules in lower privilege segments can only access modules operating at higher privilege segments by
means of a tightly controlled and protected interface called a gate. 
- call gate : call gate descriptor. The processor switches to a new stack to execute the called procedure. Each privilege level has its own stack.
- interrupt gate
- trap gate: a manner similar to calling a procedure through call gate
- task gate: accessed through a task switch

Interrupts occur at random times during the execution of a program, in response to signals from hardware. System hardware uses interrupts to handle events external to the processor, such as requests to service peripheral devices. Software can also generate interrupts by executing the INT n instruction.

Exceptions occur when the processor detects an error condition while executing an instruction, such as division by
zero. The processor detects a variety of error conditions including protection violations, page faults, and internal
machine faults. The machine-check architecture of the Pentium 4, Intel Xeon, P6 family, and Pentium processors
also permits a machine-check exception to be generated when internal hardware errors and bus errors are
detected

interrupt: asynchronous events
exception: synchronous event: faults, traps, aborts

The difference between an interrupt gate and a trap gate is as follows. If an interrupt or exception handler is called
through an interrupt gate, the processor clears the interrupt enable (IF) flag in the EFLAGS register to prevent
subsequent interrupts from interfering with the execution of the handler. When a handler is called through a trap
gate, the state of the IF flag is not changed.


If the code segment for the handler procedure has the same privilege level as the currently executing program or
task, the handler procedure uses the current stack; if the handler executes at a more privileged level, the processor
switches to the stack for the handler’s privilege level.