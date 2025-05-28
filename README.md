# add_switch_user_info
adding and switching users in linux

created using chatgpt

---

If you're on a TryHackMe machine and currently have **root access** but want to **switch to a regular (non-root) user**, you can **downgrade your shell** using the `su` or `runuser` command, **if you know the target user's password** or can switch to that user directly.

---

### ✅ **Option 1: Switch to a Known User (if you know their username)**

```bash
su - username
```

* You’ll be prompted for the user’s password.

If the user has **no password** or **password authentication is disabled**, this won’t work.

---

### ✅ **Option 2: Spawn a Shell as Another User (No Password Needed if Root)**

Since you're root, you can switch to any user **without needing their password**:

```bash
su - username
```

OR:

```bash
runuser -l username
```

You can find a list of users with:

```bash
cut -d: -f1 /etc/passwd
```

Focus on users with UID ≥ 1000 (regular users).

---

### ✅ **Option 3: Spawn a Shell as Another User Inline**

```bash
sudo -u username /bin/bash
```

or:

```bash
sudo -u username -i
```

---

### 🔍 **Finding a Non-Root User**

You can look at users who have a UID ≥ 1000:

```bash
awk -F: '$3 >= 1000 && $3 < 65534' /etc/passwd
```

---

### 🧪 Example

```bash
# As root
awk -F: '$3 >= 1000 && $3 < 65534' /etc/passwd

# Suppose you find a user named "john"
su - john
# or
sudo -u john /bin/bash
```

---

As root, you can easily create your own user on a Linux-based TryHackMe machine using the `useradd` command. Here's how to do it:

---

### ✅ **Step-by-Step: Create a New User and Switch to It**

#### 1. **Create the user**

```bash
useradd -m yourusername
```

* `-m` creates a home directory (e.g. `/home/yourusername`).

#### 2. **Set a password (optional)**

```bash
passwd yourusername
```

#### 3. **(Optional) Add user to sudoers**

If you want the user to have `sudo` access:

```bash
usermod -aG sudo yourusername
```

#### 4. **Switch to the new user**

```bash
su - yourusername
```

or

```bash
sudo -u yourusername -i
```

---

### 🧪 Example

```bash
useradd -m hacker
passwd hacker
usermod -aG sudo hacker
su - hacker
```

---


