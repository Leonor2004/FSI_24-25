# Environment Variable and Set-UID Lab

## Task 1

In this task we tested some commands. 
The first command is `printenv` and we use this command to print out the enviroment variables. When we write only the command in the terminal it shows all the enviroment variables, but if we only want one enviroment variable expecifically then we can write "printenv PWD" in the terminal to print the PWD enviroment variable 
expecifically.

The two other commands `export` and `unset` are used to set or unset enviroment variables. When we write in the terminal "export test=response" and then "echo $test" the terminal returns "response". To clear this "test" variable we used "unset test"

## Task 2

When we compile and run the `myprintenv.c` file for the first time it will show us the environment variables of the system accessible by the child process. If we comment the `printenv` function of the child process and uncomment the same function in the parent process we will see that the same output will be printed.

Analysing this outputs we can conclude that when we use the system call `fork()` an exactly copy of the parent process is created (child process) and both keep running in paralel (the system arbitrarily choose which one execute first).

## Task 3

Pequeno resumo

## Task 4

Pequeno resumo

## Task 5

Pequeno resumo

## Task 6

Documentar detalhadamente (juntando printscreens, sequências de comandos executados e/ou excertos de código escrito) todos os passos

## Task 8

Documente os passos necessários para realizar o ataque e explique resumidamente o seu funcionamento
