# Bankas klientu termiņdepozīta prognozēšana

Mašīnmācīšanās gala projekts — klasifikācijas modelis, kas prognozē, vai bankas klients piekritīs atvērt termiņdepozītu, balstoties uz demogrāfisko profilu un iepriekšējo kampaņu rezultātiem.

## Problēma

Banka veic telefona mārketinga kampaņas, piedāvājot termiņdepozītus visiem klientiem. Pašreizējā konversija ir tikai 11.7% — tūkstošiem zvanu pa nepiemērotiem klientiem. Šis projekts identificē klientus, kas visticamāk piekritīs, lai banka varētu fokusēt zvanus efektīvāk.

## Datasets

- **Avots:** [UCI Bank Marketing](https://archive.ics.uci.edu/dataset/222/bank+marketing)
- **Izmērs:** 45 211 rindas × 17 kolonnas
- **Target kolonna:** y (yes/no — vai klients piekrita termiņdepozītam)
- **Klases sadalījums:** 88.3% no / 11.7% yes (nesabalansēts)

## Pieeja

- **ML tips:** Binārā klasifikācija
- **Pipeline:** SimpleImputer → StandardScaler / OneHotEncoder → LogisticRegression
- **Validācija:** StratifiedKFold (cv=5) ar class_weight='balanced'
- **Optimizācija:** GridSearchCV
- **Salīdzinātie modeļi:** LogisticRegression, RandomForest, GradientBoosting

## Rezultāti

| Modelis | CV F1 | Std |
|---------|-------|-----|
| Bāzes (LogReg, KFold) | 0.1867 | 0.0368 |
| **LogisticRegression (galīgais)** | **0.5554** | **0.0071** |
| GradientBoosting | 0.5082 | 0.0139 |
| RandomForest | 0.4263 | 0.0109 |

**Galīgais modelis (LogisticRegression):**
- F1 Score: 0.5554
- Recall (yes): 82% — biznesa nozīmīgākais rādītājs
- Precision (yes): 42%
- Accuracy: 84%

**Biznesa vērtība:** Konversija no 11.7% uz 41.6% (3.5x uzlabojums), zvanu skaits samazinās par 77%.

## Galvenās pazīmes

1. **month_mar** (+1.84) — labākais mēnesis pārdošanai
2. **poutcome_success** (+1.59) — iepriekš veiksmīgs kontakts
3. **duration** (+1.50) — ilgāks zvans = lielāka piekrišana
4. **age_group_retired** (+0.69) — pati izveidota pazīme TOP 6

## Kā palaist

1. Klonē repozitoriju:
```
   git clone https://github.com/Mara-Medne/fita-ml-course.git
```

2. Instalē bibliotēkas:
```
   pip install -r requirements.txt
```

3. Atver `week4/week4_homework.ipynb` un izpildi visas šūnas (Kernel → Restart & Run All).

## Mapju struktūra

- `week1/`, `week2/`, `week3/` — iknedēļas mājas darbi
- `week4/` — gala projekts
  - `week4_homework.ipynb` — galvenais notebook
  - `Images/` — vizualizācijas
  - `Presentation/` — prezentācijas faili (PPTX un PDF)
- `data/` — datasets (lokāli)

## Autors

**Māra Medne**  
Mašīnmācīšanās kurss, 2026. gada aprīlis