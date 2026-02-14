# kiro-wsl-error-document

— Neeche **poori guide Roman Urdu** mein convert kar di hai, structure aur technical cheezein same rakhi hain taake samajhna easy ho.

---

# 🔧 Kiro + Claude Code Router - Complete Troubleshooting Guide

### Mukammal Kharabi Hal Karne Ki Guide

---

## 📋 Fehrist / Table of Contents

1. Authentication Conflict Error
2. Externally Managed Environment Error
3. Python Command Not Found
4. Configuration Error - No Kiro Credentials
5. Server Testing & Verification
6. Final Setup Steps

---

## 1. Authentication Conflict Error

### ❌ Masla / Problem:

```
Auth conflict: Both a token (ANTHROPIC_AUTH_TOKEN) and an API key (ANTHROPIC_API_KEY) are set.
```

### 📸 Screenshot:

Yeh error tab aati hai jab dono environment variables set hon.

### ✅ Hal / Solution:

#### **Option A: Temporary Fix (Sirf current Terminal session ke liye)**

**Ubuntu/Linux:**

```bash
unset ANTHROPIC_AUTH_TOKEN
```

**Windows Command Prompt:**

```cmd
set ANTHROPIC_AUTH_TOKEN=
```

---

#### **Option B: Permanent Fix (Hamesha ke liye)**

**Ubuntu/Linux:**

1. `.bashrc` file kholen:

```bash
nano ~/.bashrc
```

2. Yeh line dhoondhein:

```bash
export ANTHROPIC_AUTH_TOKEN=...
```

3. Is line ko delete kar dein ya start mein `#` laga dein.

4. Ya phir file ke end mein yeh line add kar dein:

```bash
unset ANTHROPIC_AUTH_TOKEN
```

5. File save karein:

* Ctrl + O
* Enter
* Ctrl + X

6. Changes apply karein:

```bash
source ~/.bashrc
```

---

**Alternative Easy Method:**

```bash
echo "unset ANTHROPIC_AUTH_TOKEN" >> ~/.bashrc
source ~/.bashrc
```

---

**Windows:**
System Environment Variables se `ANTHROPIC_AUTH_TOKEN` delete kar dein.

---

### 🔍 Verify Karein:

```bash
# Linux
echo $ANTHROPIC_AUTH_TOKEN
echo $ANTHROPIC_API_KEY

# Windows
echo %ANTHROPIC_AUTH_TOKEN%
echo %ANTHROPIC_API_KEY%
```

---

## 2. Externally Managed Environment Error

### ❌ Masla / Problem:

```
error: externally-managed-environment
This environment is externally managed
```

### 📸 Screenshot:
<img width="466" height="131" alt="image" src="https://github.com/user-attachments/assets/f2f78ebb-7866-48e4-952a-01419bcb5a91" />


Yeh error Ubuntu/Debian mein Python packages install karte waqt aata hai.

---

### ✅ Hal / Solution:

#### **Option A: Quick Fix**

```bash
pip install -r requirements.txt --break-system-packages
```

Ya:

```bash
pip3 install -r requirements.txt --break-system-packages
```

---

#### **Option B: Virtual Environment (Best Method)**

1. Virtual environment banayein:

```bash
python3 -m venv venv
```

2. Activate karein:

```bash
source venv/bin/activate
```

Terminal prompt aisa nazar aayega:

```
(venv) user@DESKTOP:~/kiro-openai-gateway$
```

3. Dependencies install karein:

```bash
pip install -r requirements.txt
```

4. Server run karein:

```bash
python main.py
```

⚠️ Yaad rakhein: Har dafa project run karne se pehle virtual environment activate karein.

---

## 3. Python Command Not Found

### ❌ Masla:

```
Command 'python' not found
```

### 📸 Screenshot:
<img width="464" height="67" alt="image" src="https://github.com/user-attachments/assets/4229ae22-07d6-49ff-8486-ed58f0ed92b2" />

Ubuntu mein default `python` command available nahi hoti.

---

### ✅ Hal:

#### **Quick Fix**

Har jagah `python` ki jagah `python3` use karein.

```bash
python3 main.py
```

---

#### **Permanent Fix (Optional)**

Temporary alias:

```bash
alias python=python3
```

Permanent alias:

```bash
echo "alias python=python3" >> ~/.bashrc
source ~/.bashrc
```

---

## 4. Configuration Error - No Kiro Credentials

### ❌ Masla:

```
ERROR | No kiro credentials configured!
CONFIGURATION ERROR
```

### 📸 Screenshot:
<img width="463" height="214" alt="image" src="https://github.com/user-attachments/assets/1d6ec93c-d6b3-4832-a5d4-bca40ec35474" />


Yeh error tab aati hai jab `.env` file sahi configure na ho.

---

### ✅ Hal:

#### **Step 1: .env File Banayein**

```bash
cd ~/kiro-openai-gateway
cp .env.example .env
```

---

#### **Step 2: .env Edit Karein**

```bash
nano .env
```

---

#### **Step 3: Yeh Lines Uncomment Karein**

Dhoondhein:

```bash
# KIRO_CREDS_FILE="~/.aws/sso/cache/kiro-auth-token.json"
# PROXY_API_KEY="my-super-secret-password-123"
```

Inhe is tarah karein:

```bash
KIRO_CREDS_FILE="~/.aws/sso/cache/kiro-auth-token.json"
PROXY_API_KEY="my-super-secret-password-123"
```

---

#### **Step 4: File Save Karein**

* Ctrl + O
* Enter
* Ctrl + X

---

#### **Step 5: Kiro IDE Login Check Karein**

⚠️ Bohat Zaroori:

1. Kiro IDE open karein
2. Login karein
3. Credits verify karein

Kiro IDE ke baghair server kaam nahi karega.

---

## 5. Server Testing & Verification

### ✅ Server Successfully Start Hone Ki Nishani:

Jab:

```bash
python3 main.py
```

Run karein to yeh messages nazar aane chahiye:

```
INFO | Starting Uvicorn server...
INFO | Credentials loaded...
INFO | Model cache ready
INFO | Uvicorn running on http://0.0.0.0:8000
```

---

### 🌐 Browser Test

Browser mein open karein:

```
http://localhost:8000
```

⚠️ 0.0.0.0 use na karein.

---

### ✅ Success Response:

```json
{
  "status": "ok",
  "message": "Kiro Gateway is running"
}
```

---

### ❌ Agar Browser Error De

Server band karein:

```
Ctrl + C
```

Phir run karein:

```bash
python3 main.py --host 127.0.0.1
```

Phir browser mein:

```
http://127.0.0.1:8000
```

---

## 6. Final Setup Steps

### 📌 Complete Setup Sequence

---

#### Terminal 1: Gateway Server

```bash
cd ~/kiro-openai-gateway
python3 main.py
```

✅ Yeh terminal band nahi karna.

---

#### Terminal 2: Claude Code Router

Naya terminal open karein:

```bash
ccr start
ccr code
```

---

#### Test Message:

```
Hi! Can you confirm you're working?
```

---

#### Model Verify:

```bash
ccr model
```

---

### 🔄 Agar Kuch Kaam Na Kare

1. System restart karein
2. Kiro IDE login check karein
3. Gateway server check karein
4. Environment variables verify karein

---

## 📊 Quick Reference Commands

| Kaam                 | Command                          | Maqsad           |
| -------------------- | -------------------------------- | ---------------- |
| Auth token unset     | unset ANTHROPIC_AUTH_TOKEN       | Conflict solve   |
| Dependencies install | pip3 install -r requirements.txt | Packages install |
| .env create          | cp .env.example .env             | Config file      |
| .env edit            | nano .env                        | Settings change  |
| Gateway start        | python3 main.py                  | Server run       |
| Server test          | localhost:8000                   | Verify           |
| Router start         | ccr start                        | Router run       |
| Claude run           | ccr code                         | Claude use       |

---

## 🎉 Success Indicators

✅ Gateway server running
✅ Browser response OK
✅ ccr code working
✅ Claude responses mil rahe hain
✅ Kiro credits use ho rahe hain

---

## 🆘 Additional Help

Agar masla solve na ho:

1. Complete system restart karein
2. Steps dobara follow karein
3. Kiro credits check karein
4. GitHub issues check karein

---

### Important Files Locations

| File             | Path                                  |
| ---------------- | ------------------------------------- |
| Kiro credentials | ~/.aws/sso/cache/kiro-auth-token.json |
| Gateway config   | ~/kiro-openai-gateway/.env            |
| Router config    | ~/.claude-code-router/config.json     |
| Shell config     | ~/.bashrc                             |

---

## ⚠️ Common Mistakes

❌ Gateway server band kar dena
❌ Kiro IDE logout hona
❌ .env ghalat configure karna
❌ python ki jagah python3 na use karna
❌ Environment variables verify na karna

---

## 💡 Pro Tips

✅ Gateway server ke liye alag terminal use karein
✅ Virtual environment use karein
✅ Kiro IDE login rakhein
✅ Credits check karte rahein
✅ Browser se server test karein

---

**Document Banaya:** Claude AI
**Date:** February 5, 2026
**Version:** 1.0
**Language:** Roman Urdu

