# KaliVM
Step-by-step guide to setting up Kali Linux virtual machine in VirtualBox for cybersecurity labs, penetration testing practice, and hands-on security learning.

## 📋 Why I Built This

I wanted to truly understand virtual machines, not just what they are, but how they work under the hood. Setting up Kali Linux in VirtualBox became the perfect hands-on way to learn.

This VM serves as my personal cybersecurity lab environment. It gives me a safe, isolated space to:
- Practice Linux commands for TryHackMe and other platforms
- Experiment with security tools without risking my main system
- Build a foundation for my next project: an offline honeypot to study attack patterns

By doing this manually instead of using a pre-built VM, I learned about resource allocation, networking modes, and troubleshooting skills that copy-paste solutions don't teach.

## 📃 How Virtual Machines Work
A virtual machine (VM) relies on a hypervisor software that communicates with the host operating system to allocate resources like CPU, RAM, and storage. This creates a separate virtual environment that runs independently from the host.

Isolation & Security
While VMs provide strong isolation, they are not completely immune to threats. In rare cases, a virtual escape attack could allow malicious code to break out of the VM and affect the host. However, for most use cases, VMs offer excellent protection by containing potential threats within the isolated environment.

Key Advantages
- Strong isolation – Protects the host OS from most malware or experiments
- Snapshots – Allows you to save a VM state and revert back if something breaks
- Multi-OS support – Run Linux, Windows, or others simultaneously on one machine

Limitations:
- Resource intensive – VMs require more CPU, RAM, and storage than containers
- Slower setup – Each VM needs its own OS installation (separate ISO files)
- Storage overhead – Multiple VMs mean multiple full OS copies

Understanding these trade-offs helped me choose the right approach for future labs, where isolation and snapshots are more valuable than speed or efficiency.

## 🛠️ Tools & Technologies
- **VirtualBox 7.x** – Virtualization platform for creating and managing isolated VMs
- **Kali Linux** (2025.4 ISO) – Security focused OS used for the attacker machine
- **Windows 11 Pro** – Host environment
- **AI assisted diagnostics** – Leveraged large language models to interpret error messages and suggest troubleshooting paths during configuration challenges.
- **Windows Security (Defender)** – Configured folder exclusions to prevent the antivirus from flagging Kali's penetration testing tools as malicious.

## 📝 Step-by-Step Process

1. VM Platform Selection
Before starting this project, I evaluated my virtualization options. I chose VirtualBox because it's free and open-source, which aligned with my goal of building a lab without additional costs. While VMware offers more features and stability, the free version has limitations I preferred to avoid. For my use case, VirtualBox's trade-offs (occasional stability quirks) were acceptable.

2. Installation
Downloaded VirtualBox 7.x from the official website and installed it on my Windows 11 host.

3. OS Selection
I selected Kali Linux because I wanted to work in an environment that closely matches what cybersecurity professionals use in real-world penetration testing. Kali is more command-line-focused and less beginner-oriented, which pushes me to build habits and workflows that align with professional industry standards. Using Kali helps me get comfortable with the same tools, structure, and methodology I would encounter in a actual pentesting role.

4. Download Choice
I downloaded the Kali installer ISO (not the pre-built VM) from kali.org. Choosing the installer gave me control over resource allocation RAM, CPU cores, and storage, which the pre-built VM would have locked to default values.

5. Installation Process
Followed the graphical installer prompts. When asked about desktop environments, I researched GNOME and KDE (with AI assistance) and chose XFCE for its lightweight performance in a VM.

6. Network Verification
After installation, I confirmed internet connectivity:
```
ping -c 4 google.ca
```

7. System Updates
Ran updates to ensure the system had the latest packages:
```
sudo apt update && sudo apt upgrade -y
```

8. Stability Check
Powered off the VM, then restarted it to verify stability. The VM remained responsive with no boot issues.

9. Snapshot Creation
With a clean, updated system confirmed working, I created a VirtualBox snapshot. This allows me to experiment freely in the future if something breaks, I can revert to this known good state in seconds.

## 💡 Lessons Learned

### Virtual Machine Configuration
- **Resource allocation requires balance** – Over-allocating RAM/CPU to a VM can destabilize both the guest and host systems. Starting with conservative settings (2GB RAM, 2 cores) and scaling up only when needed proved more reliable than maximum allocations.
- **Configuration changes can introduce instability** – Modifying VM resources after creation sometimes caused boot failures. Taking snapshots before changes became essential.

### Security & Antivirus Considerations
- **Penetration testing tools trigger antivirus** – Windows Defender flagged Kali tools as malicious. Adding the VM folder to Defender's exclusion list prevented tool deletion without compromising host security.

### Troubleshooting Techniques
- **Installer ISOs offer more control than pre-built VMs** – The pre-built Kali VM crashed repeatedly; switching to a manual ISO install resolved stability issues and allowed custom resource allocation. Sometimes "easy" isn't better.

- **Guest Additions are essential** – Installing VirtualBox Guest Additions resolved mouse integration issues and enabled seamless display resizing.

- **Keyboard navigation is a fallback** – When the mouse froze during installation, using Tab, Space, and Enter allowed me to complete the setup.

- **Documentation gaps require cross-referencing** – A tutorial I followed for password recovery omitted the critical `mount -o remount,rw /` step. Using AI helped me identify this missing piece, reinforcing that understanding the *why* behind commands is as important as following steps.

- **Filesystem mounts matter in recovery** – Password changes in recovery mode fail if the filesystem is mounted read-only. Running `mount -o remount,rw /` before `passwd` ensures changes persist.

### Network Isolation
- **Internal networks create safe lab environments** – Configuring VMs to use VirtualBox's "Internal Network" mode allowed isolated communication between Kali and Ubuntu without internet exposure.

### Documentation Value
- **Documentation is as important as technical work** – Recording steps, issues, and solutions transformed this from a one-time setup into a reusable reference and portfolio piece.

## 📸 Screenshots

| Step | Screenshot | Description |
|:-----|:-----------|:------------|
| **Kali Installer** | <img width="400" alt="Kali Installer" src="https://github.com/user-attachments/assets/0ce3d3e9-d47b-45fa-9a3f-7468f60f7be4" /> | Starting the Kali Linux graphical installation process |
| **VM Configuration** | <img width="400" alt="Kali VM Specs" src="https://github.com/user-attachments/assets/b89068dd-c0bf-4899-a796-9d78839190f0" /> | Resource allocation: 2GB RAM, 2 cores, 100GB storage |
| **Kali Login** | <img width="400" alt="Kali Login" src="https://github.com/user-attachments/assets/70494f9c-278e-42f0-b5b2-5cb64ececc48" /> | Successful installation login screen ready |
| **Network Verification** | <img width="400" alt="Ping Test" src="https://github.com/user-attachments/assets/254c0401-c9d7-42ba-8853-bd98e6312cb5" /> | Confirming internet connectivity after install |
| **Snapshot Created** | <img width="400" alt="First Snapshot" src="https://github.com/user-attachments/assets/377172fa-b2b8-4b11-8a04-0fd6d288de84" /> | Clean state saved for future experiments |


