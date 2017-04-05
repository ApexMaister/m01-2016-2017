
# Gestió de Volums Lògics

Descripció del que són
    



##### - Què volen dir les sigles, definició, analogies i exemples de comandes (explicant què fan) vistes a classe de:

    - PV: Physical Volume (Volum Fisic)
    - VG: Volume Group  (Grup de Volums)
    - LV: Logical Volume (Volums Logics)
    
#### - Entorn de pràctiques: Explicar com farem la pràctica detalladament (màquina virtual i afegir tres discs de 200M)

    - Iniciem la maquina virtual , afegim els discs durs Virtio de 200M que es diran vda ,vdb i vdc.


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
