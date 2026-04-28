# Chapter 2: The Ravana-X Architectural Vision
# දෙවන පරිච්ඡේදය: Ravana-X සැලසුම්කරණ දැක්ම

---

## 2.1 Engineering for Sovereignty
## 2.1 ස්වෛරීභාවය සඳහා වූ ඉංජිනේරු විද්‍යාව

**[English]**

As a CTO, I view infrastructure not just as a collection of servers, but as a statement of independence. The **Ravana-X** project was born from the necessity to manage Sri Lanka’s energy and medical data within our own borders, using tools we control entirely. 

The architecture is built on a "Decentralized Core" model. Each 10kW electricity generator node is an autonomous unit, capable of running its own AI diagnostics and database shards, yet perfectly synchronized with our central cluster. This resilience ensures that even if a sub-network is isolated, the nation's power grid remains intelligent and secure.

**[සිංහල]**

තාක්ෂණික ප්‍රධානියෙකු ලෙස මා යටිතල පහසුකම් දකින්නේ හුදෙක් සේවාදායක සමූහයක් ලෙස නොව, අපගේ ස්වාධීනත්වයේ ප්‍රකාශනයක් ලෙසය. **Ravana-X** ව්‍යාපෘතිය බිහිවූයේ අපගේ බලශක්ති සහ වෛද්‍ය දත්ත, අපට සම්පූර්ණ පාලනය ඇති මෙවලම් භාවිතා කරමින් අපගේ දේශසීමා තුළම කළමනාකරණය කිරීමේ අවශ්‍යතාවය මතය.

මෙහි ව්‍යුහය ගොඩනගා ඇත්තේ "විමධ්‍යගත හරය" (Decentralized Core) ආකෘතිය මතය. සෑම 10kW විදුලි ජනක ඒකකයක්ම ස්වාධීන ඒකකයක් වන අතර, ඒවාට තමන්ගේම AI පරීක්ෂණ සහ දත්ත කොටස් (Shards) හැසිරවීමට හැකියාව ඇත. යම් හෙයකින් අනු-ජාලයක් හුදකලා වුවද, ජාතික විදුලි පද්ධතියේ ආරක්ෂාව සහ බුද්ධිමත් ක්‍රියාකාරිත්වය මෙයින් සහතික කෙරේ.

---

## 2.2 The Technology Stack
## 2.2 තාක්ෂණික ස්තරය

**[English]**

To achieve this vision, we have selected a stack that prioritizes performance and open-source transparency:
1. **OS Layer:** Ubuntu 24.04 LTS (Noble Numbat) for its 12-year support window.
2. **Data Layer:** PostgreSQL with Citus for hyperscale distribution and Pigisty for industrial-grade management.
3. **Intelligence Layer:** Ubuntu AI (MicroK8s + Ollama) for local, private inference at the edge.
4. **Access Layer:** Apache Guacamole for secure, clientless remote engineering access.

**[සිංහල]**

මෙම දැක්ම සාක්ෂාත් කර ගැනීම සඳහා, අප කාර්යසාධනය සහ විවෘතභාවය මූලික කරගත් තාක්ෂණික මෙවලම් තෝරාගෙන ඇත:
1. **මෙහෙයුම් පද්ධතිය:** වසර 12ක සහය සහිත Ubuntu 24.04 LTS.
2. **දත්ත ස්තරය:** මහා පරිමාණ දත්ත බෙදා හැරීම සඳහා PostgreSQL/Citus සහ එය කළමනාකරණයට Pigisty.
3. **බුද්ධිමය ස්තරය:** දේශීයව AI ක්‍රියාත්මක කිරීම සඳහා Ubuntu AI (MicroK8s සහ Ollama).
4. **ප්‍රවේශ ස්තරය:** ආරක්ෂිත දුරස්ථ ප්‍රවේශය සඳහා Apache Guacamole.

---

## 2.3 Mapping Hela Logic to Neural Models
## 2.3 හෙළ න්‍යායයන් ස්නායුක ආකෘති සමඟ සැසඳීම

**[English]**

Our ancestors built systems—like the complex irrigation networks—that functioned as a single, living organism. In **Ravana-X**, we map these ancient "flow logics" to modern neural models. We don't just process data; we treat information flow like water in an *Elahera* canal—ensuring it reaches every node without waste or bottleneck. This is the synthesis of historical wisdom and 21st-century Linux engineering.

**[සිංහල]**

අපගේ පැරණි වාරි පද්ධතීන් මෙන්, මුළු පද්ධතියම එකම ජීවී ඒකකයක් ලෙස ක්‍රියා කරන අයුරින් අප මෙම ව්‍යුහය සකසා ඇත. **Ravana-X** හිදී අප මෙම පැරණි "ගලායාමේ න්‍යායයන්" (Flow logics) නූතන ස්නායුක ආකෘති සමඟ සමපාත කරමු. අප කරන්නේ දත්ත සැකසීම පමණක් නොවේ; තොරතුරු ගලායාම ඇළහැර ඇළේ ජලය මෙන් අපතේ යාමකින් හෝ බාධාවකින් තොරව සෑම ඒකකයකටම ගලා යන බව අප සහතික කරමු. මෙය ඓතිහාසික ප්‍රඥාව සහ 21 වන සියවසේ Linux ඉංජිනේරු විද්‍යාවේ සංකලනයයි.

---

### **Engineering Summary for the CTO**
### **පරිපාලක සාරාංශය**

* **Design Goal:** Zero Single Point of Failure.
  
* **Security Pillar:** Data must be encrypted at rest and in transit across all decentralized nodes.
  
* **Hela Resilience (ස්ථාවරත්වය):** Just as the **Jetavanaramaya** stands on a foundation designed to distribute immense weight evenly, our **Citus-sharded database** distributes the weight of national data to ensure structural integrity and speed.
  
