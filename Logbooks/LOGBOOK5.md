# Buffer-Overflow Attack Lab - Set-UID Version

# Introduction

In this logbook we will execute an exploit related to buffer-overflow. To do that we need to turn off some countermeasures of the system.

To prevent this types off attacks the systems implemented an address space randomization that will randomize the starting address of heap and stack. This makes guessing the addresses difficult that is one of the critical steps of buffer-overflow attacks.

To turn off this feature we ran this command:

```bash
$ sudo sysctl -w kernel.randomize_va_space=0
```

In the recent versions of Ubuntu OS, the `/bin/sh` symbolic link points to the `/bin/dash` shell. The `dash` program, as well as `bash`, has implemented a security countermeasure that prevents itself from being executed in a `Set-UID` process.

So we used the following command to link `/bin/sh` to other shell that doesn't have such a countermeasure `zsh`:

```bash
$ sudo ln -sf /bin/zsh /bin/sh
```

## Question 1

### Task 1

In this task we can understand how a shell code works. Using the code provided in the file *call_shellcode.c* we can initiate a new shell. When we compile this program with the given *Makefile* it will create two binaries, *a32.out* and *a64.out*. Runnig them we will see that a new shell is initiated. 

### Task 2


Explique sucintamente o processo de resolução

### Task 3

documente todos os passos necessários para demonstrar o ataque


## Question 2

