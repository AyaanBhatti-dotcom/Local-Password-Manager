# Local Password Manager (GPG + Pass)

This project demonstrates how to set up a **local password authentication system** on a Linux machine using **GPG** for encryption and **Pass** (the standard Unix password manager).

It is a hands-on lab demonstrating how to securely generate keys, store passwords, and manage them locally without reliance on cloud providers.

---

## Prerequisites
* Linux-based OS (Kali, Ubuntu, Debian, etc.)
* Terminal access
* `gpg` and `pass` installed (`sudo apt install pass gnupg`)

---

## Step 1: Setting up your Key

1. **Generate the key:**
   Run the following command to start the generation process.
   ```bash
   gpg --gen-key
   ```
   ![Generating Key](https://github.com/user-attachments/assets/c7b6a9b1-2869-4f53-9d48-ea17cedce0ba)

2. **Enter your Name:**
   It will ask for a Real Name. You can provide your actual name or a pseudonym.
   
   ![Name Entry](https://github.com/user-attachments/assets/b99e6b8e-bd5e-4806-93b6-7ba4e91987fd)

3. **Enter your Email:**
   Provide an email address. You can use a real or fake email for this lab.
   
   ![Email Entry](https://github.com/user-attachments/assets/566a64cc-8d97-4773-b134-f25742356b3c)

4. **Confirm Details:**
   Type `O` (for Okay) and press **Enter**.

   ![Confirmation](https://github.com/user-attachments/assets/4856b9cf-6df2-40cf-9371-efad779b739d)

5. **Set a Passphrase:**
   A window will pop up asking for a passphrase. **Pick a strong passphrase and remember it.**
   
   ![Passphrase](https://github.com/user-attachments/assets/bbcc87a4-85d3-416a-b5ff-4b8d31611f14)
   
   *Note: You may get a warning about insecure memory. For testing purposes, you can disregard it.*
   
   ![Warning](https://github.com/user-attachments/assets/bc837583-829b-4233-87ee-016d81680760)

6. **Key Generated:**
   Your key is now created. Make sure to keep it safe.
   
   ![Key Generated](https://github.com/user-attachments/assets/3d78b608-96f5-48e1-9174-20b732452230)
   ![Key ID](https://github.com/user-attachments/assets/5a6b0589-895b-4e93-b47e-4264c87ebfbf)

### Important: Check your Keys
If you lose your key ID, you can list all keys using:
```bash
gpg -K
```
![List Keys](https://github.com/user-attachments/assets/3e387864-2447-41d3-9767-c1db1a7f2c60)

---

## Step 2: Changing Key Expiration

By default, keys may have an expiration date. Here is how to change or remove it.

1. **Identify the Key:**
   Run `gpg -K` to see your keys.
   
   ![List Keys](https://github.com/user-attachments/assets/6d7f24d9-0903-4472-93b4-7cb68cd263f7)
   
   Locate the key you just created.
   
   ![Key Detail](https://github.com/user-attachments/assets/f544650b-2f76-414d-bbe3-223fb31cfa5b)

2. **Edit the Key:**
   Run the edit command using your Key ID (replace the placeholder below):
   ```bash
   gpg --key-edit <YOUR_KEY_ID>
   ```
   ![Edit Mode](https://github.com/user-attachments/assets/0f4acc0d-601d-4215-a0fa-b21bc73a9ce0)

3. **Set Expiration:**
   Type the following commands inside the prompt:
   ```bash
   expire
   ```
   ![Expire Command](https://github.com/user-attachments/assets/d12745d6-036a-4975-8b00-c6b6970c39ae)

4. **Confirm Selection:**
   Set it to `0` so it does not expire (or choose your preferred duration). It will ask for your passphrase again.
   
   ![Duration Selection](https://github.com/user-attachments/assets/c5000112-1b46-4a09-9f02-90eb4242bcc7)

5. **Save Changes:**
   Type `save` to exit and apply changes.
   ```bash
   save
   ```
   ![Save](https://github.com/user-attachments/assets/c6405a17-dcbe-42a7-adf3-d794306dafd5)

---

## Step 3: Initialize Password Store

1. **Initialize Pass:**
   Run the init command with your GPG Key ID:
   ```bash
   pass init <YOUR_KEY_ID>
   ```
   ![Pass Init](https://github.com/user-attachments/assets/23fd1ef9-e8c4-4a9b-8955-3ea41b250d06)

2. **Initialize Git:**
   We initialize a git repository to track changes to our passwords securely.
   ```bash
   pass git init
   ```
   ![Git Init](https://github.com/user-attachments/assets/e529b486-2ee6-4a20-8a45-542358051450)

---

## Step 4: Creating and Storing Passwords

1. **Insert a Password:**
   To manually add a password (e.g., for Facebook):
   ```bash
   pass insert facebook
   ```
   ![Pass Insert](https://github.com/user-attachments/assets/3da9cd11-bfbc-404c-9ae0-c131600145f9)
   
   Enter the password twice when prompted.

2. **View a Password:**
   To retrieve the password later:
   ```bash
   pass show facebook
   ```
   ![Pass Show](https://github.com/user-attachments/assets/ec01e4c0-408d-45c7-a8d1-f8658e353072)

3. **Organize with Folders:**
   You can nest passwords for better organization (e.g., `Social/Instagram`):
   ```bash
   pass insert Social/Instagram
   ```
   ![Folder Insert](https://github.com/user-attachments/assets/b971cb13-5394-4fce-bc08-3ea8b6a3740b)
   
   To view it:
   ```bash
   pass show Social/Instagram
   ```
   ![Folder Show](https://github.com/user-attachments/assets/61af8dd8-b332-4fba-a686-96b58d71dafc)

   **To view the entire tree of passwords:**
   ```bash
   pass show
   ```
   ![Tree View](https://github.com/user-attachments/assets/a1f6d66f-4350-42af-9e4a-deb3a715f8aa)

---

## Step 5: Generating Secure Passwords

Instead of thinking of a password, let `pass` generate a secure one for you.

1. **Generate a Password:**
   This generates a password for "twitter" and copies it to the clipboard automatically (-c is optional but common):
   ```bash
   pass generate twitter
   ```
   ![Generate](https://github.com/user-attachments/assets/8b237b9c-8175-4ff3-a4a1-c6ba47388818)
   ![Generate Output](https://github.com/user-attachments/assets/1ae3376b-8830-44ce-82f6-d4da6b949cde)

2. **Generate in Folders:**
   ```bash
   pass generate Work/Email
   ```
   ![Generate Folder](https://github.com/user-attachments/assets/d9065ef3-ddd0-479a-a2cd-1357cfc9d450)
   ![Generate Folder Output](https://github.com/user-attachments/assets/a321fb58-8693-48be-90bb-2a74222fe68e)

---

## Step 6: Adding Metadata

You can add extra information (like usernames, emails, or security questions) to a password file.

1. **Edit the File:**
   Use the edit command to open the file in a text editor (usually Nano or Vim).
   ```bash
   pass edit <PASSWORD_NAME>
   ```
   ![Edit Command](https://github.com/user-attachments/assets/43656ea3-4337-4603-b6c2-65430afd320b)

2. **Add Data:**
   Add your email or other notes below the password line.
   
   ![Nano Editor](https://github.com/user-attachments/assets/c0823361-bffe-4e17-92d1-e66e9964ed24)
   ![Adding Data](https://github.com/user-attachments/assets/b6f38cf2-3a16-44d4-87a5-3bdb3b38ab63)

3. **Save and Exit:**
   If using Nano:
   * Press `CTRL+X`
   * Press `Y`
   * Press `ENTER`

---

## Advanced Usage & Tips

### 1. Searching for Passwords
Forgot where you stored a password? Use `grep` to search inside your store.

**Search by filename/directory:**
```bash
pass grep "email"
```
![Grep Search](https://github.com/user-attachments/assets/a764979d-aaa4-4197-9759-66aa7e6789fc)

**Search content (e.g., find which password uses a specific email):**
```bash
pass grep "user@example.com"
```

### 2. Copying to Clipboard Securely
To copy a password without displaying it on the screen (shoulder surfing protection):

```bash
pass show -c <PASSWORD_NAME>
```
![Clipboard Copy](https://github.com/user-attachments/assets/75c91a37-d39f-4123-8451-489b9be3f909)

*This will clear the clipboard automatically after 45 seconds.*
