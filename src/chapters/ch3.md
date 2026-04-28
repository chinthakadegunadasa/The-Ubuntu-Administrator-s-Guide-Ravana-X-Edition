# Chapter 3: Strategic Deployment & Provisioning

# තුන්වන පරිච්ඡේදය: උපායමාර්ගික යෙදවීම සහ පද්ධති සම්පාදනය

---

## 3.1 The Deployment Philosophy
## 3.1 පද්ධති යෙදවීමේ දර්ශනය

**[Humanized English]**
In the **Ravana-X** project, we do not perform "manual installs." To ensure national-scale reliability, every field unit must be identical at the kernel level. As a CTO, I advocate for **Immutable Infrastructure**. This means we define the server's state in code (YAML), and the system builds itself automatically. 

Whether we are deploying a node in the Colombo data center or a remote 10kW generator unit in Doloswela Kanda, the process is hands-off. This eliminates human error and ensures that security patches are baked into the system from the first second of its life.

**[සිංහල]**
**Ravana-X** ව්‍යාපෘතියේදී අප "අතින් සිදුකරන ස්ථාපනයන්" (Manual installs) සිදු නොකරමු. ජාතික මට්ටමේ විශ්වාසනීයත්වය සහතික කිරීම සඳහා, සෑම ඒකකයක්ම කර්නල් මට්ටමින් එක හා සමාන විය යුතුය. තාක්ෂණික ප්‍රධානියෙකු ලෙස මා යෝජනා කරන්නේ "නොවෙනස්වන යටිතල පහසුකම්" (Immutable Infrastructure) ක්‍රමයයි. මෙහිදී අප කරන්නේ සේවාදායකයේ ස්වභාවය කේතයක් (YAML) හරහා අර්ථ දක්වා, පද්ධතිය ස්වයංක්‍රීයව ගොඩනැගීමට ඉඩ දීමයි.

කොළඹ දත්ත මධ්‍යස්ථානයේ හෝ දොලොස්වෙල කන්දේ 10kW ඒකකයක වුවද, මෙම ක්‍රියාවලිය සිදුවන්නේ ස්වයංක්‍රීයවය. එමගින් මිනිස් අතින් සිදුවන වැරදි අවම වන අතර, පද්ධතිය ආරම්භයේ සිටම ආරක්ෂණ යාවත්කාලීන කිරීම්වලින් සමන්විත බව සහතික කෙරේ.

---

## 3.2 Automated Provisioning Tools
## 3.2 ස්වයංක්‍රීය පද්ධති සම්පාදන මෙවලම්

**[English]**

To achieve this "Zero-Touch" deployment, we utilize the modern Ubuntu stack:
1. **Subiquity:** The next-generation installer that allows us to use an `autoinstall.yaml` file to pre-define disk partitions, network settings, and user accounts.
2. **Cloud-init:** The "industry standard" for cross-platform cloud instances, which we use to bootstrap our physical hardware, installing the Ravana-X custom repositories and SSH keys upon first boot.
3. **Netplan:** Our primary tool for defining complex network topologies (VLANs and Bridges) required for internal generator communication.

**[සිංහල]**
මෙම ස්වයංක්‍රීය යෙදවීම සඳහා අප නවීන Ubuntu මෙවලම් භාවිතා කරමු:
1. **Subiquity:** `autoinstall.yaml` ගොනුවක් හරහා තැටි බෙදීම් (Partitions) සහ ජාල සැකසුම් කල්තියා තීරණය කිරීමට ඉඩ සලසන නවීන ස්ථාපන මෙවලමයි.
2. **Cloud-init:** පළමු පණගැන්වීමේදීම (First boot) Ravana-X මෘදුකාංග ගබඩා සහ SSH යතුරු ස්ථාපනය කරමින් භෞතික දෘඩාංග සක්‍රීය කිරීමට මෙය භාවිතා කරයි.
3. **Netplan:** අභ්‍යන්තර සන්නිවේදනය සඳහා අවශ්‍ය සංකීර්ණ ජාල ව්‍යුහයන් (VLANs/Bridges) අර්ථ දැක්වීමට භාවිතා කරන ප්‍රධාන මෙවලමයි.

---

## 3.3 The Bare-Metal Blueprint
## 3.3 භෞතික දෘඩාංග සඳහා වූ සැලසුම

**[Humanized English]**
For our 10kW units, we leverage **MAAS (Metal-as-a-Service)**. This allows the CTO's office to manage thousands of physical servers as if they were virtual machines in a cloud. We can re-provision a failed node in the field remotely in under 10 minutes, ensuring the electricity grid's data flow is never interrupted for long.

**[සිංහල]**
අපගේ 10kW ඒකක සඳහා අප **MAAS (Metal-as-a-Service)** තාක්ෂණය භාවිතා කරමු. එමගින් භෞතික සේවාදායකයන් දහස් ගණනක් වුවද Cloud පද්ධතියක ඇති Virtual Machines මෙන් පහසුවෙන් පාලනය කිරීමට තාක්ෂණික අංශයට හැකියාව ලැබේ. ක්ෂේත්‍රයේ ඇති ඒකකයක් අක්‍රීය වුවහොත්, මිනිත්තු 10ක් ඇතුළත එය දුරස්ථව නැවත යථා තත්ත්වයට පත් කළ හැකි බැවින් දත්ත ගලායාම අඛණ්ඩව සිදු වේ.

---

### **Engineering Summary for the CTO**
### **පරිපාලක සාරාංශය**

* **Golden Image:** Never build from scratch in the field. Always deploy from a verified "Golden Image" or a tested Autoinstall script.
* **Network Sovereignty:** Use Netplan to isolate the generator's management network from the public internet.
* **Hela Resilience (සූදානම):** Our ancestors prepared the soil meticulously before building the great stupas. Similarly, we use **Subiquity and Cloud-init** to prepare the digital "soil" of our servers, ensuring the infrastructure we build upon it is unshakable.
* 
