---
title: "Windows' Innards Part 1"
date: "2025-06-22T23:24:37+07:00"
draft: false
tags:
  - article
  - windows
  - api
categories:
  - fundamental
---
## A bit of introduction
Hello, so I've been trying to get my head around this part of red teaming. People said that if you want to know how to break things, you have to know how it works. Here I am while scratching my head to know how things work.

> Please take everything from here with a grain of salt and do fact check it. Let's just say this article is vegetable, without sprinkle of salt it won't be that good (for me). And feel free to let me know in Twitter DM if there are suggestions, critics, idea, or correction. Thank you!

I want to make the title into *Innards Skynyrd*, is it a good pun? Well anyway, let's dive into it.

---

## Windows? Is it 🪟?
No. We are talking about the operating system (OS) that runs on PC. It manages your device's hardware, apps, memory, security, and exposes all that to developers through APIs.

---

## Shallow Dive of Windows Interface 🤿
How we can access things inside Windows? Let’s dip our toes in first.

### Windows API 🪟🔥
In my native language, `api` means `fire`, that's the joke. But in tech, API stands for Application Programming Interface, something with "interface" that we can use to access functionality of subject. The Windows API is a massive collection of C/C++ functions. It means that we can access parts of the OS by coding in C with its predefined functions that run in user mode, meaning they don't interact with hardware directly, they request services from the OS.

### Component Object Model 🧱
The original Win32 API was written in C with direct access to low level functions. But, it's hard to scale, inconsistencies in naming, etc. To tackle those problems, Component Object Model (COM) was born. From what I understand, COM is a binary component model. It defines how code written in different languages can interact through interfaces.

### Windows Runtime🪟 🏃‍♂️⏳
Why Windows running? Because running can improve Windows' health. As well as the sanity of coder. WinRT is built on COM and works on all Windows platforms (x86, x64, ARM). It's not the same as Windows RT, which was ARM-only. The goal is convenience of API usage across platforms, devices, and programming languages. It's like a wrapper for COM based API.

### .NET 🥅
To catch fishes. Just kidding, this is the framework Windows used for building Windows applications. It consists of Common Language Runtime (CLR) and Framework Class Library (FCL). The CLR (Common Language Runtime) runs .NET apps, it handles memory, security, and compilation. The FCL (Framework Class Library) provides reusable classes for files, networking, UI, and more.

### Evolution 🧬
`Win32 API -> COM -> WinRT -> .NET`

So that's about it I guess. The more I know 🧠 my brain hurts

I guess I should make comment section.

---

## Threads and Sewing 🧵
Named like the culture of spilling tea all over X platform, a thread is the unit of execution inside a process. It’s what the CPU actually runs. It is a stream of what, who, when instructions run. It's like the instruction pointer on debugger, except we don't have to hit 'C' every time we want to continue from breakpoint.

### Stack 🧱
Each thread has a stack, a memory structure that stores function calls, return addresses, and local variables.

### Instruction Pointer 🫵
At ease! Well, not that kind of instruction. The Instruction Pointer (IP) tells the CPU which instruction to execute next, like a finger on the current line of code.

### Thread ID 🪪
The unique number as identifier for thread. No pun here.

---

## Trust the Process 🛞
Well you shouldn't trust processes fully. Have you ever suffered from a crashed app and you hit `ctrl+alt+del` or `ctrl+shift+del`? Yes, that thing right there even when opened to kill the process still freezes the entire laptop, at least in my case. A process is running instance of something inside your gadget. It could be an app, another app, and-uh, you get the idea. An app can spawn multiple processes with each doing different tasks. But usually it runs as a single process with multiple threads.

### Executable Programs 🧑‍💻
A program, or notepad, when you run it, writes thing you'll never save and just leave it there. Running a program like notepad creates a process, it may even spawn helper processes or background threads.

### Process ID 🪪
The unique number as identifier for processes. Your notepad might have 1337 as its process ID.

### Private Virtual Address Space 🌌
Each process gets its own virtual memory space, a private sandbox or domain expansion where it can load code, data, and stacks. This keeps processes isolated and secure.

### Open Handles 👐
Open handles are like bookmarks. They point to system resources (files, registry keys, etc.) the process is using. All threads in a process share this table.

### Security Context 📖
Context matters. As well as security. This thing right here acts as access control, governs who runs the process, what groups, what privileges, etc.

---

## References
Thanks to these books and articles:
- Windows Internals Part 1 by Pavel Yosifovich
- https://learn.microsoft.com/en-us/windows/win32/apiindex/windows-api-list
- https://learn.microsoft.com/en-us/windows/win32/com/component-object-model--com--portal
- https://en.wikipedia.org/wiki/Windows_Runtime
- https://hansanimperera.medium.com/a-dive-into-windows-internals-processes-threads-handles-and-the-registry-e0efdac81a3a
