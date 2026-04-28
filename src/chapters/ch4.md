# Chapter 4: Automated Provisioning with Subiquity & Cloud-init
# සිව්වන පරිච්ඡේදය: Subiquity සහ Cloud-init හරහා ස්වයංක්‍රීය පද්ධති සම්පාදනය

---

## 4.1 Beyond Manual Installation
## 4.1 අතින් සිදුකරන ස්ථාපනයෙන් ඔබ්බට

**[Humanized English]**
As a Senior Architect, you know that consistency is the foundation of security. In the **Ravana-X** project, we cannot have engineers making individual choices during installation. We use **Subiquity**, Ubuntu's next-generation installer, to eliminate the "human variable." 

By using an `autoinstall.yaml` configuration, we define the exact DNA of a 10kW generator node—from its LVM partition layout to its pre-installed security headers. This ensures that a node deployed in Doloswela Kanda is a perfect digital twin of the one tested in our Colombo lab.

**[සිංහල]**

ජ්‍යෙෂ්ඨ සැලසුම් ශිල්පියෙකු ලෙස, ස්ථාවරත්වය යනු ආරක්ෂාවේ පදනම බව ඔබ දනී. **Ravana-X** ව්‍යාපෘතියේදී, ස්ථාපනය කරන අවස්ථාවේදී ඉංජිනේරුවන්ට තනි තනිව තීරණ ගැනීමට අප ඉඩ නොතබමු. ඒ වෙනුවට අප "මිනිස් සාධකය" ඉවත් කිරීම සඳහා Ubuntu හි නවීනතම **Subiquity** ස්ථාපන මෙවලම භාවිතා කරමු.

`autoinstall.yaml` ගොනුවක් භාවිතා කරමින්, 10kW ඒකකයක දත්ත ගබඩා සැකසුම් (LVM) සහ ආරක්ෂණ පද්ධති ඇතුළු සියලුම අංග අප නිවැරදිව අර්ථ දක්වන්නෙමු. එමගින් දොලොස්වෙල කන්දේ ස්ථාපනය කරන ඒකකය, කොළඹ පර්යේෂණාගාරයේ පරීක්ෂා කළ ඒකකයේම පරිපූර්ණ ඩිජිටල් පිටපතක් බව සහතික කෙරේ.

---

## 4.2 The Power of Cloud-init
## 4.2 Cloud-init හි ඇති ශක්තිය

**[Humanized English]**
While Subiquity handles the installation, **Cloud-init** handles the "awakening" of the server. It is the multi-distribution method for cross-platform cloud instance initialization. For Ravana-X, we use it to:
1.  **Inject SSH Keys:** Ensuring only authorized CTO-office keys can access the node.
2.  **Configure Network:** Setting up static IPs and VLANs for generator telemetry.
3.  **Run Bootcmd:** Executing final hardening scripts and connecting the node to the Pigisty monitoring cluster immediately upon first boot.

**[සිංහල]**
Subiquity මගින් ස්ථාපනය සිදු කරන අතරතුර, සේවාදායකය පණගැන්වීමේ (Awakening) කාර්යය සිදු කරන්නේ **Cloud-init** මගිනි. Ravana-X ව්‍යාපෘතියේදී අප මෙය පහත සඳහන් කාර්යයන් සඳහා භාවිතා කරමු:
1.  **SSH යතුරු ඇතුළත් කිරීම:** නිසි බලයලත් ඉංජිනේරුවන්ට පමණක් පද්ධතියට ප්‍රවේශ වීමට ඉඩ දීම.
2.  **ජාලකරණය:** දත්ත ලබා ගැනීම සඳහා අවශ්‍ය Static IP සහ VLAN සැකසුම් සිදු කිරීම.
3.  **Bootcmd ක්‍රියාත්මක කිරීම:** පද්ධතිය ආරම්භ වූ සැණින් එය ආරක්ෂිත කිරීම සහ Pigisty අධීක්ෂණ පද්ධතියට සම්බන්ධ කිරීම.

---

## 4.3 Practical: The Autoinstall Blueprint
## 4.3 ප්‍රායෝගිකව: Autoinstall සැලසුම් පත්‍රිකාව

**[Humanized English]**
To automate our deployment, we host the `user-data` file on a local web server. When the Ravana-X hardware boots via PXE or USB, it fetches this YAML and configures itself without a single keystroke.

**[සිංහල]**
අපගේ යෙදවීම් ස්වයංක්‍රීය කිරීම සඳහා අප `user-data` ගොනුව දේශීය වෙබ් සේවාදායකයක ගබඩා කරමු. Ravana-X දෘඩාංග පණගැන්වූ විට, එය මෙම YAML ගොනුව ලබාගෙන කිසිදු මිනිස් මැදිහත්වීමකින් තොරව ස්වයංක්‍රීයව පද්ධතිය සකස් කර ගනී.

```yaml
# Example snippet for Ravana-X Node
autoinstall:
  version: 1
  identity:
    hostname: ravana-node-01
    password: "$6$examp$dc6..."
    username: chinthaka
  ssh:
    install-server: true
    authorized-keys:
      - ssh-rsa AAAAB3Nza...
  storage:
    layout:
      name: lvm
