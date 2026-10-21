# COEP CyberCell Induction CTF Write-up

## About me and this CTF
I am Aafan, a B.Tech Computer Science student at COEP. I joined the CyberCell induction CTF to explore cybersecurity, and this write-up explains how I solved all six challenges.

## Challenge 1: Nothing to See Here
**Category:** Web source

**The challenge:** The webpage looked completely empty. It asked whether what the browser shows is the whole story.

**What I did:** I opened the page source (the hint mentioned Ctrl+U) and read through it, looking for the flag format `COEP{`.

**What I found:** The flag was hidden in an HTML comment. Browsers do not show comments on the page, but they still send them to everyone.

**What I learned:** What I see on the screen is not everything the server sends. Developers must never leave secrets, passwords or keys in comments, because anyone can read them.

## Challenge 2: Mystery String
**Category:** Cryptography (encoding vs encryption)

**The challenge:** I was given a long string of letters and numbers that looked like nonsense.

**What I did:** The challenge notes pointed to Base64. The text used only letters and numbers, and the tools listed were `base64 --decode` and CyberChef. I decoded it using a command-line Base64 decode.

**What I found:** The decoded text was the flag, and its words said that Base64 is not encryption.

**What I learned:** Base64 is encoding, not encryption. There is no key, so anyone can decode it. It must never be used to protect secrets.

## Challenge 3: Picture Perfect
**Category:** Forensics (file metadata)

**The challenge:** I was given a photo called `photo.jpg`. The page said the secret was not in the pixels but in the hidden information stored inside the file (metadata).

**What I did:** I downloaded the file, right-clicked it, chose Properties, and opened the Details tab. Then I read the lines one by one, looking for anything unusual.

**What I found:** The flag in the format `COEP{...}` was written in the Title, Subject and Authors fields. The Program name field also showed a CyberCell forensic tool name.

**What I learned:** Photos carry hidden labels (metadata) such as the camera, the date, comments and sometimes the GPS location. I did not need a special tool, because Windows shows many of these fields. This can leak private information, so metadata should be removed before sharing photos.

## Challenge 4: Polite Robots
**Category:** Web recon (robots.txt)

**The challenge:** The page explained that websites have a file called `robots.txt` that tells search engine bots which folders to avoid. I had to find the hidden path listed there and visit it.

**What I did:** I opened the `robots.txt` file at the root of the site and read the `Disallow:` lines (https://cybercell.coeptech.ac.in/mini-ctf/s3cr3t-vault-7f3a/). Then I typed that path after the site address in my browser.

**What I found:** The flag was not inside `robots.txt`. It was on the disallowed page, in the format `COEP{...}`.

**What I learned:** `robots.txt` only asks well-behaved bots to stay away. It is not a lock, and anyone can read it. Listing private pages there actually shows attackers where to look. Secret pages need real protection, such as a login.

## Challenge 5: Where Was This Taken?
**Category:** OSINT (open-source intelligence)

**The challenge:** I was given a photo of an old stone building. The GPS data had been removed, so I had to find the building using only the picture. The flag was the building's common name.

**What I did:** I used the clues in the briefing: a heritage stone building with a clock tower, an administrative landmark on our own COEP campus. I recognised it as the Main Building, where the student section, exam cell and MIS office are. Then I double-checked it with Google Lens, which matched photos of the COEP main building.

**What I found:** Two sources agreed (my knowledge of the campus and Google Lens). I wrote the common name in lowercase with underscores to make the flag.

**What I learned:** OSINT means using public information. Local knowledge is powerful, and checking an answer with a second source avoids mistakes.

## Challenge 6: Not What It Seems
**Category:** File forensics (magic bytes)

**The challenge:** A file called `mystery.jpg` could not be opened as a picture.

**What I did:** The page showed the first bytes of the file: `50 4B 03 04`, which spell "PK". These are the magic bytes of a ZIP file. So I renamed `mystery.jpg` to `mystery.zip` and extracted it.

**What I found:** Inside was a text file called `flag.txt` with the flag.

**What I learned:** A file extension is only a label. The real type is decided by the first bytes of the file. Attackers can disguise harmful files as pictures, so analysts check the signature and not the name.

## What I learned overall

| Challenge | Where the secret was hidden | Idea or tool |
|---|---|---|
| 1 | Inside the page source | View source |
| 2 | Disguised as Base64 text | Decode Base64 |
| 3 | Inside the file's metadata | File Properties, Details tab |
| 4 | Behind a path listed in robots.txt | Reading robots.txt |
| 5 | In the real world | OSINT: Google Lens and local knowledge |
| 6 | A ZIP disguised as a JPG | Magic bytes, then rename and extract |

I learned to ask three questions: Where could the secret be hiding? What form is it in? Which tool will show it? This helped me with the later challenges.

## AI tools used
I used Claude (an AI assistant by Anthropic) to explain concepts in simple language, to suggest tools and commands. I also used Google Lens for the reverse image search in Challenge 5. I ran each step myself, checked the results, and edited the text to match what I did.
