---
title: 'Windows Innards Part 2'
date: '2025-08-16T21:21:58+07:00'
draft: false
tags:
  - article
  - windows
  - api
categories:
  - fundamental
---
## A bit of introduction
It's been a while since I'm uploading more content on this web. First part of this series is me trying to sound like linkedin-y style with all those of emoticons. Looking back at it, looks like an AI generated content and too much jokes poured into it.

> Please take everything from here with a grain of salt and do fact check it. Let's just say this article is vegetable, without sprinkle of salt it won't be a good food (atleast for me). And feel free to let me know in Twitter DM if there are suggestions, critics, idea, or correction. Thank you!

---

## Throwback
Let's peek to what I've learnt before: 
- A bit of Windows Interface (API, COM, Runtime, .NET) which basically a bunch of functions on libary
- A bit of Thread (stack, instruction pointer, thread ID) on how do CPU and process rearrange itself.
- A bit of Process (process ID, virtual address, open handles, security context, programs) where it's about process components, how did it allocate things, and how do they identified.

Now, onto the topic about jobs, memory, and access modes.

---

## Jobs
Damn, these days are rough man. Waiting for those 19 mil- Back to the topic, job is a model where it invokes several processes into a unit, usually using a sequence of program like batch file. You may find or manage it on job scheduler or task management.

---

## Memory
Parts of computer that holds the data using lots of addresses in a disk or RAM. Everything has parts for "memory", for example:
- Registers: used in CPU to holds the data of what its currently doing
- Cache L1, L2, L3: used in CPU to stores recently used data
- RAM: to stores data for running programs
- Disk: storage such as HDD and SSD for long term storage

Some of them are used by operating system to allocated virtual and physical memory logically.

### Virtual Memory
As far as I know virtual memory on Windows is implemented as table of reference to map what address each pointing to in CPU. What I meant by that is, there are tables of memory (virtual) in RAM that tells CPU where each piece of memory is, whether its in RAM or disks (physical). So, whenever you want to access the physical memory, you would reference it through the virtual one. This is needed because there are times RAM couldn't handle all of the processes, so it has to page or store process queue into disk and have a "mental mapping" of what to be accessed next.

### Physical Memory
I think I have nothing much to explain here. This is where the real memory resides on the hardware inside your computer. Your data has exact position in form of electronic. You might find your programs, codes, and processes that you run on your computer.

---

## Processor Access Modes
This thing is mentioned on part 1 on Windows API, where parts of OS can be accessed by using predefined funtions that run in user mode. The modes is made to protect from unwanted changes on OS. There are kernel and user mode in Windows.

### Kernel Mode
When you stumble upon kernel mode, then you become the computer. You can control and do anything from it, ranges from accessing memories, accessing hardwares, controlling every part of systems, etc. This is what people usually said about ring level 0. Some of anticheat do run in this mode and usually EDR run in this mode too. Windows has a feature on its kernel called Data Execution Prevention (DEP) that will prevent malicious process from running. Although, Windows don't have protection once a process runs in the kernel mode. But, to reduce risk, Windows enforce driver signing and monitor kernel mode drivers.

### User Mode
Usually applications run in this mode since its more secure and stable. Programs are isolated from other things such as OS and other applications, which helps prevent crashes or unauthorized access to system memory. If it needs to perform privileged operations such as accessing files, using the network, or communicating with hardware, it must request these actions from the kernel through a system call. The CPU then temporarily switches to kernel mode to execute the request.

---

## References
Thanks to these books and articles:
- Windows Internals Part 1 by Pavel Yosifovich
- https://learn.microsoft.com/en-us/windows/win32/procthread/job-objects
- https://learn.microsoft.com/en-us/answers/questions/2696389/physical-and-virtual-memory-in-windows-10
- https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode
