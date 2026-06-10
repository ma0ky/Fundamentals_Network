Un paquet est une suite d'octects 

hexadecimal > important pour lire un paquet comme lire une phrase
Lois base = 2^n
![](Pasted%20image%2020260607232309.png)

## Représentation des nombres
### Conversion du binaire en décimal

on prend un octet comme : 11010010
Il faut savoir qu'un octet là il contient 8bits 
Le binaire contient 2 caractères (0 et 1)
Le décimal contient 10 caractères (0,1,2,3,4,5,6,7,8,9)


| 2^7 | 2^6 | 2^5 | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 | Poids binaire                  |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------------------ |
| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   | Poids binaire simplifié        |
| 1   | 1   | 0   | 1   | 0   | 0   | 1   | 0   | Nombre binaire (=octet)        |
| 128 | 64  | 0   | 16  | 0   | 0   | 2   | 0   | Poids binaire x nombre binaire |
|     |     |     |     |     |     |     | 210 | Resultat                       |
Questions : 
- Pourquoi c'est des 2exposants ? >> c'est en base 2 comme le décimal qui est lui en base 10 et l'héxadécimal en base 16
- Comment est-ce que sa communique avec l'ordinateur et à quelle échelle ? C'est surtout l'héxadécimal qui communique (héxadécimal est juste du binaire écrit différament et compacter sans perte) c'est pour ça que tout les outils  comme Wirehsark parlent héxadécimal. >>"un dump hexa, c'est du binaire déguisé." Pour le décimal, ce n'est pas une puissance de 2 aucun découpage peut-être propre donc ce n'est pas du binaire compacté sans perte.
- A quoi sa sert concrêtement ? >> à communiquer dans le langage de la machine qui lui comprend que le binaire, l'hexa sert aux humains à le lire.
- Pourquoi un octet c'est seulement 8bits et pas 7 ou 9 ? >> On prend 8 car c'est divisable parfaitement par 2 donc binaire 8=2^3 , l'ascii original tenait sur 7bits(128 = 128 caractères) donc on est passer à 8bits(256) pour laisser place aux symboles et accents, IBM (entreprise multinationale américaine présente dans les domaines du matériel informatique, du logiciel et des services informatiques) a standardisé avec son System/360 (1964) toute l'industrie a suivi.
- Soyons honnête est-ce que c'est important et utile de connaître 2^7 = 128 sinon à chaque fois que sa convertit du binaire en décimale je pense direct à 128 que 2^7 ? >> connaître ses puissances
- Comment devrais-je mieux faire la convertion ? >> oui 
- Est-ce que c'est la bonne méthode ? >> oui,
- Le 2^0 compte t-il comme un bit >> oui
### Conversion du binaire en héxadécimal

L'héxadecimal contient 16 caractères (0,1,2,3,4,5,6,7,8,9), et (A,B,C,D,E,F)
#### Méthode 1 ( pas faire)

| binaire | hexadécimale | x   | binaire   | hexadécimale | binaire   | hexadécimale |
| ------- | ------------ | --- | --------- | ------------ | --------- | ------------ |
| 0000    | 0            | x   | 1010      | A            | 0001 0100 | 14           |
| 0001    | 1            | x   | 1011      | B            | 0001 0101 | 15           |
| 0010    | 2            | x   | 1100      | C            | 0001 0110 | 16           |
| 0011    | 3            | x   | 1101      | D            | 0001 0111 | 17           |
| 0100    | 4            | x   | 1110      | E            | 0001 1000 | 18           |
| 0101    | 5            | x   | 1111      | F            | 0001 1001 | 19           |
| 0110    | 6            | x   | 0001 0000 | 10           | 0001 1010 | 1A           |
| 0111    | 7            | x   | 0001 0001 | 11           | 0001 1011 | 1B           |
| 1000    | 8            | x   | 0001 0010 | 12           | 0001 1100 | 1C           |
| 1001    | 9            | x   | 0001 0011 | 13           | 0001 1101 | 1D           |

On va donc prendre un octet comme : 11010010
On va découper cet octet en 2 : 1101 0010

| 1101 | 0010 |
| ---- | ---- |
| D    | 2    |
donc le résulat de la conversion est D2

#### Méthode 2 (faire)

On a un octet de 11010010, qu'on va diviser en 2 pour faire un paquet de 4bits (nibble) : 1101 0010 avec des poids du bas donc 8-4-2-1
on va prendre 1101 == 8+4+0+1 >> 13 et 0010 == 0+0+2+0 >> 2 
si on prend 13 sachant que A commence à 10 sa donne D et 2=2
donc le résultat est D2


Questions : 
- Dois-je apprendre le tableau par coeur ? >> non je ne dois pas pas apprendre par coeur et faut calculer chaque groupe de 4bits comme en décimal, qui peut aussi s'appliquer pour l'héxadécimale
- Existe-il une technique pour trouver de la bonne façon le résulat ? >> Méthode 2, par nibble
- Est-ce que c'est la bonne méthode ? >> Méthode 2, par nibble

## Endianness

On a vu des nombres qui tenait sur 1 octet (8bits = 2^8 = 0 à 255), mais beaucoup dépassent un octet comme le port 443(HTTPS). 443 = 0x01BB > 2 octets 01 et BB 

Cours 
Tu dois ranger ces 2 octets en mémoire, l'un après l'autre, du plus bas au plus haut. Lequel tu mets **en premier** (à l'adresse la plus basse) : `01` ou `BB` ? Et surtout — d'après toi, est-ce qu'il y a **une seule bonne réponse** ? 
->> Même si on trie du plus bas au plus haut, il n'y aura pas une seule bonne réponse valide. 
0x01BB ne change pas tout seul( le sens de la donnée n'influence rien), ce qui change c'est l'ordre des octets en mémoire qui est déterminer par le système ou la convention d'un protocole utiliser.
Il existe 2 conventions possibles :

| 0x01BB | Big-endian    | [01][BB] | l'octet de poid fort en premier   |
| ------ | ------------- | -------- | --------------------------------- |
| 0x01BB | little-endian | [BB][01] | l'octet de poid faible en premier |

Big-endian >> l'octet du poid le plus fort est à l'adresse la plus basse :
- adresse 1000 : 01
- adresse 1001 : BB
Little-endian >> l'octet du poid le plus faible est à l'adresse la plus basse:
- adresse 1000 : BB
- adresse 1001 : 01

L'octet du poids fort est celui en premier (MSB, Most Significant Byte) tandis que le poid faible est en deuxième (LSB, Least Significant Byte). Par exemple : 0x01BB
1234 = 1 est vu comme 1000 tandis que 2 est vu comme 200 etc

- 0x01BB >> 01 est multiplié par 256 tandis que BB est mulitplié par 1 .
Il faut regarder sa position dans le nombre et non dans sa forme binaire comme une conversion 

Le sens aussi est définit par le programme, pas par la mémoire : 
- 0x01BB est le port 443 selon l'endianness
- 0x01BB comme une température 
- 0x01BB ou n'importe quoi
L'interprétation change, mais le rangement des octets reste identique pour une même machine

Le réseau a choisit big-endian comme convention officielle.
Dans les années 70 et 80, lorsque les protocoles fondateurs d'internet ont émergés (TCP/IP qui ont été développés pour le réseau ARPANET, la plupart des machines, ordinateurs et serveurs (mainframes IBM, processeurs Motorola 68000, ...) utilisaient majoritairement le format Big-Endian.
Le choix s'est porté naturellement sur les machines dominantes qui accèdaient au réseau via cette convention à l'époque.
Les équipements réseaux comme le routeur ont une prise de précision plus rapide car les bits de poids forts sont lu en permier comme ils sont à gauche ( adresse IPv4 qui vaut 32bits soit 4octets) donc le routeur peut déjà commencer le chemin vers l'hôte en ayant déjà une idée de la destination.
Pour les humains, c'était plus facile au niveau du débogagecar le Big-endian correspond à la façon dont nous les humains nous lisons (de gauche à droite), comme les ingénieurs d'autre fois d'autrefois devait souvent lire des dumps de paquets réseaux pour déboguer les communications.
Le fait que l'en-tête notamment les adresses IP et les ports soient directement lisibles directement à gauche leurs rendaient la tâche moins ardue.

Les données sont pas générés depuis le little-endian mais vient avant, c'est comme ça qu'on détermine le poids fort du faible. 
- **La valeur** `0x01BB` : c'est des maths pures. Elle existe « avant », indépendamment de toute machine. C'est elle qui définit qui est le MSB (`01`, l'octet de poids fort) et qui est le LSB (`BB`, l'octet de poids faible). Ça, aucune machine ne peut le changer — c'est de l'arithmétique.
- **Notre écriture** `0x01BB` sur le papier : une convention _humaine_. On écrit le gros bout à gauche, comme en décimal (on écrit « 256 », pas « 652 »).
- **Le stockage en mémoire** : c'est _seulement ici_ que l'endianness débarque. Elle ne touche ni à la valeur, ni à notre façon de l'écrire — elle décide juste **quel octet va à quelle adresse**.

Question
Sur ta machine Debian, tu stockes le nombre `0x01BB`. Une première fois c'est un **numéro de port**, une deuxième fois c'est la **taille d'un fichier**. Les octets seront-ils rangés **pareil ou différemment** dans les deux cas ? Et **pourquoi** ?
->> Si ma debian stocke 0x01BB même si unepremière fois c'est un port ou l'autre fois c'est la taille d'un fichier, l'ordre des octets ne change pas car le sens de la donnée n'a aucune emprise sur l'ordre des octets, c'est le système et la convention qui a une emprise.

Exercice
0xDEADBEEF
Découpe-la en octets, puis donne-moi sa représentation en mémoire **(a)** en big-endian et **(b)** en little-endian. Et dis-moi laquelle ta **Debian** utilise.

| 0xDEADBEEF | a   | [DE][AD][BE][EF] |
| ---------- | --- | ---------------- |
| 0xDEADBEEF | b   | [EF][BE][AD][DE] |
Ma debian utilise du little-endian donc b.
Tout les architectures intel x86 et amd64/x86-64 utilise littme-endian.

L'endianness réordonne les octets en entier mais pas les bits à l'intérieur de celui-ci.
### Mémoire

Endianness détermine dans quel ordre on classe les octets dans la mémoire.
Comme dit précédemment dans la mémoire c'est stocker sous forme d'adresses.
Exemple : 0x01BB
Big-endian >> l'octet le plus fort est à l'adresse la plus basse :
- adresse 1000 : 01
- adresse 1001 : BB
Little-endian >> l'octet le plus faible est à l'adresse la plus basse:
- adresse 1000 : BB
- adresse 1001 : 01

En mémoire, l'unité la plus petite qui a une **adresse**, c'est l'**octet**. Le processeur distribue les adresses octet par octet — il n'existe pas d'adresse pour un bit isolé. Donc le plus petit truc que l'endianness _peut_ déplacer, c'est un octet entier. Les bits d'un octet partagent la même adresse → impossible de les réordonner individuellement.

#### Représentation de la mémoire 

représentation mémoire d'une structure simple : ordre des champs, alignement

Chaque octet à une adresse , certaines données qui font plusieurs octets peuvent prendre plusieurs adresses.
Par exemple: un entier 1000 et il commence à l'adresse 1010 et finit 1013 comme il prend 4 octets donc 4 adresses 

La structure de la mémoire est un ensemble d'informations différentes(champs) qui concerne la même chose. 

| Spider-man |              |           |
| ---------- | ------------ | --------- |
| Nom        | Peter Parker | 11 octets |
| Pouvoirs   | Toile        | 5 octets  |
| Sexe       | M            | 1 octet   |
| Age        | 22           | 2 octets  |
L'ordre des champs dans une mémoire pour une même information(dossier) dépend de l'ordre que dans lequel tu le ranges dans le dossier de base.
Exemple A :

| Spider-man         |                  |          |          |
| ------------------ | ---------------- | -------- | -------- |
| Nom : Peter Parker | Pouvoirs : Toile | Sexe : M | Age : 22 |
| 11 octets          | 5 octets         | 1 octet  | 2 octets |
Exemple B :

| Spider-man |          |                    |                  |
| ---------- | -------- | ------------------ | ---------------- |
| Sexe : M   | Age : 22 | Nom : Peter Parker | Pouvoirs : Toile |
| 1 octet    | 2 octets | 11 octets          | 5 octets         |
Même données mais dans un ordre différents, on pourrait penser que c'est la même chose mais loin de là, c'est là qu'intervient l'alignement.

Il existe une règle de l'alignement : Un champ doit commencer à une adresse qui est un multiple de sa taille. Contrainte que le processeur a c'est qu'il lit par blocs réguliers.
Voici les règles d'alignements :

| Types de données     | Exemple                            | Taille   | adresses              |
| -------------------- | ---------------------------------- | -------- | --------------------- |
| Caractères (char)    | [a][B][5][@]                       | 1 octet  | nimporte où           |
| Entier court (short) | entre -32 768 et 32 768            | 2 octets | 0, 2, 4, 6, 8, ...    |
| Entier (int)         | entre -2 milliards et +2 milliards | 4 octets | 0, 2, 4, 8, 12,...    |
| Double (double)      | nombre à virgules : [3,14] [0,001] | 8 octets | 0, 8, 16, 24, 32, ... |

| Spider-man       |          |          |                    |                |                 |
| ---------------- | -------- | -------- | ------------------ | -------------- | --------------- |
| Pouvoirs : Toile | Sexe : M | Age : 22 | Nom : Peter Parker | Padding de fin |                 |
| 5 octets         | 1 octets | 2 octets | 11 octets          | 1 octet        |                 |
| 0 à 4            | 5        | 6 à 7    | 8 à 19             | 20             | Adresse mémoire |

Le padding est du remplissage d'octets vides insérer automatiquement entre les champs pour respecter les règles d'alignements .
Dans notre cas, on en a pas eu besoin mais avec padding on aurait pu faire :
On a rajouter un padding de fin avec la règle "la taille totale d'une structure doit toujours être un multiple de son alignement le plus grand." toute les autres valueurs sont du chart donc 1 octet tandis que Age est de 2 octets, c'est le plus grand donc v=on va chercher un total qui est le multiple de celui-ci, ce qui donne à rajouter un padding de 1 pour donner 20

### Communication

On a pu voir que ma debian ( architecture de  x86) utilise la convention little-endian tandis que le réseau utilise le big-endian. 
Donc techniquement le pc et le réseau sont tout le temps en désaccord. La solution est qu'à chaque fois qu'un nombre de plus d'un octet part, il est converti automatiquement, maintenant qui est-ce qui fait la conversion, c'est tout simplement les programmes informatiques qui le font.
La conversion a lieu juste avant l'envoi et après du message, ce n'est pas la carte réseau qui convertit mais le C, le Python où le service système de la debian qui prépare les données en question en utilisant des fonctions de conversion standardisées.
Exemple :
Dans le langage de programmation C, une bibilothèque système nommé "glibc" a certaines fonctions qui le font

| htons()   | Host to Network Short | convertit un entier de 16 bits (2^16 == 2 octets) en Big-Endian idéal pour l'envoi des numéros de ports |
| --------- | --------------------- | ------------------------------------------------------------------------------------------------------- |
| htonl()   | Host to Network Long  | convertit un entier de 32 bits (2^32 == 4 octets) en Big-Endian idéal pour l'envoi des adresses IPv4    |
| ntohs()   | Network to Host Short | fait l'inverse                                                                                          |
| ntohl()   | Network to Host Long  | fait l'inverse                                                                                          |
| htobe64() | Host to Big-Endian    | convertit un entier de 64bits (=8 octets ) en big_endian                                                |
| be64toh() | Big-Endian to Host    | convertit le big-endian à l'architecture host                                                           |
#### Exemple 

![](Pasted%20image%2020260608112956.png)
Imaginons qu'on veut envoyer un paquet à quelqu'un, imaginons que le paquet est une lettre à la poste 

| L'enveloppe (En-tête) : | IP Source                                         | IP Destination | Port | -> Format réseau (Big-endian) obligatoire |
| ----------------------- | ------------------------------------------------- | -------------- | ---- | ----------------------------------------- |
| Le contenu (Payload)    | "Bonjour, voici le cours d'aujourd'hui" ou un pdf |                |      |                                           |

Avant d'envoyer, ce qui est convertie est l'en-tête pour que le réseau comprenne où envoyer quand le switch et le routeur le réceptionne. Dans notre cas, la Debian utilise les fonctions htons() et htonl() pour écrire l'adresse IP et le port en Big-Endian.

Mais le paylod lui, son contenu reste inchanger ? > le réseau ne lit pas le contenu de la lettre donc pas besoin d'éventuels convertions pour qu'il soit en Big-endian :
- si le contenu c'est du texte , chaque lettre vaut 1 octet donc il n'y a pas de poids ni de poids faible donc pas besoin de l'endianess, donc pas de conversion
- si le contenu est plus gros ( 4 octets ou + ) comme une adresse IP, la conversion se fait directement en Big-endian
- si sa mélange les 2 , c'est que le contenu qui a besoin d'être convertit qui convertit et après le programme "colle" les morceaux pour que le tout fasse un bloc de 5 octets indépendamment de chaque.

En conclusion, le processeur dicté par le programme (comme Gmail ou WhatsApp) ne convertit que l'en-tête en Big-endian et pour ce qui est du contenu, il ne cherche même pas à savoir, il découpe juste le tout en petit paquets et met des en-têtes en Big-endian autour et envoit le tout depuis la carte réseau ( processeur envoit paquet dans la RAM > carte réseau qui prend les octets qui le concerne et qui constitue la requête dans la RAM > qui transforme le tout en signaux pour l'ejecter dans le cables )
## Axes d'entraînements

### DUMP À ANALYSER

Offset 0000 : 01 BB 00 50 48 54 54 50 EF BE AD DE 00 00 01 F4 

a) octets 0-1 (01 BB), 16 bits big-endian → valeur décimale ? 
-> on peut voir qu'il y a 2 octets dont on va découper par poids de position
![](Pasted%20image%2020260608161336.png)
On sait que B = 11 en décimale

| 0               | 1              | B              | B             | base 16    |
| --------------- | -------------- | -------------- | ------------- | ---------- |
| 0 * 16^3(=4096) | 1 * 16^2(=256) | 11 * 16^1(=16) | 11 * 16^0(=1) | conversion |
| 0               | 256            | 176            | 11            | conversion |
|                 |                |                | 443           | base 10    |

b) octets 2-3 (00 50), 16 bits big-endian → valeur décimale ? 
-> on peut voir qu'il y a 2 octets qu'on va découper en poids de position

| 0        | 0        | 5        | 0        | base 16    |
| -------- | -------- | -------- | -------- | ---------- |
| 0 * 16^3 | 0 * 16^2 | 5 * 16^1 | 0 * 16^0 | conversion |
| 0        | 0        | 80       | 0        | conversion |
|          |          |          | 80       | base 10    |


c) octets 4-7 (48 54 54 50) en ASCII → quel mot ? (indice : 0x48 = 'H', lettres consécutives) 
->  On a de l'hex qu'on veut convertir en ASCII, il faut savoir qu'il existe des repères 
https://www.ascii-code.com/fr

| Catégorie       | Plage en hexadécimal | Point de repère ASCII |
| --------------- | -------------------- | --------------------- |
| Chiffres        | 30 à 39              | 30 = 0                |
| Alphabets(Maj)  | 41 à 5A              | 41 = A                |
| Alpahabets(Min) | 61 à 7A              | 61 = a                |
Donc nous notre suite d'héxadécimal commence par 4 ou 5 donc c'est forcement une majuscule .
Pour 48, on commence à compter à part de 41= A , sa donne nous H.
Pour 54, on repart aussi de 41 mais faut comprendre qu'après 49 sa fait (4A à 4F == J à O) pour reprendre à 50 qui sera P faut juste faire +4 pour tomber sur notre lettre qui est T.
2 * 54 donc 2 * P
Et donc 50 pour en revenir c'est P 
Résulat : HTTP

d) octets 8-11 (EF BE AD DE) lus en LITTLE-endian, 32 bits → valeur hexa ?
-> comme on a une suite d'octets et qu'on veut en little-endian, on inverse ce qui donne DE AD BE EF
-> 

e) octets 12-15 (00 00 01 F4), 32 bits big-endian → valeur décimale ?
-> on va chercher la valeur décimale donc on va les découper par poids de position

| 0        | 0        | 0        | 0        | 0        | 1        | F         | 4        | base de 16 |
| -------- | -------- | -------- | -------- | -------- | -------- | --------- | -------- | ---------- |
| 0 * 16^7 | 0 * 16^6 | 0 * 16^5 | 0 * 16^4 | 0 * 16^3 | 1 * 16^2 | 15 * 16^1 | 4 * 16^0 | conversion |
| 0        | 0        | 0        | 0        | 0        | 256      | 240       | 4        | conversion |
|          |          |          |          |          |          |           | 500      | base de 10 |

## Exercice

- exercices automatismes
#### EX.1 — Compter en hexa (combler le trou post-F)

Consigne : pars d'un nombre hexa donné, écris les valeurs suivantes en ajoutant 1 à chaque pas. But : que « ...F, 10, 11 » devienne réflexe. Règle : comme en décimal, dès qu'un chiffre dépasse F (=15) il repasse à 0 et on ajoute 1 à gauche. 
Exemples (réponses incluses) : 
- Depuis 0E, +1 six fois → 0E, 0F, 10, 11, 12, 13, 14 
- Depuis 1D, +1 cinq fois → 1D, 1E, 1F, 20, 21, 22 
- Depuis F8, +1 six fois → F8, F9, FA, FB, FC, FD, FE (puis FF, 100...)
- Progression : +1 → +2 → compter à rebours (−1) depuis 0x21.

#### EX.2 — Conversions éclair (octet)

Consigne : pour chaque octet, donne décimal ET hexa par calcul des nibbles (8-4-2-1), en moins de 30 s. Pas de tableau. 
Méthode : couper en 2 nibbles, calculer chacun, mapper 10-15 → A-F.
Exemples (réponses incluses) : 
- 1011 0100 → déc 180, hexa B4
- 1111 1111 → déc 255, hexa FF
- 0x6C → bin 0110 1100, déc 108 
- 0xA0 → bin 1010 0000, déc 160 
- Progression : binaire→(déc,hex) → hexa→(bin,déc) → décimal→(bin,hex) (le plus dur : diviser par 16).

#### EX.3 — Endianness (ranger / lire)

Consigne : pour un nombre multi-octets, écris-le en big-endian ET little-endian, puis dis ce qu'une machine little-endian lirait si les octets venaient du réseau (big-endian). 
Rappel : l'endianness réordonne les OCTETS, jamais les bits internes. 
Exemples (réponses incluses) : 
- 0xCAFE → BE [CA] [FE] · LE [FE] [CA] 
- 0x12345678 → BE [12] [34] [56] [78] · LE [78] [56] [34] [12] 
- Port 0x1F90 (8080) reçu [1F] [90] : lu BE = 0x1F90 = 8080 (correct) · lu LE = 0x901F = 36895 (faux) 
- Progression : 2 octets → 4 octets → scénario « mauvaise lecture réseau ».