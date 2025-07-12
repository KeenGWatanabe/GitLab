# GitLab SSH key
Creating an SSH key for your GitLab profile is a straightforward process. Follow these steps to generate and add an SSH key to your GitLab account:

### **Step 1: Check for Existing SSH Keys**
Before generating a new key, check if you already have one:
```sh
ls ~/.ssh/
```
If you see files like `id_rsa` and `id_rsa.pub`, you already have an SSH key.

### **Step 2: Generate a New SSH Key (if needed)**
Run the following command (replace `your_email@example.com` with your GitLab email):
```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- For older systems that don’t support `ed25519`, use:
  ```sh
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  ```
- Press `Enter` to accept the default file location (`~/.ssh/id_ed25519` or `~/.ssh/id_rsa`).
- Enter a secure passphrase (optional but recommended).

### **Step 3: Start the SSH Agent**
Ensure the SSH agent is running:
```sh
eval "$(ssh-agent -s)"
```
Then add your SSH key:
```sh
ssh-add ~/.ssh/id_ed25519   # or ~/.ssh/id_rsa if using RSA
```

### **Step 4: Copy the SSH Public Key**
Display and copy your public key:
```sh
cat ~/.ssh/id_ed25519.pub   # or ~/.ssh/id_rsa.pub
```
(Select and copy the entire output, which starts with `ssh-ed25519` or `ssh-rsa`.)

### **Step 5: Add the SSH Key to GitLab**
1. Go to [GitLab](https://gitlab.com/) and sign in.
2. Click your profile picture → **Preferences** → **SSH Keys**.
3. Paste the copied public key into the **"Key"** field.
4. Give it a **Title** (e.g., "My Laptop").
5. Click **Add key**.

### **Step 6: Test the SSH Connection**
Verify the setup by running:
```sh
ssh -T git@gitlab.com
```
You should see:
```
Welcome to GitLab, @username!
```

### **Troubleshooting**
- **Permission denied?** Ensure the public key is correctly added to GitLab.
- **Still issues?** Run `ssh -vT git@gitlab.com` for debugging.

Now you can use SSH to interact with GitLab repositories securely! 🚀