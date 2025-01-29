# TryHackMe-CTF-Mr-Robot
Utilizing exploitation techniques to hack a machine.

We will start with a classic nmap scan:

![nmap](https://github.com/user-attachments/assets/9654de18-7b6d-4f27-b9f7-6728194518fc)

We can clearly see that there is a web application running on this virtual machine, let's for a little visit:

![fsociety](https://github.com/user-attachments/assets/3bfed332-45b5-4a0c-914e-79849607b12a)

Playing around with the commands won't give us much except cool animations. The next logical step would be to fuzz for more directories:

![gobuster](https://github.com/user-attachments/assets/48ac2f64-63e3-4e07-984d-c1ebf4908917)

We do find a couple of directories and we see that this is most definitely using wordpress but we do need the credentials to access that admin panel. Checking the other directories will reveal to us the first key in the robots directory:

![robots](https://github.com/user-attachments/assets/b42c2ce6-6f73-4188-8b7e-7fa10299249a)

The dictionnary also included seems very long so maybe there is another way to find our credentials. Looking through more of our directories will we find something interesting in license. It seems to be base64 and when we decode it we find a login and password!

![license](https://github.com/user-attachments/assets/7534f2d9-c3b3-4380-9cff-add0747e966b)

![login](https://github.com/user-attachments/assets/274e552b-48e6-4e7d-bdbf-2dc189603cda)

Using our credentials we can access the admin portal for wordpress:

![logged in](https://github.com/user-attachments/assets/b6cf5737-ac42-4505-9b7d-8a180994e32d)

If we browse the admin panel we will notice that there is section in theme where we can put our own php code which we absolutely will by copy pasting a webshell in it:

![php admin](https://github.com/user-attachments/assets/bae1bed5-7da0-4612-bcba-abe15a72f834)

Now let's connect to our webshell using netcat:

![shelled ](https://github.com/user-attachments/assets/88a98f50-8dbf-4345-8d5e-6b16309ce8e1)

Now that we are in let's find our 2nd key. We found it but can't access it so but if we look at the other file we can find a user and hash and cracking that hash will give us the password:

![shell log in](https://github.com/user-attachments/assets/17e2233b-3974-41fa-84a8-efccaa676c73)

![cracked](https://github.com/user-attachments/assets/a207f5f2-b213-445e-b362-5d1c3519a0bf)

Now that we are robot we can see the 2nd key:

![key 2](https://github.com/user-attachments/assets/5877554b-ff51-47af-9ba6-38530f3d61cc)

The last key im assuming is hiding in root which we can't access so we will need to escalate our privileges. Checking our permissions will allow to find that we are capable of running nmap which is odd and when checking gtfo bins we find a way to escalate our privileges!

![privesc](https://github.com/user-attachments/assets/51f678a5-3e9e-42f0-ae61-f8e629572e10)

![nmap shell](https://github.com/user-attachments/assets/19c4dc8c-3151-4d4c-bbf2-c138568b1847)

We can now see the final key:

![key 3](https://github.com/user-attachments/assets/fd111b65-3632-4b53-a18a-aa7ae3c514d4)
