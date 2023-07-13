---
description: Docker & Lilypad, Private Key
---

# Install Run Requirements

## Install Requirements

### **Install Docker**

{% hint style="info" %}
[Docker](https://www.docker.com/products/docker-desktop/) :whale: installed
{% endhint %}

### **Install Lilypad CLI in your terminal / command line**

{% code overflow="wrap" %}
```bash
curl -sSL -O https://bit.ly/get-lilypad && sudo install get-lilypad /usr/local/bin/lilypad
```
{% endcode %}

### **Add your private key to your terminal / command line instance:**

Get your private key from metamask: Accounts -> Account Details -> Show private key

<div>

<figure><img src="../../.gitbook/assets/Screenshot 2023-07-13 at 2.31.17 pm.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../../.gitbook/assets/Screenshot 2023-07-13 at 2.31.25 pm.png" alt=""><figcaption></figcaption></figure>

</div>

Set your private key in terminal

```bash
export PRIVATE_KEY=<the private key you copied>
```

You can verify you have set it with:

```bash
echo $PRIVATE_KEY
```

