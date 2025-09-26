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














ek callback hota hai jo handoff ke waqt trigger hota hai, history ko filter karne ka kaam nahi karta.
on_handoff → jaise hi handoff hota hai, console pe log print ho jata hai ke handoff kis agent ko hua.
