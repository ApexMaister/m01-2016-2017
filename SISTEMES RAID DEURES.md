# SISTEMES RAID

### 1. Resum de sistemes RAID fent servir una taula com la vista a classe.1

| TIPUS DE RAID | Nº MÍNIM DISCS | Nº MÀXIM DISCS FALLATS | CAPACITAT | LECTURA | ESCRIPTURA |
| --------------| -------------- | ---------------------- | --------- | ------- | ---------- |
|    RAID 0     |     2     |      0      | 100% |Excelent | Excelent |
|    RAID 1     | 2 (Màxim) | 1 | 50% |Very Good|  Good |
|    RAID 5     |     3     | 1 | 67%-94%|Very Good|    Good    |
|    RAID 6     |     4     | 2 | 50%-88% | Good | Good |
|    RAID 10    |     4     | 1/Mirror | 50% |Very Good| Good |


### 2. Descripció de la metodologia utilitzada a classe per a fer proves amb màquines virtuals.

- Crear tres discs durs de 200MB a la màquina virtual per crear el sistema RAID.
- Instalar mdadm.
- Crear el RAID que volguem (comandes exercicis següents).
- Crear sistema de fitxers : # mkfs.ext4_dev/md0.
- Muntar RAID : mount_dev/md0_/mnt.
- Crear carpetes o archius.
- Mirar discs : cat_proc/mdstat.
- Veure estat del RAID : mdadm_--detail_/dev/md0.
- dd_if=/dev/zero_of=test.img_bs=4k_count=1000.
- Treure el que hi es fallat : mdadm_dev/md0_-remove_dev/vda.
- mdadm_/dev/md0_--add_/dev/vdc (lliure per reconstruir).

### 3. Comandes i descripció de les mateixes per tal de crear un sistema RAID1.

    mdadm_--create_/dev/md1_--level=1_--raid-devices=2_/deb/sda_deb/sdb

### 4. Comandes i descripció de les mateixes per tal de crear un sistema RAID5.

    mdadm_--create_/deb/md5_--level=5_--raid-devices=3_/deb/sda_deb/sdb

### 5. Comandes i descripció de les mateixes per tal de crear un sistema RAID6.

    mdadm_–create_/deb/md6_--level=6_--raid-devices=4_/deb/sda _deb/sdb

### 6. Comandes i descripció de les mateixes per tal de crear un sistema RAID10.

    mdadm_-create_/deb/md10_--level=10_--raid-devices=4_deb/sda_deb/sdb


