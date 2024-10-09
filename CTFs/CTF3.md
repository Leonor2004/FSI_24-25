# CTF3

This document is a brief explanation of our resolution of the Wordpress CTF presented in class during week 3.

## Recognition

 Our first step was collecting as much information about the site as possible.

 We searched in the different pages of the site for any usefull information and we found the versions of the WordPress and plugins.
 We also found two possible users called "admin" and "Orval Sanford".

 <img src= fotos/CTF3_1.png width="550" >
 <sub><sup>Image of the versions available on the site.</sup></sub>

 <img src= fotos/CTF3_2.png width="550" >
 <sub><sup>Image of a chat with 2 possible users.</sup></sub>

## Searching and Choosing for Vulnerabilities

After completing the recognition phase, we began exploring potential vulnerabilities within the specific version of WordPress we were using. However, we were unable to find any vulnerabilities that aligned with our objectives. We then shifted our focus to examining the plugins installed on the platform. During this process, we successfully identified the vulnerability we were targeting. It is associated with the MStore API plugin, version 3.9.0, and is listed under CVE-2023-2732.

## Finding an Exploit

After identifying the wanted vulnerability, we searched for its exploits online, and quickly found a github repository authored by RandomRobbieBF (https://github.com/RandomRobbieBF/CVE-2023-2732) with exactly what we wanted. 


## Exploring the Vulnerabilities

 Now that we had an exploit it was time to explore this vulnerability of the server.
 We ran the script, with the username "admin" that has the user ID 1. This action was successful and we then entered a new url where we were already logged in as an administrator. Then the flag was in the text that showed up.

 <img src= fotos/CTF3_3.png width="550" >
 <sub><sup>Image of the terminal after successfully running the python script.</sup></sub>

 <img src= fotos/CTF3_4.png width="550" >
 <sub><sup>Image of the site already logged in as admin, where we found the flag.</sup></sub>

## How to Prevent
The best way to prevent this exploit is to update the MStore API plugin to a version higher than 3.9.2, because this CVE only affects versions up to, and including, 3.9.2.
