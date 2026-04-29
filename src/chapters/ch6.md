# Chapter 6: System Maintenance & Task Automation
# හයවන පරිච්ඡේදය: පද්ධති නඩත්තුව සහ ස්වයංක්‍රීයකරණය

---

## 6.1 The Philosophy of Continuous Upkeep
## 6.1 අඛණ්ඩ නඩත්තුවේ දර්ශනය

**[English]**

For a CTO, a server is not a "set and forget" asset. In the **Ravana-X** infrastructure, reliability is maintained through proactive cycles. If we ignore maintenance, technical debt accumulates, leading to catastrophic failure in our energy grid monitoring.

We utilize **Unattended Upgrades** to ensure that critical security patches are applied automatically. However, for core engine updates like PostgreSQL or AI models, we schedule maintenance windows. This balance between automation and human oversight is the key to managing hundreds of nodes across the island.

**[සිංහල]**

තාක්ෂණික ප්‍රධානියෙකුට සේවාදායකයක් යනු එක්වරක් සකසා අමතක කර දැමිය හැකි දෙයක් නොවේ. **Ravana-X** ව්‍යුහය තුළ විශ්වාසනීයත්වය පවතින්නේ ක්‍රමානුකූල නඩත්තු චක්‍ර මතය. අප නඩත්තු කටයුතු නොසලකා හැරියහොත්, එය තාක්ෂණික දෝෂ එකතු වීමට හේතුවන අතර, අවසානයේ බලශක්ති පද්ධතිය අඩාල වීමට පවා ඉඩ ඇත.

අත්‍යවශ්‍ය ආරක්ෂණ යාවත්කාලීන කිරීම් සඳහා අප **Unattended Upgrades** පද්ධතිය භාවිතා කරමු. නමුත් දත්ත සමුදායන් හෝ AI ආකෘති වැනි ප්‍රධාන කොටස් යාවත්කාලීන කරන්නේ සැලසුම් සහගත නඩත්තු කාල සීමාවන් තුළදීය. දිවයින පුරා විසිරී ඇති ඒකක සිය ගණනක් කළමනාකරණය කිරීමේ රහස වන්නේ මෙම ස්වයංක්‍රීයකරණය සහ මානව අධීක්ෂණය අතර ඇති සමබරතාවයයි.

---

## 6.2 Automation with Cron & Systemd Timers
## 6.2 Cron සහ Systemd Timers හරහා ස්වයංක්‍රීයකරණය

**[English]**

Automation is the silent engineer of Ravana-X. We use **Cron** for traditional repetitive tasks, such as clearing temporary buffers from generator logs. However, for more complex workflows—like syncing medical data at specific intervals—we prefer **Systemd Timers**. 

Systemd Timers are superior because they provide better logging and dependencies; for instance, a timer can be set to only run if the network is active. This prevents error logs from filling up the disk if a remote node in Doloswela Kanda loses its uplink.

**[සිංහල]**

ස්වයංක්‍රීයකරණය යනු Ravana-X පද්ධතියේ නිහඬ ඉංජිනේරුවායි. විදුලි ජනක යන්ත්‍රවල තාවකාලික දත්ත ගොනු පිරිසිදු කිරීම වැනි සරල කාර්යයන් සඳහා අප **Cron** භාවිතා කරමු. නමුත් වෛද්‍ය දත්ත හුවමාරුව වැනි සංකීර්ණ කාර්යයන් සඳහා අප **Systemd Timers** භාවිතා කිරීමට කැමැත්තක් දක්වමු.

Systemd Timers වඩාත් දියුණු වන්නේ ඒවා මගින් වඩා හොඳ වාර්තාකරණයක් (Logging) සහ පරායත්තතාවයක් (Dependencies) ලබා දෙන බැවිනි. උදාහරණයක් ලෙස, ජාලය සක්‍රීයව පවතින විට පමණක් දත්ත යැවීමට මෙහිදී නියම කළ හැක. එමගින් දුරස්ථ ඒකකයක ජාලය බිඳ වැටී ඇති අවස්ථාවක අනවශ්‍ය දෝෂ වාර්තා (Error logs) වලින් දෘඩ තැටිය පිරීම වළක්වයි.

---

## 6.3 Log Rotation: Managing Metadata
## 6.3 Log Rotation: දත්ත වාර්තා කළමනාකරණය

**[English]**

A 10kW generator node generates massive amounts of metadata. Without **Logrotate**, the `/var/log` partition would overflow in days. We configure specialized policies to compress old logs and keep only the last 30 days of high-resolution data on the field node, while archiving long-term summaries to our central Citus cluster.

**[සිංහල]**
10kW විදුලි ජනක ඒකකයකින් විශාල දත්ත වාර්තා ප්‍රමාණයක් නිපදවයි. **Logrotate** ක්‍රමය භාවිතා නොකළහොත් දින කිහිපයක් ඇතුළත දෘඩ තැටියේ ඉඩ පිරී යනු ඇත. අප කරන්නේ පැරණි වාර්තා හැකිලීම (Compress) සහ දින 30ක දත්ත පමණක් ඒකකය තුළ තබා ගැනීමයි. දීර්ඝකාලීන දත්ත වාර්තා අපගේ මධ්‍යම Citus දත්ත ගබඩාව වෙත ස්වයංක්‍රීයව යොමු කරනු ලැබේ.

```bash
# Force a log rotation for testing (පරීක්ෂා කිරීම සඳහා)
sudo logrotate -f /etc/logrotate.conf

# Check disk usage of logs (ලොග් ගොනුවල ඉඩ පරීක්ෂාව)
du -sh /var/log/
