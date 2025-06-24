---
title: "Windows' Innards Part 1"
date: "2025-06-22T23:24:37+07:00"
draft: false
tags:
  - article
  - windows
  - api
  - architecture
categories:
  - fundamental
---
## A bit of introduction
Hello, so I've been trying to get my head around this part of red teaming. People said that if you want to know how to break things, you have to know how it works. Here I am while scratching my head to know how things work.

> Please take everything from here with a grain of salt and do fact check it. Let's just say this article is vegetable, without sprinkle of salt it won't be that good (for me). And feel free to let me know in Twitter DM if there are suggestions, critics, idea, or correction. Thank you!

I want to make the title into *Innards Skynyrd*, is it a good pun? Well anyway, let's dive into it.

---

## Windows? Is it 🪟?
No. We are talking about the operating system (OS) that runs on PC. It manages our device's hardware, apps, memory, security and exposes this to developer via API.

### Brief of Windows Architecture🪟🏛️
Originally, the architecture of Windows started as:

| Year        | Architecture                  |
| ----------- | ----------------------------- |
| 1980s-1990s | 16-bit, MS-DOS                |
| 1990s-2000s | 32-bit, x86 from Win95 to XP  |
| 2005+       | 64-bit, x64 on modern Windows |
Sort of like a *Pokemon* evolution. Then what is x86, is that the bite of 86? No, it came from 80386 intel's processor which introduced 32-bit mode. As far as I know, x86 has the same property as 32-bit. x64 is shorthand for 64-bit version of x86 architecture, also called AMD64.

### Windows API 🪟🔥
In my native language, `api` means `fire`, that's the joke. But in tech, API stands for Application Programming Interface, something with "interface" that we can use to access functionality of subject. Windows API has massive compilation of C/C++ functions. It means that we can access parts of the OS by coding in C with its predefined function that runs in user mode. User mode means that we aren't touching hardware directly by using the API.

### Component Object Model 🧱
The original Win32 API was written in C with direct access to low level functions. But, it's hard to scale, inconsistencies in naming, etc. To tackle those problems, Component Object Model (COM) was born. From what I understand, COM is a binary consists of functions that can be used across multiple programming languages.

### Windows Runtime🪟 🏃‍♂️⏳
Why Windows running? Because running can improve Windows' health. As well as the sanity of coder. This thing made from COM and only available on ARM based OS version. The goal is convenience of API usage across platforms, devices, and programming languages. It's like a wrapper for COM based API.

### .NET 🥅
To catch fishes. Just kidding, this is the framework Windows used for building Windows applications. It consists of Common Language Runtime (CLR) and Framework Class Library (FCL). CLR is the engine to run .NET apps and FCL is libraries of functions used to build apps.

### Evolution
Win32 API -> COM -> WinRT -> .NET

So that's about it I guess. The more I know 🧠 my brain hurts

I guess I should make comment section.

---

## References
Thanks to these books and articles:
- Windows Internals Part 1 by Pavel Yosifovich
- https://learn.microsoft.com/en-us/windows/win32/apiindex/windows-api-list
- https://learn.microsoft.com/en-us/windows/win32/com/component-object-model--com--portal
- https://en.wikipedia.org/wiki/Windows_Runtime
