
# Gestió de Volums Lògics

#### Descripció del que són: (Logical Volume Management)

LVM és una implementació d'un administrador de volums lògics per al nucli Linux.

LVM inclou moltes de les característiques que s'esperen d'un administrador de volums, incloent:

- Redimensionament de grups lògics
- Redimensionament de volums lògics
- Instantànies de només lectura (LVM2 ofereix lectura i escriptura)
- RAID0 de volums lògics.
    



### - Què volen dir les sigles, definició, analogies i exemples de comandes (explicant què fan) vistes a classe de:


#### PV: Volum físic / Physical Volume (PV).

Un volum físic  és un dispositiu d'emmagatzematge, o més correctament expressat un dispositiu de bloc. Pot ser un disc dur, una partició, una targeta SD, 1 floppy, un dispositiu RAID, un dispositiu loop (que converteix un fitxer a un dispositiu de bloc), un dispositiu xifrat, fins i tot un volum lògic (LV) pot usar-se de PV !. Per simplificar direm que un PV és una font d'emmagatzematge, és a dir un dispositiu que ens proporciona espai. 
    
    
#### VG: Volume Group  (Grup de Volums)

 Podem dir que un VG és una espècie de disc dur virtual . Un VG és un "disc" compost de un o més PVs i que creix simplement afegint més PVs. A diferència d'un disc real, un VG pot créixer amb el temps, només cal "donar-li" un PV més. En una màquina amb un sol disc podem crear un VG que estigui compost per un només PV (el disc físic o una de les seves particions). Si amb el temps ens vam quedar sense espai al VG, vam comprar un altre disc (PV), la qual afegim al VG i la resta és transparent per a sistemes de fitxers, processos o usuaris.


#### LV: Logical Volume (Volums Logics)

 Els volums lògics  són "el producte final" de l'LVM. Són aquests dispositius els que farem servir per crear sistemes de fitxers, swap, discos per a màquines virtuals, etc ... Per seguir amb l'analogia del "disc dur virtual" que és el VG, els LVs serien les particions. Amb els que treballarem realment. A diferència de "els seus primeres" les particions tradicionals, els LVs poden créixer (mentre hi hagi espai en el VG) independentment de la posició en què estiguin, fins i tot expandint per diferents PVs. Un LV de 1G pot estar compost de 200MB procedents d'un disc dur, 400MB d'un RAID programari, i 400MB d'una partició en un tercer dispositiu físic. L'únic requisit és que tot els PVs pertanyin al mateix VG. Per descomptat, encara que possible, no sembla una combinació amb molt sentit.


    
#### - Entorn de pràctiques: Explicar com farem la pràctica detalladament (màquina virtual i afegir tres discs de 200M)

Iniciem una maquina virtual , te que ser preferiblement Fedora o Debian , en el cas de no tenir anem al mirror.escoladeltreball.org i ens baixem una iso. Una vegada creada la maquina escollim la opcio de modificar abans de arrancarla i li afegim tres disc virtuals 


#### - Pràctica 1: Creació d'un volum lògic a partir d'un dels tres discs durs (vda per exemple). Aquest volum lògic ha de ser del total de capacitat del disc. El volum de grup s'ha de dir practica1 i el volum lògic dades.

    - vg create practica1 /dev/vda
    
    - lvcreate -L 100%FREE -n dades practica1 





#### - Pràctica 2: Creació d'un sistema de fitxers xfs al volum lògic creat i muntatge a /mnt. També s'ha de crear un fitxer amb dd de 180MB.

     mkfs.ext4 /dev/practica1/dades
     
      mount /dev/practica1/dade
    
      dd if=/dev/zero of=test.img bs=1k count=180000


#### - Pràctica 3: Creació d'un RAID 1 als dos discos sobrants (vdb i vdc per exemple).

    mdadm -- create /dev/md1 -level=1 --raid-devices=2 /dev/vdb /dev/vdc



#### - Pràctica 4: Ampliació del volum lògic de dades al raid.



    lv extend -L 50M /dev/practica1/dades



#### - Pràctica 5: Ampliació del sistema de fitxers xfs al tamany actual del volum lògic dades (s'ha de poder fer sense desmuntar-lo de /mnt ja que és xfs). Una vegada creat crearem un nou fitxer de 180M.

