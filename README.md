I. Prezentarea bazei de date si importarile bibliotecilor necesare

În acest proiect pentru disciplina Econometrie Avansată am folosit setul de date de pe Kaggle numit Loan Approval Classification Dataset, care conține 45.000 de înregistrări și 14 variabile. Scopul proiectului este de a construi un model care clasifică clienții în două categorii pe baza variabilelor disponibile: dacă cererea de împrumut va fi acceptată sau respinsă.
Printre variabile se numără: vârsta persoanei, nivelul de educație atins, venitul anual, suma solicitată pentru împrumut, scorul de credit și existența antecedentelor de neplată a datoriilor.

II. Analiz Exploratorie a Datelor (EDA)

În această secțiune am reprezentat, prin grafice adecvate, toate variabilele din baza de date, am realizat statistici descriptive și am analizat distribuțiile în funcție de variabila țintă loan_status (cererea acceptată vs. respinsă).
De asemenea, acolo unde au existat outlieri superiori (valori extreme), am aplicat winsorizare: valorile peste percentila 99 au fost înlocuite cu chiar valoarea percentilei 99.

III. Simularea valorilor lipsa

Pentru a simula o bază de date realistă, cu lipsă de date, am creat o funcție care introduce 5% valori lipsă la toate variabilele, cu excepția variabilei țintă loan_status. Am construit, de asemenea, un dicționar în care am memorat pentru fiecare variabilă indecșii (înregistrările) unde au fost introduse valorile lipsă, pentru a putea evalua ulterior imputările.

IV. Corelatii si asocieri dintre variabile

Pentru a susține imputări mai complexe, am calculat o serie de coeficienți de corelație/asociere între toate variabilele: Pearson, Phi, Point-Biserial, Kendall Tau, Cramér’s V, Spearman și Eta pătrat (η²). Aceste relații au fost folosite ulterior ca ghid pentru selecția predictori­lor în metodele de imputare.

V. Imputarile Finale

Am folosit tehnici custom și avansate de imputare, printre care:

Imputare pe coloane corelate: pentru fiecare coloană cu valori lipsă dintr-un grup de coloane corelate (conform analizei anterioare), am antrenat regresii liniare pe rândurile complete și am prezis valorile lipsă.

Imputare prin Random Forest Regressor pentru variabile numerice cu relații potențial neliniare.

Imputare pe categorie cu valoarea modală (most-frequent-category), pentru variabilele categorice.

VI. Calcularea erorii de imputarea

După imputări și folosindu-ne de dicționarul cu pozițiile valorilor lipsă, am calculat o eroare de imputare pentru toate variabilele:

pentru variabilele numerice: eroare normalizată (de ex., MAE/RMSE raportată la amplitudine sau deviație standard);

pentru variabilele categorice: acuratețe (proporția de valori imputate corect).
Această secțiune ne-a ajutat să identificăm cele mai performante strategii de imputare.

VII. Regresie Logistica

Am pregătit baza de date astfel:

am creat variabile dummy pentru caracteristicile categorice;

am standardizat variabilele numerice aflate pe scări foarte diferite;

am folosit SMOTE pentru a echilibra clasele (setul inițial era dezechilibrat între cereri aprobate și respinse).

Rezultate:

Accuracy: 0.893

AUC (ROC): 0.954

VIII. Arbori de decizie

Am antrenat un Decision Tree folosind cele mai importante 5 caracteristici și am obținut o acuratețe de 0.909.

IX. XGBoost

Am aplicat XGBoost cu selecție de caracteristici după importanță, ajustarea threshold-ului de decizie și SMOTE pentru echilibrarea claselor.
Rezultat: accuracy = 0.91.
