# Format-String Vulnerability Lab

# Introduction

descrição do set up talvez ?

## Question 1

### Task 1

In this task, our goal was to interact with a vulnerable server running a program with a format-string vulnerability. The server accepts user input and processes it through the myprintf() function, which is improperly formatted, leading to exploitable behavior. By constructing a specific input, we were able to cause the program to crash. Crashing the program provides an entry point for testing the vulnerability.

To list the running containers we used the command:

```bash
docker ps --format "{{.ID}} {{.Names}}"
```

<div align="center">
    <figure>
        <img src="images/logbook6/logbook6_1.png">
        <figcaption style="font-size: smaller">Figure 1: ???</figcaption>
    </figure>
</div>

In one terminal we did:

<div align="center">
    <figure>
        <img src="images/logbook6/logbook6_2.png">
        <figcaption style="font-size: smaller">Figure 2: ???</figcaption>
    </figure>
</div>

The server program is accessible through a container with IP 10.9.0.5, running on port 9090. To simulate an exploit and verify the vulnerability, we first sent a benign message to confirm the server setup 8on another terminal.

```bash
echo hello | nc 10.9.0.5 9090
```
And on the first terminal we recived:

<div align="center">
    <figure>
        <img src="images/logbook6/logbook6_3.png">
        <figcaption style="font-size: smaller">Figure 3: ???</figcaption>
    </figure>
</div>

And after doing CONTROL+C on the second terminal, this shows on the first:

<div align="center">
    <figure>
        <img src="images/logbook6/logbook6_4.png">
        <figcaption style="font-size: smaller">Figure 4: ???</figcaption>
    </figure>
</div>

Now that we tested with that benign message is time to do one that will hopefully crash the program.

```bash
cat ../attack-code/build_string.py | nc 10.9.0.5 9090
```

After using this command, we check the other terminal and see that it didn't print the "Returned properly" message, meaning we successfuly crashed the program.


### Task 2

documentação

### Task 3 (excluindo a Task 3.C)

documentação


## Question 2

documentação
