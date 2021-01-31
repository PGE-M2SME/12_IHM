# 12_IHM

## Trames et registres

Trames et registres reçu pour le STM32.

### Trames Génération flux

/!\ Théorie pour l'instant

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

### Trames Analyse flux (En reception)

Octet| Nom |Valeur| Description
-----|-----|------|--------------
1| Nb_Octets| 0x9 |Nombre d’octet de la trame
2| ID_Sys| 0x3| Système dont la commande est sollicitée
3| ID_Cmd| 0x1| SDI_INFO
4| Vid_format| 2 bits| Se compose de 2 bits, il permet d’afficher la résolution (voir tableau ci-dessous)
6| Frame_format| 3 bits| Se compose de 3 bits, il permet d’afficher le frame format (voir tableau ci-dessous)
7| Vid_active| 1 bit| Une info d’un bit qui indique qu’une ligne du frame est transmise.
8| vblank| 1 bit| Une info d’un bit, si égal 1 en reçoit un flux sinon on ne reçoit rien
9| hblank| 1 bit |Un signal d’un bit est transmis après le transfert de la frame entière


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
