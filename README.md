# Rsyslog-forwarding-
# 📡 Centralized Log Forwarding with Rsyslog

This repository provides a hands-on guide to configuring *Rsyslog* for centralized log forwarding on Linux systems. It includes configuration examples for both the *client (sender)* and the *central log server (receiver)* using TCP/UDP.

---

## 🧠 What is Rsyslog?

*Rsyslog* is a powerful and flexible logging system used to collect, filter, store, and forward log messages in Unix and Linux systems. It supports:

- ✔ High-performance log processing  
- ✔ Log forwarding via *UDP, **TCP, or **RELP*  
- ✔ Integration with *SIEM platforms* like *Splunk, **Elastic Stack, and **Graylog*  
- ✔ Custom filters, templates, and modules

---

## 🛠 Lab Environment

| Component | OS           | Role           | Example IP     |
|-----------|--------------|----------------|----------------|
| Server    | Ubuntu 20.04+| Log Receiver   | 192.168.1.10   |
| Client    | Ubuntu 20.04+| Log Sender     | 192.168.1.20   |

---

## 🧰 Tools Used

- 🔧 Rsyslog  
- 🔧 logger (log generator)  
- 🔧 tcpdump / Wireshark (for packet capture)  
- 🔧 Netdiscover / Nmap (for recon)

---

## ⚙ Setup Instructions

### 📤 On the Client (Log Sender)

1. *Edit Rsyslog configuration*:

```bash
sudo nano /etc/rsyslog.conf
Add this line to forward logs to the central server (UDP or TCP):

bash
Copy
Edit
. @@192.168.1.10:514     # Use @ for UDP, @@ for TCP
Restart Rsyslog service:

bash
Copy
Edit
sudo systemctl restart rsyslog
Test the setup:

bash
Copy
Edit
logger "🔐 Test log from Rsyslog client"
📥 On the Server (Log Receiver)
Enable Rsyslog to receive logs:

bash
Copy
Edit
sudo nano /etc/rsyslog.conf
Uncomment or add the following:

bash
Copy
Edit
module(load="imudp")
input(type="imudp" port="514")

module(load="imtcp")
input(type="imtcp" port="514")
Restart Rsyslog service:

bash
Copy
Edit
sudo systemctl restart rsyslog
Monitor logs:

bash
Copy
Edit
sudo tail -f /var/log/syslog
📂 Project Structure
bash
Copy
Edit
rsyslog-forwarding/
├── client/
│   └── rsyslog.conf         # Sample client config
├── server/
│   └── rsyslog.conf         # Sample server config
├── logs/
│   └── test-logs.txt        # Example log outputs
├── images/
│   └── rsyslog-diagram.png  # Optional architecture diagram
├── README.md
🔐 Security Tips
Use TLS for secure transport in production environments

Restrict ports using UFW/iptables

Monitor and alert on unusual log patterns

📊 Optional: SIEM Integration
✅ Splunk Universal Forwarder (UF)

✅ Elastic Stack (Beats + Logstash)

✅ Graylog Inputs

📚 Resources
Rsyslog Official Documentation


RFC 5424 - Syslog Protocol

✍ Author
Your Name : Shaikh Salman
384shaikhsalman@gmail.com
🔗 LinkedIn
📧 www.linkedin.com/in/
shaikh-salman-60524b324


