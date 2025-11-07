# signal-cli

# This is a little tutorial on howto set up signal-cli on the server.

Complete tutorial here: https://github.com/AsamK/signal-cli

But if you have never done it, here is the detailed step-by-step tutorial:

## 1. install java

```bash
sudo apt install default-jre
```

## 2. Install `signal-cli`

### 2.1. Set the version being installed

```bash
export VERSION=0.13.21
```

The latest version can be found here: https://github.com/AsamK/signal-cli/releases

### 2.2. Download binaries

```bash
wget https://github.com/AsamK/signal-cli/releases/download/v"${VERSION}"/signal-cli-"${VERSION}".tar.gz
```

### 2.3. Extract it

```bash
sudo tar xf signal-cli-"${VERSION}".tar.gz -C /opt
```
### 2.4. Install it

```bah
sudo tar xf signal-cli-"${VERSION}".tar.gz -C /opt
```
### 2.5. And create the link for the executable

```bash
sudo ln -sf /opt/signal-cli-"${VERSION}"/bin/signal-cli /usr/local/bin/
```
## 3. Register

```bash
signal-cli -a <your_number> register
```
This will send an SMS to your phone containing the verification code.

## 4. Generate captcha here:

https://signalcaptchas.org/registration/generate

## 5. Prove yourself using captcha

Prove you are a human using captcha. You can obtain the captcha code from the link "Open Signal" you get after you solve captcha. Just copy the link behind the "Open Signal" link text.

```bash
signal-cli -a <your_number> register --captcha signalcaptcha://signal-hcaptcha.5fad97ac-7d06-4e44-b18a-b950b20148ff.registration.P1_eyJ0eXAi......GnfMv0XOdvIC6JTFZSaA
```

## 6. Verify yourself

Now you can use the one-time code from SMS to verify yourself:

```bash
signal-cli -a <your_number> verify 123456
```
## 7. Now try to send the message

```bash
signal-cli -a <your_number> send -m "This is a message" <recipient_number>
```

The first number is your registered number and the second is the recipient.

## 8. Trust the recipient

You will probably get an error message like this:

```bash
Failed to send (some) messages:
<recipient_number>: Untrusted Identity for "<recipient_number>"
```

That is because you have to first trust your number. First, list the identities of the **RECIPIENT NUMBER**:

```bash
signal-cli -u <recipient_number> listIdentities
```

You will get multiple lines in this format

```bash
telephone_number UNTRUSTED Added: <some id> (2025-08-02T48:33:51.174Z) Fingerprint: <long fingerprint> Safety Number: <safety number>
```

You need to trust the recipient using that safety number:

```bash
signal-cli -u <your_number> trust <recipient_number> -v "<safety_number>"
```

## 9. Send a message

```bash
signal-cli -a <your_number> send -m "This is a message" <recipient_number>
```
