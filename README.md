# ssm
How to SSM into your aws instance


1. Install AWS CLI
Debian:
```
sudo apt update
sudo apt install awscli -y
```

Done.

2. Install SSM Session Manager Plugin
Without this, start-session throws errors.
```
sudo apt install session-manager-plugin -y
```

If Debian’s repo doesn’t have it (some versions don’t), then:
 
```
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o session-manager-plugin.deb
```
(If you’re on ARM, use ubuntu_arm64.) 

If that doesnt work, download it manually.

Install it:
```
sudo dpkg -i session-manager-plugin.deb
sudo apt-get install -f -y   # fix any missing deps
```

Verify:

```
session-manager-plugin --version
```

3. Configure AWS CLI
```
aws configure
```

It will ask for:

AWS Access Key ID

AWS Secret Access Key

Default region (like ap-south-1)

Output (just press enter)

This step is mandatory. No credentials, no SSM, no magic.

4. Make sure the machine you want to connect to is actually registered
If it’s an EC2 instance, it needs:

SSM agent running

IAM role: AmazonSSMManagedInstanceCore

If it’s a Hybrid Activation machine, you need to register it.

5. Start the session
```
aws ssm start-session --target <instance-id or managed-instance-id>
```

That’s the whole setup.
Nothing fancy. Nothing mystical. Just install CLI, install plugin, configure credentials, start a session.
