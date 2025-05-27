# 🛡️ AWS WAF Implementation Using Honeypot Intelligence (Part 2)

This project is a follow-up to my [AWS Honeypot Deployment & Attack Analysis (Part 1)](https://github.com/RichGerg/aws-honeypot-attack-analysis). After collecting over 670,000 events using the T-Pot honeypot on AWS EC2, I leveraged the data to build and test a **Web Application Firewall (WAF)** using AWS services to block malicious IPs, suspicious behavior, and reduce overall threat traffic by over 99%.

---

## 📌 Objective

Analyze honeypot data collected over 10 days and design a WAF with custom rules to block known attackers, high-frequency scanning tools, and IPs from high-risk countries — improving system security and reducing attack volume in real time.

---

## 🔍 T-Pot Honeypot Insights (10-Day Summary)

- 📊 **Total Events Logged**: 670,000+
- 🌐 **Unique IPs Detected**: 6,400+
- ⚠️ **Known Attackers Identified**: 88% of IPs
- 🗺️ **Top Attacker Countries**:
  - India (18%)
  - Vietnam (14%)
  - China (13%)
  - USA (12%)
  - Russia (10%)
- 🧪 **Top Scanning Tool**: ZGrab (~86% of events)
- 🔒 **Top Targeted Ports**:
  - 445 – File Sharing / Active Directory
  - 53 – DNS
  - 5900 – VNC (Remote Desktop)
  - 547 – DHCPv6
  - 80 – HTTP/Web Server

![Mock](https://www.phishy.cloud/assets/img/proj/mock9.jpg)

---

## 🛠️ Tools & Technologies

- AWS WAF (Web Application Firewall)
- AWS ALB (Application Load Balancer)
- AWS EC2
- T-Pot Honeypot Framework
- Custom Inbound Rules
- Linux / Networking

---

## ⚙️ Implementation Steps

### 1. 🔀 Create Application Load Balancer (ALB)
The ALB was configured to distribute incoming traffic between WAF rules and the honeypot server, acting as a controlled entry point.

### 2. 🧱 Create WAF & Custom Rules
Three test rules were designed based on honeypot insights:
- **Rule A**: Block top 10 known malicious IPs
- **Rule B**: Block IPs from high-risk countries (excluding the U.S.)
- **Rule C**: Block any IP that sends over 500 requests in 5 minutes

> ⚠️ *Note*: Blocking entire countries may not be practical in real-world environments where users, VPNs, or contractors reside in those regions. Adjust rules based on operational requirements.

### 3. 🔗 Associate WAF with ALB
The WAF was linked to the Application Load Balancer to begin filtering and responding to malicious traffic.

![Mock](https://www.phishy.cloud/assets/img/proj/mock11.jpg)

### 4. 🔄 Connect ALB to EC2 Instance
Security group rules were updated so the ALB could forward filtered traffic to the EC2-based honeypot instance.

### 5. 📉 Monitor & Analyze Results
After WAF deployment:
- **Pre-WAF**: ~5,000 events/hour
- **Post-WAF**: ~50 events/hour  
→ **📉 99% Reduction** in attack activity

![Mock](https://www.phishy.cloud/assets/img/proj/mock10.jpg)

---

## 🧠 Challenges & Lessons Learned

A major learning curve was understanding how the **Application Load Balancer** fits into the WAF-to-EC2 traffic flow. After consulting AWS documentation and tutorials, the architecture became clearer and easier to implement. This experience helped solidify my knowledge of how layered defenses can be built and tested in cloud environments.

---

## ✅ Conclusion

This project demonstrated how actionable insights from a honeypot can directly inform the design of modern, cloud-native defensive systems like AWS WAF. Real-time monitoring, traffic shaping, and intelligent blocking helped dramatically reduce system noise and potential threats.

Due to resource costs (18 Docker containers on a `t3.xlarge` instance with 128 GB storage), the honeypot has been paused. However, this experience has provided deep insight into **attack detection**, **traffic behavior**, and **cloud-based mitigation** strategies.

---

## 🔗 Related Projects

- 📡 [AWS Honeypot Deployment & Attack Analysis](https://github.com/RichGerg/aws-honeypot-attack-analysis)

---

## 📄 License

This project is open source under the [MIT License](LICENSE).

---

## ✉️ Credits

[T-Pot](https://github.com/telekom-security/tpotce) by Deutsche Telekom Security GmbH and walkthrough by RichGerg - Honeypot-driven AWS WAF setup to reduce malicious traffic through intelligent, real-world attack analysis.
