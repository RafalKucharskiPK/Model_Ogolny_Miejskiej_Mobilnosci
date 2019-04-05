# Model popytu na przewozy dalekobieżne

1. Ok 20 rejonów w Polsce (Aglomeracje)
2. Potencjał ruchotwórczy to `0.1 x LUDNOSC x MNOZNIK_ATRAKCYJNOSCI`
3. Grawitacja oparta o odległości, albo średnią z czasów KZ/KI
4. Sieć:
* DK
* A/S
* K_70
* K_120
* K_160
* K_220
5. Podział zadań przewozowych oparty o różnice w czasach $u_kz = exp(-0.1*t_kz)/(exp(-0.1*t_kz)+exp(-0.1*t_ki))$
