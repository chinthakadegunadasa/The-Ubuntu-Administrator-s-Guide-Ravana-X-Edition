
# Chapter 5: Advanced Package Management
# පස්වන පරිච්ඡේදය: උසස් මෘදුකාංග පැකේජ කළමනාකරණය

---

## 5.1 The Lifecycle of Software
## 5.1 මෘදුකාංගයක ජීවන චක්‍රය

**[Humanized English]**
In a production environment like **Ravana-X**, we do not simply "install" software; we manage its entire lifecycle. Ubuntu uses the **Advanced Package Tool (APT)** to handle dependencies and ensure system integrity. 

As a CTO, you must distinguish between the stability of the core OS and the agility of specialized applications. While we rely on `apt` for the hardened Linux kernel and libraries, we utilize **Snaps** for containerized, self-updating engineering tools that need to be isolated from the base system. This hybrid approach ensures that a medical app update never breaks the underlying energy monitoring service.

**[සිංහල]**
**Ravana-X** වැනි සජීවී පද්ධතියකදී අප කරන්නේ හුදෙක් මෘදුකාංග ස්ථාපනය කිරීම පමණක් නොව, එහි සමස්ත ජීවන චක්‍රයම කළමනාකරණය කිරීමයි. මෘදුකාංග අතර ඇති අන්තර්-සම්බන්ධතා (Dependencies) හැසිරවීමට සහ පද්ධතියේ ස්ථාවරත්වය සුරැකීමට Ubuntu විසින් **Advanced Package Tool (APT)** භාවිතා කරයි.

තාක්ෂණික ප්‍රධානියෙකු ලෙස, ඔබ මෙහෙයුම් පද්ධතියේ ස්ථායීතාවය සහ විශේෂිත මෘදුකාංගවල වේගවත් බව අතර වෙනස හඳුනාගත යුතුය. Linux කර්නලය වැනි මූලික කොටස් සඳහා අප `apt` භාවිතා කරන අතර, ප්‍රධාන පද්ධතියෙන් වෙන්ව තබාගත යුතු විශේෂිත ඉංජිනේරු මෙවලම් සඳහා **Snaps** තාක්ෂණය භාවිතා කරමු. මෙම දෙමුහුන් ක්‍රමය නිසා, වෛද්‍ය යෙදුමක යාවත්කාලීන කිරීමක් මගින් බලශක්ති පද්ධතියට බාධාවක් වීම වළක්වයි.

---

## 5.2 Managing Private Repositories
## 5.2 පෞද්ගලික මෘදුකාංග ගබඩා කළමනාකරණය

**[Humanized English]**
To maintain **Digital Sovereignty**, we do not rely solely on public mirrors. For Ravana-X, we host our own **Local APT Repository**. This allows us to:
1. **Audit Packages:** Every update is tested in a sandbox before being pushed to the field nodes.
2. **Bandwidth Efficiency:** 10kW nodes in remote areas like Doloswela Kanda sync with a local mirror rather than consuming international bandwidth.
3. **Custom Versions:** We can pin specific versions of PostgreSQL or Citus that are certified for our unique hardware.

**[සිංහල]**

**ඩිජිටල් ස්වෛරීභාවය** තහවුරු කිරීම සඳහා අප පොදු මෘදුකාංග ගබඩා මත පමණක් යැපෙන්නේ නැත. Ravana-X ව්‍යාපෘතිය සඳහා අප අපගේම **දේශීය APT මෘදුකාංග ගබඩාවක්** පවත්වාගෙන යමු. එමගින්:
1. **පරීක්ෂා කිරීම:** සෑම යාවත්කාලීන කිරීමක්ම ක්ෂේත්‍ර ඒකක වෙත යැවීමට පෙර ආරක්ෂිතව පරීක්ෂා කළ හැක.
2. **කලාප පළල සුරැකීම:** දොලොස්වෙල කන්ද වැනි දුරස්ථ ප්‍රදේශවල ඇති ඒකක, අන්තර්ජාලය වෙනුවට දේශීය ජාලය හරහා දත්ත ලබා ගනී.
3. **විශේෂිත සංස්කරණ:** අපගේ දෘඩාංග සඳහා වඩාත්ම සුදුසු PostgreSQL හෝ Citus සංස්කරණ ස්ථාවරව පවත්වා ගැනීමට අපට හැකියාව ලැබේ.

---

## 5.3 Essential Commands for the Architect
## 5.3 ඉංජිනේරු සැලසුම්කරුවෙකුට අවශ්‍ය ප්‍රධාන විධාන

**[English]**

Managing thousands of nodes requires precision. We use `apt-mark hold` to prevent critical database engines from upgrading automatically during a maintenance window, ensuring we only upgrade when the CTO office gives the "Green Light."

**[සිංහල]**

ඒකක දහස් ගණනක් කළමනාකරණය කිරීමේදී නිරවද්‍යතාවය අත්‍යවශ්‍ය වේ. පද්ධති නඩත්තු කාලයකදී දත්ත සමුදායන් ස්වයංක්‍රීයව යාවත්කාලීන වීම වැළැක්වීමට අප `apt-mark hold` විධානය භාවිතා කරමු. එමගින් යාවත්කාලීන කිරීම් සිදුවන්නේ තාක්ෂණික අංශයේ පූර්ණ අනුමැතිය ඇතිව පමණි.

```bash
# Pinning the PostgreSQL version (සංස්කරණය ස්ථාවරව තබා ගැනීම)
sudo apt-mark hold postgresql-16

# Checking for security-only updates (ආරක්ෂණ යාවත්කාලීන කිරීම් පරීක්ෂාව)
apt list --upgradable | grep security

# Cleaning the cache to save space on Edge units (ඉඩ ඉතිරි කර ගැනීම)
sudo apt clean && sudo apt autoremove
