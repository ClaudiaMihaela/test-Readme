# Analiza Politicilor de Învățare în Federated Learning (FL) prin Rețele Neurale și Fictitious Play

Acest proiect implementează un cadru de simulare și analiză pentru adoptarea strategiilor în sistemele de **Federated Learning (FL)**. Codul utilizează tehnici de rețele neurale pentru învățarea politicilor (*Policy Learning*) și algoritmi din teoria jocurilor (**Fictitious Play**) pentru a prezice echilibrul Nash în diferite scenarii de adoptare a tehnologiei.

## 📋 Cuprins
1. Descriere Generală
2. Scenarii Analizate
3. Componente Software
4. Instalare și Utilizare
5. Interpretarea Rezultatelor

---

## 🚀 Descriere Generală
Codul este structurat în două secțiuni majore de analiză computațională:

1.  **Neural Network Policy Learning:** Antrenează o rețea de tip *feed-forward* pentru a aproxima strategia optimă a unui nod dintr-un sistem FL, bazându-se pe matrice de recompense (*payoff matrices*).
2.  **Dinamica Învățării și Stabilitate:** Utilizează algoritmul *Fictitious Play* pentru a observa cum converg strategiile jucătorilor în timp spre un punct de echilibru și analizează senzitivitatea acestui echilibru în funcție de beneficiile de acuratețe.



[Image of neural network architecture diagram]


---

## 📊 Scenarii Analizate
Sunt evaluate patru contexte distincte, reprezentate prin matrice de utilitate, pentru a observa comportamentul agenților:

* **Scenariul (a) - Early Adopters (EA):** Beneficii ridicate pentru adoptarea timpurie.
* **Scenariul (b) - Late Adopters (LA):** Recompense optimizate pentru tranziția întârziată.
* **Scenariul (c) - Rezistență Ridicată:** Utilitate scăzută pentru cooperare, simulând un mediu sceptic sau costuri mari de participare.
* **Scenariul (d) - Populație Echilibrată:** Testarea stabilității într-un mediu cu beneficii reduse.

---

## 🛠️ Componente Software

### 1. Neural Network Policy Learning
* **Arhitectură:** MLP (Multi-Layer Perceptron) cu două straturi ascunse de dimensiuni `[10 5]`.
* **Intrare (Input):** Distribuții aleatorii de probabilitate ale strategiilor din rețea.
* **Ieșire (Output):** Clasificarea strategiei optime (EA, LA sau R).
* **Antrenare:** Folosește algoritmul Levenberg-Marquardt pentru minimizarea MSE (Mean Squared Error).

### 2. Fictitious Play (Teoria Jocurilor)
* Implementează un model de învățare iterativă unde fiecare jucător își alege cea mai bună replică (*Best Response*) bazându-se pe frecvența acțiunilor trecute ale adversarilor.
* Identifică numeric punctele de **Echilibru Nash (NE)** pentru fiecare scenariu.



### 3. Analiza de Senzitivitate
* Evaluează robustețea echilibrului pentru strategia "Late Adopter".
* Variază parametrul de beneficiu ($b$) pentru a identifica pragul de stabilitate al sistemului.

---

## 💻 Instalare și Utilizare
1.  Asigurați-vă că aveți instalat **MATLAB** (versiune recomandată R2021a sau mai recentă).
2.  Necesită **Deep Learning Toolbox** pentru funcțiile `feedforwardnet` și `train`.
3.  Copiați codul într-un script de tip `.m` (ex: `analiza_FL.m`).
4.  Rulați scriptul. Acesta va genera automat două ferestre grafice maximizate cu rezultatele analizei.

---

## 📈 Interpretarea Rezultatelor

| Grafic | Explicație |
| :--- | :--- |
| **Training Loss** | Indică eroarea de aproximare a rețelei. O curbă descendentă confirmă faptul că NN a învățat corect matricea de payoff. |
| **Politica Învățată** | Reprezintă probabilitatea ca un agent să aleagă o anumită strategie FL în funcție de contextul învățat. |
| **Dinamica Învățării** | Ilustrează convergența strategiilor spre echilibru pe parcursul celor 1000 de iterații. |
| **Stabilitate LA** | Arată intervalul de parametri în care strategia "Late Adopter" rămâne cea mai bună opțiune. |

---

## 📝 Note Tehnice
* Normalizarea datelor se face prin `X ./ sum(X, 2)` pentru a asigura suma probabilităților egală cu 1.
* S-a introdus un factor de zgomot (`0.08 * rand`) în etichetarea datelor pentru a permite vizualizarea progresului pierderii (*loss*) în timpul antrenării rețelei.
