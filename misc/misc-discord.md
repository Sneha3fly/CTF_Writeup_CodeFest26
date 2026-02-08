**Misc — Discord Welcome Challenge**

Challenge: Sanity Check

Category: Misc

Difficulty: Trivial

Objective: Find the hidden flag in the official Discord server.

**Approach :**

The challenge hinted that the flag was hidden somewhere in the CTF’s Discord server. After joining the server, I inspected the #ctf channel and checked the channel header and pinned information.
At the top of the channel, there was a grey clickable box labeled “Let’s go brrrrrr.” Clicking this box opened the channel topic popup, which contained the hidden flag.
The below image shows this:-\
![Free_points](images/discord_flag)
 
This follows a common CTF pattern where organizers embed flags inside Discord metadata such as channel topics, pinned messages, or announcement sections.
**Flag :**

CodefestCTF{w3lcome_70_cod3f3s7}

**Lessons Learned :**

•	Always inspect Discord channel topics and pinned sections during CTFs

•	Click interactive UI elements — flags may be hidden in metadata

•	Many misc challenges rely on familiarity with common platform tricks
