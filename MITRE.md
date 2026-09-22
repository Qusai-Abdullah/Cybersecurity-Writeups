
The [MITRE ATT&CK®](https://attack.mitre.org/)
framework is "a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations. The ATT&CK knowledge base is used as a foundation for the development of specific threat models and methodologies in the private sector, in government, and in the cyber security product and service


- [Tactic(opens in new tab)](https://attack.mitre.org/tactics/enterprise/): An adversary's goal or objective. The “why” of an attack.
- [Technique(opens in new tab)](https://attack.mitre.org/techniques/enterprise/): How an adversary achieves their goal or objective.
- Procedure: The implementation or how the technique is executed.

1. **Tactic**: Let's say that an attacker wants to perform Reconnaissance on their target. This is the attacker's goal.
2. **Technique**: They may utilize the Active Scanning technique. This is how they achieve their Reconnaissance goal.
3. **Sub-technique**: Active Scanning comprises three specific methods: Scanning IP Blocks, Vulnerability Scanning, or Wordlist Scanning.
![](Attachments/Pasted%20image%2020260709231853.png)



<mark style="background: #FF5582A6;">## Why ATT&CK Matters?</mark>
ATT&CK provides cyber security professionals and organizations with a standard and consistent language for describing adversary behavior. In your cyber learning journey, you’ve probably seen the same action or technique referred to by several different names. By providing standard terminology and unique IDs, the framework makes it easier to compare data and incidents, enabling effective communication across the security community.

ATT&CK also helps bridge the gap between threat intelligence and defensive operations.


<mark style="background: #FF5582A6;">**Who Uses ATT&CK?**</mark>
1. ![](Attachments/Pasted%20image%2020260709234607.png)

- ** what is MITRE ATT&CK Navigator tool ?**.





 what is the MITRE ATT&CK Groups؟ هي صفحات توثق مجموعات التهديدات السيبرانية، أسمائها ?  المختلف?، تقنياتها، أدواتها، وحملاتها لمساعدة المحللين في فهم سلوك المهاجمين واكتشافهم.




**هدف صفحة Groups في MITRE ATT&CK:**

- توثيق **من هم المهاجمون** (Threat Groups).
- معرفة **الأساليب والتقنيات (TTPs)** التي يستخدمونها.
- ربطهم بالـ **Malware / Tools** التي يستخدمونها.
- ربط نشاطهم بالحملات (Campaigns).
- مساعدة المحللين على اكتشاف الهجمات والدفاع ضدها.




**MITRE CAR (Cyber Analytics Repository)**
هو عبارة عن **قاعدة معرفة (Knowledge Base)** تحتوي على قواعد وتحليلات جاهزة لاكتشاف سلوك المهاجمين.
بمعنى أبسط:

> MITRE CAR هو مكتبة تحتوي على أفكار وقواعد Detection تساعد المدافعين على اكتشاف تقنيات المهاجمين التي وصفها MITRE ATT&CK.
### <mark style="background: #FF5582A6;">MITRE CAR</mark>...?: 
This all sounds a bit complex, so let's break it down. CAR is a collection of ready-made detection analytics built around ATT&CK. Each analytic describes how to detect an adversary's behavior
This is key because it allows you to identify the patterns you should look for as a defender. CAR also provides example queries for common industry tools such as Splunk, so you, as a defender, can translate ATT&CK TTPs into real detections.
https://car.mitre.org/ for visit it 
CAR is a repository of security detection analytics built around MITRE ATT&CK. It provides detection analytics and ready-made rules that help analysts translate adversary techniques (TTPs) into real-world detections using tools such as Splunk and EQL.

يقول لك:

"إذا كان المهاجم يستخدم هذه التقنية، كيف أكتشفه؟"

مثال:

ATT&CK يقول:

> Technique: Scheduled Task (T1053)

CAR يقول:

> ابحث عن إنشاء Scheduled Task ثم راقب الملفات التي يتم الوصول إليها بعدها.



that is mean >> 
ATT&CK = سلوك المهاجم  
CAR = طريقة اكتشاف هذا السلوك



<mark style="background: #FF5582A6;">ATT&CK</mark>  give you the attacker use the PowerShell 
 CAR give you how to monitor the PowerShell 



<mark style="background: #FF5582A6;">## 1. MITRE ATT&CK (القاموس الهجومي)
</mark>
- **ما هو؟** هو موسوعة تشرح **ماذا يفعل الهكر**؛ فهو يركز بالكامل على سلوك المهاجمين وتكتيكاتهم.
    
- **فكرته:** يخبرك بـ "التقنيات" التي يستخدمها المخترق للدخول والتحرك داخل الشبكة (مثل: كيف يخترق الحسابات السحابية `T1078.004`).
    
- **الخلاصة:** يجيبك على سؤال: **"كيف يفكر ويتحرك العدو؟"**
    

<mark style="background: #FF5582A6;">## 2. MITRE D3FEND (الخريطة الدفاعية)</mark>

- **ما هو؟** هو الإطار المقابل والمكمل لـ ATT&CK، ولكنه يركز بالكامل على **ماذا يفعل المدافع (Blue Teamer)**.
    
- **فكرته:** يعطيك استراتيجيات وهندسة دفاعية لمواجهة هجمات ATT&CK (مثل استراتيجية `DET0546` التي بحثنا عنها). هو لا يعطيك كوداً برمجياً، بل يعطيك "المفهوم الهندسي" لكيفية الكشف أو الحماية (مثلاً: مراقبة الـ API، أو تحليل سلوك الحسابات).
    
- **الخلاصة:** يجيبك على سؤال: **"ما هي الاستراتيجية أو المفهوم الدفاعي الذي أحتاجه لأصُد هذا الهجوم؟"**
    

<mark style="background: #FF5582A6;">## 3. MITRE CAR (المستودع التطبيقي لـ الكود والـ Queries)
</mark>
- **ما هو؟** اختصار لـ _(Cyber Analytics Repository)_. هذا هو المكان الذي تجد فيه **الكود الفعلي والـ Analytics الصريحة** التي تطبقها في بيئتك.
    
- **فكرته:** يترجم لك مفاهيم الـ D3FEND إلى "معادلات وأكواد كشف" حقيقية جاهزة للاستخدام (مثل كود Splunk SPL، أو لغة سيكما Sigma، أو Elastic Security queries).
    
- **الخلاصة:** يجيبك على سؤال: **"ما هو الكود أو الـ Query الفعلي الذي سأكتبه في الـ SIEM لتنفيذ الكشف؟"**
    

### مثال عملي يربط الثلاثة معاً (لتتضح الصورة تماماً):

> - **ATT&CK يخبرك:** الهكر يقوم بـ "تعديل في سجلات الويندوز (Registry Run Keys) ليضمن بقاءه في الجهاز".
>     
> - **D3FEND يخبرك:** الاستراتيجية الدفاعية الصحيحة هنا هي عمل **Process Spawn Analysis** (تحليل للعمليات التي تنبثق وتعدل السجل).
>     
> - **CAR يخبرك:** إليك الكود الفعلي (مثلاً بلغة سيكما) الذي يبحث عن العمليات التي تعدل مسار الـ Registry المحدد.
>




Situational Awareness     فهم البيئه او الاشياء او اي شي يحدث داخل البيئه 




With MITRE ATT&CK, you learn how attacks happen, but with MITRE D3FEND, you discover how to stop them.


<mark style="background: #FF5582A6;">User Behavior Analysis (UBA) ?</mark>  https://d3fend.mitre.org/technique/d3f:UserBehaviorAnalysis/
Analyzing user behavior to see if their actions are normal or indicate a threat.
![](Attachments/Pasted%20image%2020260710220423.png)





---

# 4. Adversary Emulation Plans
https://github.com/center-for-threat-informed-defense/adversary_emulation_library

## Definition

MITRE Adversary Emulation Plans are step-by-step guides that simulate real-world threat actor behavior.

They allow security teams to replicate attacks performed by known threat groups.

---

## Purpose

Used for:

- Defense validation
- Purple team exercises
- SOC training
- Detection testing

---

## Example

A threat group uses:

```
PowerShell
Credential Dumping
Remote Services
Data Collection
```

The emulation plan recreates these behaviors to test whether defenses detect them.

---

# 5. MITRE Caldera
https://caldera.mitre.org/

## Definition

MITRE Caldera is an automated adversary emulation platform designed to test security defenses using ATT&CK-based attack simulations.

---

## How Caldera Works

Caldera consists of:

### Server

Controls and manages operations.

### Agents

Execute actions inside the testing environment.

### Abilities

Predefined attack actions mapped to ATT&CK techniques.

---

## Example Operation

Caldera can simulate:

```
PowerShell Execution
        ↓
Credential Access
        ↓
Lateral Movement
        ↓
Data Collection
```

The security team then verifies whether monitoring tools detect these activities.

---

## Uses

- Red Team Testing
- Blue Team Validation
- SOC Detection Testing
- Purple Team Exercises

---

# 6. MITRE ATLAS
https://atlas.mitre.org/matrices/ATLAS

## Definition

MITRE ATLAS (Adversarial Threat Landscape for Artificial Intelligence Systems) is a knowledge base focused on threats targeting Artificial Intelligence and Machine Learning systems.

---

## Purpose

ATLAS documents:

- AI attack techniques
- Vulnerabilities
- Mitigation strategies

---

## Examples of AI Threats

### Data Poisoning

Attackers manipulate training data to affect model behavior.

---

### Model Evasion

Attackers modify inputs to bypass AI detection.

---

### Prompt Injection

Attackers manipulate AI instructions to cause unintended behavior.

---

### Model Extraction

Attackers attempt to recreate an AI model.

---

# 7. MITRE AADAPT     
https://aadapt.mitre.org/

## Definition

AADAPT (Adversarial Actions in Digital Asset Payment Technologies) is a MITRE knowledge base focused on threats targeting digital asset systems.

---

## Focus Areas

Includes:

- Blockchain systems
- Cryptocurrency platforms
- Digital wallets
- Smart contracts

# الفرق بين هذه المكتبة و MITRE Caldera

هذا مهم جدًا:

## Adversary Emulation Library

هي:

```
الخطة
```

يعني:

"كيف يتصرف المهاجم؟"

---

## MITRE Caldera

هو:

```
التنفيذ الآلي
```

يعني:

"نفذ هذه الخطة على بيئة اختبار"

---

العلاقة:

```
Adversary Emulation Library

          |
          |
          v

     Caldera

          |
          |
          v

 Execute Simulation
```


