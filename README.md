# 12_IHM

## Trames et registres

### Trames Génération flux


Octet | Nom  | Description
-----|------|-------------
1|Nb_Octets| Nombre d’octets de la trame
2|ID_Sys| Système dont la commande est sollicité
3|ID_Cmd| Commande sollicité
4|State| Etat de la demande (OK ou KO)

### Registres Génération flux

State  | Valeur
-----|-------------
OK | 0x1
Erreur | 0x2

### Trames Analyse flux

Octet | Nom  | Description
-----|------|-------------
1|Nb_Octets| Nombre d’octets de la trame
2|ID_Sys| Système dont la commande est sollicité
3|ID_Cmd| Commande sollicité
4|Type_flux| Flux DVI ou SDI
5|Colorimetrie|YCbCr 4:2:2 ou 4:4:4
6<br>7|Frequence| De 25 à 165 MHz (330 avec connecteur B)
8|Format_X| Format en X 
9|Format_Y| Format en Y

### Registres Analyse flux

Type_flux  | Valeur
-----|-------------
SDI | 0x1
DVI | 0x2

Colorimetrie  | Valeur
-----|-------------
YCbCr 4:2:2 | 0x1
YCbCr 4:2:2 | 0x2

### Trames BUS_COM

Octet | Nom  | Description
-----|------|-------------
1|Nb_Octets|Nombre d’octets de la trame
2|ID_Sys|Système dont la commande est sollicité
3|ID_Cmd|Commande sollicité
4|Bus_type|Type de bus utilisé :</br> 0x1 : SPI </br> 0x2 : I2C </br> 0x3 : UART
5|Adresse|Adresse de l'esclave
6|Taille_mot|Taille du mot seul à transmettre en octet (hors spécification de taille ou fréquence)
7|Operateur|Nature de l'opérateur du facteur de bauds. _Exemple : 0 pour multiplication ; 1 pour division_
8|Facteur_baud|Facteur (multiple de 9 600) du baud rate de transmission. **Dans le cas où Operateur = 0, la valeur de Facteur_baud multiplie 9 600. Dans le cas où Operateur = 1, la valeur de Facteur_baud divise 9 600.** </br>_Exemple : </br> Operateur = 1; Facteur_baud = 0x20 (32) ==> Bauds = 300 </br> Operateur = 0; Facteur_baud = 0x68 (104) ==> Bauds = 998 400_
9 <br>...<br>n|Mot|Mot à transmettre (dépend de Taille_mot)

### Registres BUS_COM

Type_protocol  | Valeur
-----|-------------
UART| 0x1
I2C | 0x2
SPI | 0x3
