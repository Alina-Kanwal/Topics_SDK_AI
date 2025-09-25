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
