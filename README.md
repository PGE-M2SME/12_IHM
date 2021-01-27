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
1|Nb_Octets| Nombre d’octets de la trame
2|ID_Sys| Système dont la commande est sollicité
3|ID_Cmd| Commande sollicité
4|Type_protocol| UART / I2C / SPI
5<br>6|Baud| Baud rate si UART (multiple 9600)
7<br>...<br>N|Data|Octets dédiés aux data. On peut en mettre autant qu'on veut (dans la limite du possible) car la longueur de la trame est définit avec Nb_Octets

### Registres BUS_COM

Type_protocol  | Valeur
-----|-------------
UART| 0x1
I2C | 0x2
SPI | 0x3