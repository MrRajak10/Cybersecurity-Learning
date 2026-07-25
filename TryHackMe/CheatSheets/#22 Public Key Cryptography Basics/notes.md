Welcome to **Public Key Cryptography Basics**! Cryptography is often considered one of the most intimidating topics for beginners in cybersecurity because of the heavy math involved. But don't worry — as a cybersecurity professional, you rarely need to do the math yourself. You just need to understand *how* the concepts fit together to secure systems.

Let's break down your notes, expand on the mechanics, and see how these concepts are used daily by attackers and defenders.

---

## 1. The Core Security Goals (The "Why")

Before we can protect data, we need to know exactly what we are trying to achieve. In cybersecurity, we use cryptography to answer four specific questions:

* **Confidentiality:** *Can anyone else read this?* We want to scramble data so only authorized people can read it.
* **Integrity:** *Has anything changed?* We need a way to prove that a file or message wasn't secretly altered while traveling across the network.
* **Authentication:** *Who are you?* Proving that a user or a server is exactly who they claim to be (like entering a password).
* **Authenticity:** *Did this message actually come from the sender?* Proving that a specific piece of data originated from a verified source.

---

## 2. Symmetric vs. Asymmetric Encryption

### Symmetric Encryption (The House Key)

Think of symmetric encryption like the key to your front door. You use the exact same key to lock the door (encrypt) and unlock the door (decrypt).

* **The Good:** It is incredibly fast. Algorithms like **AES (Advanced Encryption Standard)** or **ChaCha20** are used to encrypt massive amounts of data, like entire hard drives or gigabytes of video streaming.
* **The Problem:** The **Key Distribution Problem**. If Alice wants to send a secret message to Bob, she has to give Bob the key. But if she sends the key over the internet, a hacker can steal it. How do you securely share a secret key over an insecure network?

### Asymmetric Encryption (The Padlock and Key)

This is where **Public Key Cryptography** saves the day. Instead of one key, you generate a **Key Pair** that are mathematically linked.

1. **Public Key (The Padlock):** You can give this to anyone in the world. Its only job is to lock (encrypt) data.
2. **Private Key (The Key):** You keep this strictly secret on your computer. Its only job is to unlock (decrypt) what the public key locked.

If Alice wants to send a secure message to Bob, she asks for his Public Key (padlock). She locks the message with it, and sends the locked box over the internet. Even if a hacker intercepts it, they can't open it because only Bob has the Private Key.

---

<img width="2048" height="1380" alt="image" src="https://github.com/user-attachments/assets/dd4894d8-4326-4400-8c0e-41f75cfae7e6" />


## 3. How the Math Works: RSA

**RSA (Rivest–Shamir–Adleman)** is one of the most famous asymmetric algorithms. You don't need to do the math, but you need to understand the concept of a **One-Way Function**.

A one-way function is easy to do in one direction, but almost impossible to reverse.

* **Easy:** Multiplying two massive prime numbers together.
* **Hard:** Taking that massive result and figuring out which two prime numbers created it (Factoring).

Because it relies on complex math, RSA is very slow. We don't use RSA to encrypt large files. We use it to securely send a small *Symmetric* key, and then use the faster symmetric key for the rest of the conversation.

---

## 4. Diffie-Hellman Key Exchange

**Diffie-Hellman (DH)** is another brilliant solution to the Key Distribution Problem. It allows two people who have never met to mathematically agree on a shared secret key over a public network, without ever actually sending the key itself!

The classic analogy is mixing paint.

> **Cybersecurity Context:** Diffie-Hellman is used heavily in VPNs (like IPsec or OpenVPN) and in setting up modern HTTPS connections to quickly generate the session keys.

---

## 5. Applying Cryptography: SSH (Secure Shell)

SSH is the industry standard for logging into servers remotely. It uses cryptography heavily.

### Server Authentication (`known_hosts`)

When you connect to a server for the first time, it sends you its Public Key. Your computer asks, "Do you trust this fingerprint?" If you say yes, it saves that key in a file called `~/.ssh/known_hosts`.
If a hacker tries to reroute your connection to a fake server later, the fake server won't have the right private key, the fingerprints won't match, and SSH will block the connection to protect you.

### Client Authentication (`authorized_keys`)

Instead of typing a password to log in, you can generate your own SSH Key Pair.

1. You keep the Private Key on your laptop.
2. You paste your Public Key into the server's `~/.ssh/authorized_keys` file.

Now, when you try to log in, the server encrypts a challenge using your Public Key. If your computer has the matching Private Key, it solves the challenge instantly and logs you in.

> **Important:** Always protect your private SSH key with a **Passphrase**. If a hacker steals your laptop and copies your `id_rsa` file, the passphrase acts as a final layer of encryption so they still can't use it.

---

## 6. Hashing and Digital Signatures

### Hashing (The Digital Fingerprint)

A hash function (like SHA-256) takes data of any size and squashes it into a fixed-length string of characters.

* It is a one-way street (you can't turn a hash back into a file).
* If you change even a single pixel in an image, the entire hash changes completely.
* This provides **Integrity**.

### Digital Signatures (Reverse Asymmetric)

If Asymmetric Encryption is used for Confidentiality (Public Key locks, Private Key unlocks), Digital Signatures flip the rules to provide **Authenticity**.

1. Alice writes a contract and creates a Hash (fingerprint) of the document.
2. Alice encrypts the Hash using her **Private Key**. This encrypted hash is her Digital Signature.
3. Bob receives the contract. He uses Alice's **Public Key** to decrypt the signature, revealing the original hash.
4. Bob hashes the document himself. If his hash matches Alice's hash, he knows two things absolutely:
* **Integrity:** The document wasn't altered.
* **Authenticity:** Only Alice's Private Key could have created that signature, so she definitely sent it.



---

## 7. Digital Certificates and HTTPS

We have a problem: How do you know a Public Key actually belongs to the person claiming it? What if a hacker gives you *their* public key and says, "Hi, I'm Google.com"?

This is solved by **Digital Certificates** and **Certificate Authorities (CAs)**.
A CA (like Let's Encrypt or DigiCert) acts like the DMV. Google proves they own `google.com`, and the CA issues a Digital Certificate. The certificate contains Google's Public Key, and the CA physically signs the certificate with their own Digital Signature.

When you visit an HTTPS website:

1. The server sends your browser its Digital Certificate.
2. Your browser checks the CA's signature.
3. If it is valid and hasn't expired, the padlock icon appears, and a secure session begins.

---

## 8. Practical Tools: GPG (GNU Privacy Guard)

GPG is a command-line tool used to create keys, encrypt files, and digitally sign emails (often called PGP - Pretty Good Privacy).

* `gpg --full-generate-key`: Walks you through creating your own Public/Private key pair.
* `gpg --import filename.key`: Adds someone else's public key to your keychain so you can send them encrypted files.
* `gpg --decrypt file.gpg`: Uses your private key to open a file meant for you.

> **Penetration Testing Context:** When red teamers compromise a developer's machine, one of the first things they look for are poorly protected GPG or SSH keys. If they can steal a private key, they can impersonate that developer across the network or push malicious code to GitHub under their name!

---

## Beginner Mistakes to Avoid

* **Confusing the Keys:** Remember, Public Keys *encrypt*, Private Keys *decrypt*. (Unless you are making a digital signature, where the roles reverse).
* **Sharing Private Keys:** A Private Key should never be emailed, sent in a chat, or uploaded to GitHub. If it is compromised, it is worthless and must be revoked immediately.
* **Ignoring Certificate Warnings:** If your browser says "Your connection is not private," it means the certificate is expired, or someone is actively trying to intercept your traffic (a Man-in-the-Middle attack). Do not click "Proceed anyway"!
