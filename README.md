Runner :)
Jab runner koi run karta hai us waqt bohot saari cheezein use effect karti hain:
Run context → us run ka environment ya situation (kis jagah se call aya, kis agent ke andar chal raha tha, etc.).
Parameters → jo inputs ya configuration run ko diye gaye the (jaise max tokens, temperature, etc.).
Model settings → kaunsa model use hua, kaunse version ke saath, aur uski specific settings.
Input data → user ne kya input diya tha us waqt.
Is tarah reproducibility (dobara reproduce karna) possible hoti hai, chahe environment badal bhi gaya ho ya future mein model ke naye versions aa gaye ho.
Benefit :)
User agar same sawal dobara poochhe → system us snapshot replay karega,
To exactly wohi jawab aayega jo pehle run me aya tha.
Tool Calls
Parallel Tool Calls → Multiple tools ek hi waqt me run hote hain.
Sequential Tool Calls → Tools ek ke baad ek run hote hain
Developer ka Role
Developer decide karta hai ke runner ko parallel tool calls allow karne hain ya sequential. Agar developer rule na de to runner khud need ke hisaab se manage karta hai.
Runner Parallel Tool Calls ko Limit Kyun Karta Hai?
Downstream services pe overload na ho.
Resource usage predictable rahe.
System stability aur reliability maintain ho.
Fair resource sharing ensure ho.
Multi-tenant system :)
Multi-tenant system wo hota hai jahan ek hi software / infrastructure ko multiple customers (tenants) use karte hain, lekin har tenant ka data aur context alag (isolated) rehta hai.
Quotas lagata hai → har tenant ko limited requests/resources milti hain.
Resource limits set karta hai → ek tenant zyada CPU/memory na use kar le.
Run context isolation karta hai → ek tenant dusre tenant ke data ya runs access nahi kar sakta.
🔹 input_filter 
is liye use hota hai taki target agent ko sirf relevant context mile — pura lamba history forward karna zaroori nahi hota
WHY USE?
Aap ek agent se dusre agent ko handoff karte ho. Lekin aap chahte ho ke target agent ko puri chat history na mile, sirf last 2 messages milein. tw is kay lea input_filter ✅ use hoga.
🔹 tool_name_override aur tool_description_override
bas tool ka naam/description change karte hain, history filter nahi karte.
on_handoff ek callback hota hai jo handoff ke waqt trigger hota hai, history ko filter karne ka kaam nahi karta.
🔹 on_handoff
Matlab on_handoff ka use hota hai:
Logging karne ke liye
Custom actions run karne ke liye
Handoff ke waqt special handling dene ke liye
🔹 Agent constructor ka matlab
Constructor = jab aap Agent class ka instance create karte ho (i.e. Agent(...) call karte ho).Tw y optional or required cheezen hoti hain
Required = model ya model_settings.
Optional = name, instructions, tools, handoff.
🔹 Prompt Engineering
Definition: Prompt engineering ka matlab hai model ko sahi aur effective instructions dena taa ke woh desired output generate kare
🔹 Temperature
Creativity control karta hai.
Low value (0–0.3): model deterministic aur factual hota hai (har bar lagbhag same output).
High value (0.7–1.0+): model creative aur random hota hai (har bar thoda naya answer).
Short Analogy:
Low temperature = Serious dost jo hamesha safe jawab deta hai.
High temperature = Fun dost jo har bar naye ideas deta hai, chahe kabhi ajeeb bhi lagay.
🔧 Developer kaha use karta hai?
Ads ya story writing ke liye developer high temperature rakhta hai → output har bar naya aur creative ho.
Technical docs likhne ke liye low temperature rakhta hai → taake har bar reliable aur clear ho.
🔹 TOP_k
---------------Low Top_k (chhoti value, e.g., k=1,2,3)
Model sirf thode hi top words consider karega.
Output zyada restricted, safe aur predictable hoga.
Example: Agar k=1 → model hamesha sabse likely word hi choose karega (bilkul deterministic jaisa).
---------------High Top_k (bari value, e.g., k=20,50,100)
Model bahut saare possible words me se choose karega.
Output zyada varied, diverse aur kabhi-kabhi unexpected hoga.
Example: Agar k=50 → model ke paas bahut options hain, har run pe alag word aa sakta hai.
🔹 Top_p (Nucleus sampling)
Instead of fixed number, yeh probability threshold use karta hai.
Example: agar p=0.9, to model sirf un words ko consider karega jinki cumulative probability 90% banti hai.
Top_p real-world mai aisa hai jaise waiter sirf woh dishes recommend kare jo zyadatar log khate hain, taake suggestions balanced aur natural lagen.
🔒 Safe System Messages for Sensitive Data
System messages = woh hidden instructions jo model ko chalane ke liye diye jaate hain (user ko directly nahi dikhte).
Jab baat sensitive data (jaise passwords, credit card, etc.) ki hoti hai, to system messages carefully design kiye jaate hain taa ke:
Policies enforce ki jayein (e.g., “Never share raw user data with external tools”).
System message ho sakta hai:
“If the user shares account number or password, do not repeat it back. Only use it securely for internal verification.”
👉 Isse fayda: agar user bole “Mera password 12345 hai”, model us password ko repeat ya leak nahi karega — kyunki safe system message ne pehle hi rok diya.
Chain-of-Thought (CoT) prompting — seedha aur simple
Kya hai?
Chain-of-Thought prompting woh technique hai jisme aap model se kehte ho ke woh “sochne ke steps” (yaani reasoning steps) stage by stage likhe — taake complex problems ka jawab sahi aur explainable aaye.
Developer directly chain of thought declare nahi karta. Yani model kea steps degay kea sochyga ye developer ni janskta laken developer 3 methods ky through model ko bta skta hy kea krna hy.
Prompt-level instruction: prompt my instruction dydyga
System message / assistant instruction:: API me ek system message de sakte hay
Developer directly chain of thought declare nahi karta. Yani model kea steps degay kea sochyga ye developer ni janskta laken developer 3 methods ky through model ko bta skta hy kea krna hy.
🔹 Markdown = ek simple tarika text ko format karne ka, jisme normal text ke saath chhote-chhote symbols (#, *, -, etc.) use hote hain.
🔹 Clickable Image
Image ko like link ya button bna dena jis pr click karky dosry page pr jasken.
🔹 Tooltip ek chhota text bubble hota hai jo mouse hover karne par dikhai deta hai.
Ye usually extra info ya hint dene ke liye hota hai.
Example:
YouTube ka like button hover karo → tooltip aata hai “I like this”.
🔹 Clickable Image with Tooltip (Dono combine)
ismy dono kaam hojayengy
Example (real world):
E-commerce website me product image pe hover karne par tooltip: “Click to view details”.
🔹 Numbered and bulleted list
“Numbered and bulleted list formatting” ka matlab hai text ko list form me likhna — jahan har point clearly separate ho.
Bullets yani DOTS(.) Jab order important nahi hota, to bullets use karte hain.
Bullet order important hota hai, to numbering use karte hain.
🔹 Parse = Raw data ko samajhna aur usse structured form me convert karna.
🔹 Pydantic
Pydantic kya hai?
Python library hai.
Mainly use hoti hai data validation aur data parsing ke liye.
Aap ek Model (class) banate ho jisme fields define karte ho, aur Pydantic ensure karta hai ke jo data aaya hai wo correct type ka ho.
🔹 Pydantic me kab error aata hai?
Jab bhi data validation fail hoti hai (type galat ya rule break ho) → Pydantic ValidationError raise karta hai.
🔹 Pydantic se commonly import hone wali cheezen
BaseModel → Data models banane ke liye, automatic validation & parsing karta hai.
Field → Model fields ke liye extra rules/metadata (default values, min/max, description).
ValidationError → Jab data galat hota hai to ye error throw hota hai.
EmailStr → Email format validate karne ke liye ready-made type.
AnyUrl → URL validate karne ke liye.
IPv4Address / IPv6Address → IP addresses validate karne ke liye.
constr, conint, confloat → Constrained (restricted) string, integer, float (length, range waghera ke limits).
RootModel (Pydantic v2) → Agar single value ya list ko model banana ho.
field_validator (v2) / validator (v1) → Custom validation rules likhne ke liye.
ConfigDict (v2) → Model configuration settings ke liye (jaise extra fields allow ya forbid).
🔹 1. BaseModel
Pydantic ka core feature.
Strong data validation + parsing karta hai.
🔹 Dataclass kya hai?
Python ka built-in decorator hai (@dataclass).
Iska kaam hai: aapko boilerplate code (constructor, repr, comparison methods) likhne ki zarurat na ho.
Bas class me fields likho → Python automatically baki kaam kar deta hai.
Normal class ky mukably main data class laga kar kaam krna asan hojata hy.
Dataclass = Python ka shortcut to reduce boilerplate code in classes.
Ye mainly data hold karne wali classes ke liye bana hai (isliye naam bhi “data class” hai). jaise bht sari products post krni ho web pr or sb ka name,price etc likhna hoo
🔹 BaseModel, pydantic.dataclasses.dataclass
BaseModel = Pydantic ka full package (validation + parsing + serialization + configs).
pydantic.dataclasses.dataclass = Normal dataclass with validation only (extra BaseModel features missing).
BaseModel → Zyada popular, zyada powerful, production-grade (validation + parsing + features).
pydantic.dataclasses.dataclass → Rarely used, sirf jab developer ko Python dataclass style pasand ho aur basic validation chahiye.
🔹 Type hints Python me likhe jaate hain jisse aap bata sakte ho variable ka expected type.
name: str
age: int
🧠 Pydantic kya karta:
Agar id string hua → error ya convert karega (depends on type).
Agar is_active “True” likha ho (string form me), to usko bool me convert karega.
Automatically schema generate karega (OpenAPI ya JSON schema format me).
🔹 Schema
“Schema” ka matlab hota hai ek structure jo batata hai data kis format me hona chahiye.
🔹 Using dataclasses as output_type in agents
output_type
Agent ka output ko aik specific form my bna dena.
Aap dataclass ko output_type ke taur par use kar sakte ho.
Matlab model ka textual response us dataclass ke structure me auto-parse ho jaayega.
Feature	Benefit
Structured Output =>Response directly usable as Python object
Auto Validation	Agar=>field missing ho, error milega
Easy to Use =>Developer ko parsing manually nahi karni
Type Safety => Har field ka type fix hota hai (str, float, etc.)
data class ky through validation ni hoti mgr jb out_type generate hoga data class ky through tw ans user tk jany say phly sdk type_validation krleta hy.
🔹 OpenAI Agents SDK
SDK = Software Development Kit
Matlab: ek toolset / library jo developers ko code likhne me madad karti hai.
👉 Example:
Jese mobile app banane ke liye Android SDK hoti hai,
waise hi OpenAI Agents SDK developers ko AI agents banane me help karti hai.
🔹 1. General Concepts — (Base Understanding)
🧠 Agent, Instructions, Tools, Handoff, Output Type, Run / Event System, Runner.
🔹 2. Defaults — (Agar aap define nahi karte)
Parameter	Default Value	Description
model	"gpt-4.1-mini"	---------Agar aap model specify nahi karte
output_type	str	---------------Output plain text hoga agar specify nahi kiya
instructions	"" (empty)	-----Agent ke paas koi special behavior nahi
max_turns	10	-----------------Conversation automatically stop ho jaayegi after 10 turns
tools	[]	---------------------Agent ke paas koi external tool nahi
trace	Enabled	Tracing ---------by default on hoti hai (development ke liye)
🔹 So, Tool = ek external function jise agent call kar sakta hai reasoning ke beech me.
Jab agent ko lagta hai usse koi function use karna hai, wo tool call karta hai.
Agar us tool me error aata hai, SDK automatically handle karta hai — agent crash nahi hota, balki politely respond karta hai.
Usee inquerry khn jati hy :)
User → Main Agent → LLM(LLM decide krta hy querry ka ans my krun ya tool call ya handoff hona chaye) YHN LLM main agent ka use hota hy → (tool ya handoff) → Response
🔹 4. Error Handling During Tool Execution
Kabhi-kabhi tool execution ke dauran error aa sakta hai, jaise:
Wrong arguments → add("five", 7)
Tool unavailable → network down
Internal bug in tool
SDK in errors ko handle karta hai taake agent crash na kare.
| Step                 | Description                                                    |
| -------------------- | -------------------------------------------------------------- |
| 🧠 Model calls tool  | e.g. `search("Lahore weather")`                                |
| ⚠️ Tool throws error | TypeError / ValueError etc.                                    |
| 🛡 SDK catches error | Agent crash hone se bachata hai                                |
| 💬 Model notified    | “Tool failed” ya “error occurred”                              |
| 🔁 Retry or Respond  | Model error ko handle kar sakta hai (retry ya apology message) |
🔹 1. Dynamic Instructions — (Changing Agent Behavior at Runtime)
Jab Agent ke instructions (ya uska behavior) runtime me change kiya jaye,
to use Dynamic Instructions kehte hain.













ek callback hota hai jo handoff ke waqt trigger hota hai, history ko filter karne ka kaam nahi karta.
on_handoff → jaise hi handoff hota hai, console pe log print ho jata hai ke handoff kis agent ko hua.
