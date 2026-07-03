### Rainbow Table Attack:

- "A rainbow table is a precomputed table for caching the output of cryptographic hash functions, usually for cracking password hashes"

- Tables are usually used in recovering a key derivation function (or credit card numbers, etc.) up to a certain length consisting of a limited set of characters.

- It is a practical example of a space–time trade-off, using less computer processing time and more storage than a brute-force attack which calculates a hash on every attempt, but more processing time and less storage than a simple key derivation function with one entry per hash.

- Use of a key derivation that employs a salt makes this attack infeasible.

- Reference: <https://en.wikipedia.org/wiki/Rainbow_table>

A rainbow table is a precomputed table which contains word lists like dictionary files and brute force lists and their hash value.

- **Compare the Hashes**: Capture the hash of a password and compare it with the precomputed hash table. If a match is found then the password is cracked.

- **Easy to Recover**: It is easy to recover passwords by comparing captured password hashes to the precomputed tables.

<!-- -->

- **Precomputed Hashes**:

  - 1qazwed à 21c40e47dba72e77518ee3ef88ad0cc8

  - hh021da à 2ce80b192cfa47a0d6c8a2446314810b

  - 9da8dasf à eb0f5690164ffabbed1744087a4d6761

  - sodifo8sf à 2c749bf3fff89778efc50af7e4f8d6a8

- **Tools to create rainbow tables:**

  - **RTGEN**: This program needs several parameters to generate a rainbow table.

  - **WinRTGEN**: It is a graphical rainbow table generator that supports …

- **Rainbow Tables used for password cracking:**

  - "A rainbow table is a precomputed table for caching the output of cryptographic hash functions, usually for cracking password hashes".

  - Tables are usually used in recovering a key derivation function (or credit card numbers, etc.) up to a certain length consisting of a limited set of characters.

  - It is a practical example of a space–time tradeoff, using less computer processing time and more storage than a brute-force attack which calculates a hash on every attempt, but more processing time and less storage than a simple key derivation function with one entry per hash.

  - Use of a key derivation that employs a salt makes this attack infeasible.

<!-- -->

- Reference: <https://en.wikipedia.org/wiki/Rainbow_table>

**Rainbow Tables used for password cracking**

- Rainbow table is a precomputed table for caching the output of cryptographic hash functions for cracking password hashes.

- Can you describe Rainbow table? A rainbow table is a listing of all possible plaintext permutations of encrypted passwords specific to a given hash algorithm. Rainbow tables are often used by password cracking software for network security attacks. All computer systems that require password-based authentication store databases of passwords associated with user accounts, typically encrypted rather than plaintext as a security measure.

<!-- -->

- Key logging password attack an installed keylogger intercepts passwords as they are typed. Defend Use MFA, so even one password intercepted other protect our account.

- Manual guessing password attack Personal information, such as name and date of birth can be used to guess common passwords. Defend Prioritise administrator, remote user accounts monitor failed login attempts, train users to report suspicious activity.

- Non electronic password attacks Attacker does not need technical knowledge to crack password such as Shoulder surfing Looking at either the user's keyboard or screen while he/she is logging in. Social engineering, dumpster diving.

- Offline attacks Attacker copies targets password file and tries to crack password on his own system such Rainbow table attack (Pre computed hashes), Distributed network attack

- Passive online attacks Attacker cracks password without communicating with authorizing party such as Wire sniffing, Man in the middle attack, Replay attack
